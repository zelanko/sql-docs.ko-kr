---
title: SQL에 대한 R 코드 변환
description: SQL Server의 관계형 데이터베이스에 대한 솔루션 배포 및 데이터 액세스를 위해 R 코드를 SQL Server 저장 프로시저로 마이그레이션합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 882ce47467a38ab4a891f632c9598070e13494e3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727541"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>SQL Server(데이터베이스 내) 인스턴스에서 실행할 수 있도록 R 코드를 변환합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server에서 작동하도록 R 코드를 수정하는 방법에 대한 개략적인 지침을 제공합니다. 

R Studio 또는 다른 환경에서 SQL Server로 R 코드를 이동할 때 대부분의 경우 추가 수정 없이 코드가 작동합니다(예: 일부 입력을 사용하고 값을 반환하는 함수와 같이 간단한 코드). 변경을 최소화하고 다양한 실행 컨텍스트에서 실행을 지원하는 **RevoScaleR** 또는 **MicrosoftML** 패키지를 사용하는 솔루션을 쉽게 포팅할 수도 있습니다.

그러나 다음 중 하나라도 적용된다면 코드에 상당한 변경이 필요할 수 있습니다.

+ 네트워크에 액세스하거나 SQL Server에 설치될 수 없는 R 라이브러리를 사용합니다.
+ 이 코드는 Excel 워크시트, 공유 파일 및 기타 데이터베이스와 같은 SQL Server 외부에 있는 데이터 원본을 개별적으로 호출합니다. 
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 *\@script* 매개 변수에서 코드를 실행하고 저장 프로시저를 매개 변수화하려고 합니다.
+ 원래 솔루션에는 데이터 준비, 기능 엔지니어링 및 모델 학습, 채점 또는 보고와 같이 독립적으로 실행되는 경우 프로덕션 환경에서 보다 효율적일 수 있는 여러 단계가 포함됩니다.
+ 라이브러리를 변경하거나, 병렬 실행을 사용하거나, 일부 처리를 SQL Server로 오프로드하여 성능을 개선하고 최적화하려고 합니다. 

## <a name="step-1-plan-requirements-and-resources"></a>1단계. 요구 사항 및 리소스 계획

**패키지**

+ 필요한 패키지를 결정하고 SQL Server에서 작동하는지 확인합니다.
 
+ Machine Learning Services에서 사용하는 기본 패키지 라이브러리에 패키지를 미리 설치합니다. 사용자 라이브러리는 지원되지 않습니다.

**데이터 원본** 

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 R 코드를 포함하려면 기본 및 보조 데이터 원본을 식별합니다. 

    + **기본** 데이터 원본은 모델 학습 데이터 또는 예측을 위한 입력 데이터와 같은 큰 데이터 세트입니다. 가장 큰 데이터 세트를 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 입력 매개 변수에 매핑하도록 계획합니다.

    + **보조** 데이터 원본은 일반적으로 요소 목록 또는 추가 그룹화 변수와 같은 더 작은 데이터 세트입니다. 
    
    현재 sp_execute_external_script는 저장 프로시저에 대한 입력으로 단일 데이터 세트만 지원합니다. 그러나 스칼라 또는 이진 입력을 여러 개 추가할 수 있습니다.

    EXECUTE 뒤에 있는 저장 프로시저 호출은 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 대한 입력으로 사용할 수 없습니다. 쿼리, 뷰 또는 기타 유효한 SELECT 문을 사용할 수 있습니다.

+ 필요한 출력을 결정합니다. sp_execute_external_script를 사용하여 R 코드를 실행하는 경우 저장 프로시저는 하나의 데이터 프레임만 결과로 출력할 수 있습니다. 그러나 R 코드 또는 SQL 매개 변수에서 파생된 다른 스칼라 값뿐만 아니라 이진 형식의 플롯 및 모델을 포함한 여러 스칼라 출력을 출력할 수도 있습니다.

**데이터 형식**

+ 가능한 데이터 형식 문제의 검사 목록을 확인합니다.

    모든 R 데이터 형식은 SQL Server Machine Learning Services에서 지원됩니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 R보다 다양한 데이터 형식을 지원합니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 R로 보내거나 그 반대로 보낼 때 일부 암시적 데이터 형식 변환이 수행됩니다. 일부 데이터를 명시적으로 캐스팅하거나 변환해야 할 수 있습니다. 

    NULL 값이 지원됩니다. 그러나 R은 `na` 데이터 구문을 사용하여 null과 비슷한 누락된 값을 나타냅니다.

+ R에서 사용할 수 없는 데이터에 대한 종속성을 제거하는 것이 좋습니다. 예를 들어 SQL Server의 rowid 및 GUID 데이터 형식은 R에서 사용하고 오류를 생성할 수 없습니다.

    자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)을 참조하세요.

## <a name="step-2-convert-or-repackage-code"></a>2단계. 코드 변환 또는 다시 패키지

코드를 얼마나 변경할 것인지는 SQL Server 컴퓨팅 컨텍스트에서 실행할 원격 클라이언트에서 R 코드를 제출하려는지, 아니면 향상된 성능과 데이터 보안을 제공할 수 있는 저장 프로시저의 일부로 코드를 배포하려는지 여부에 따라 다릅니다. 저장 프로시저에서 코드를 래핑하는 경우 몇 가지 추가 요구 사항이 적용됩니다. 

+ 데이터 이동을 방지하기 위해 가능하면 항상 기본 입력 데이터를 SQL 쿼리로 정의합니다.

+ 저장 프로시저에서 R을 실행하는 경우 여러 **스칼라** 입력을 전달할 수 있습니다. 출력에서 사용하려는 매개 변수의 경우 **OUTPUT** 키워드를 추가합니다. 

    예를 들어 다음 스칼라 입력 `@model_name`은 결과의 자체 열에 있는 출력이기도 한 모델 이름을 포함합니다.

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 매개 변수로 전달하는 변수는 모두 R 코드의 변수에 매핑되어야 합니다. 기본적으로, 변수는 이름으로 매핑됩니다.

    입력 데이터 세트의 모든 열을 R 스크립트의 변수에 매핑해야 합니다.  예를 들어 R 스크립트에 다음과 같은 수식이 포함되어 있다고 가정합니다.

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    입력 데이터 세트에 이름이 ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour 및 DayOfWeek로 일치하는 열이 포함되지 않은 경우 오류가 발생합니다.

+ 경우에 따라 결과에 대한 출력 스키마를 미리 정의해야 합니다.

    예를 들어 테이블에 데이터를 삽입하려면 **WITH RESULT SET** 절을 사용하여 스키마를 지정해야 합니다.

    R 스크립트에서 `@parallel=1` 인수를 사용하는 경우에도 출력 스키마가 필요합니다. 이유는 SQL Server에서 여러 프로세스를 만들어 병렬로 쿼리를 실행하고 끝에 결과를 수집할 수 있기 때문입니다. 따라서 출력 스키마를 먼저 준비해야 병렬 프로세스를 만들 수 있습니다.
    
    다른 경우에는 **WITH RESULT SETS UNDEFINED** 옵션을 사용하여 결과 스키마를 생략할 수 있습니다. 이 문은 열 이름을 지정하거나 SQL 데이터 형식을 지정하지 않고 R 스크립트에서 데이터 세트를 반환합니다.

+ R이 아닌 T-SQL을 사용하여 타이밍 또는 추적 데이터를 생성하는 것이 좋습니다.

    예를 들어 R 스크립트에서 비슷한 데이터를 생성하는 대신 결과에 전달되는 T-SQL 호출을 추가하여 감사 및 스토리지에 사용되는 시스템 시간 또는 기타 정보를 전달할 수 있습니다. 

**성능 및 보안 향상**

+ 예측 또는 중간 결과를 파일에 기록하지 마세요. 대신, 테이블에 예측을 기록하여 데이터 이동을 방지합니다.

+ 모든 쿼리를 미리 실행하고 SQL Server 쿼리 계획을 검토하여 병렬로 수행할 수 있는 작업을 식별합니다.

    입력 쿼리를 병렬 처리할 수 있는 경우 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 대한 인수의 일부로 `@parallel=1`을 설정합니다. 

    이 플래그를 사용한 병렬 처리는 일반적으로 SQL Server에서 분할된 테이블로 작업하거나 여러 프로세스에 쿼리를 분산하고 끝에 결과를 집계할 때마다 수행할 수 있습니다. 일반적으로 모든 데이터를 읽어야 하는 알고리즘을 통해 모델을 학습하거나 집계를 만들어야 하는 경우에는 이 플래그를 사용한 병렬 처리를 수행할 수 없습니다.

+ R 코드를 검토하여 독립적으로 수행하거나 별도의 저장 프로시저 호출을 사용하여 보다 효율적으로 수행할 수 있는 단계가 있는지 확인합니다. 예를 들어 기능 엔지니어링 또는 기능 추출을 별도로 수행하고 값을 테이블에 저장하여 더 나은 성능을 얻을 수 있습니다.

+ 세트 기반 계산을 위해 R 코드 대신 T-SQL을 사용하는 방법을 알아보세요.

    예를 들어 이 R 솔루션은 사용자 정의 T-SQL 함수 및 R에서 동일한 기능 엔지니어링 작업을 수행할 수 있는 방법을 보여 줍니다. [데이터 과학 엔드투엔드 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ 가능한 경우 분산 실행을 지원하는 **ScaleR** 함수로 기본 R 함수를 대체합니다. 자세한 내용은 [Comparison of Base R and Scale R Functions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)(Base R 및 Scale R 함수 비교)를 참조하세요.

+ 데이터베이스 개발자에게 문의하여 [메모리 최적화 테이블](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)과 같은 SQL Server 기능을 사용하거나 Enterprise Edition이 있는 경우 [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor))를 사용하여 성능을 개선하는 방법을 확인하세요.

    자세한 내용은 [SQL Server Optimization Tips and Tricks for Analytics Services](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)(Analytics Services에 대한 SQL Server 최적화 팁과 요령)를 참조하세요.

### <a name="step-3-prepare-for-deployment"></a>3단계. 배포 준비

+ 코드를 배포하기 전에 패키지를 설치 및 테스트할 수 있도록 관리자에게 알립니다. 

    개발 환경에서는 코드의 일부로 패키지를 설치해도 되지만 프로덕션 환경에서는 바람직하지 않습니다. 

    저장 프로시저를 사용하거나 SQL Server 컴퓨팅 컨텍스트에서 R 코드를 실행하는지 여부에 관계없이 사용자 라이브러리는 지원되지 않습니다.

**저장 프로시저에서 R 코드 패키지**

+ 코드가 비교적 간단한 경우 다음 샘플에 설명된 대로 수정 없이 T-SQL 사용자 정의 함수에 코드를 포함할 수 있습니다.

    + [rxExec에서 실행되는 R 함수 만들기](../tutorials/deepdive-create-a-simple-simulation.md)
    + [T-SQL 및 R을 사용하는 기능 엔지니어링](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ 코드가 더 복잡한 경우 R 패키지 **sqlrutils**를 사용하여 코드를 변환합니다. 이 패키지는 숙련된 R 사용자가 적절한 저장 프로시저 코드를 작성하는 데 도움이 되도록 디자인되었습니다. 

    첫 번째 단계는 분명히 정의된 입력 및 출력을 사용하여 R 코드를 단일 함수로 다시 작성하는 것입니다.

    그런 다음, **sqlrutils** 패키지를 사용하여 입력 및 출력을 올바른 형식으로 생성합니다. **sqlrutils** 패키지는 전체 저장 프로시저 코드를 생성하며 데이터베이스에 저장 프로시저를 등록할 수도 있습니다. 

    자세한 내용 및 예제는 [sqlrutils(SQL)](ref-r-sqlrutils.md)를 참조하세요.

**다른 워크플로와 통합**

+ T-SQL 도구 및 ETL 프로세스를 활용합니다. 데이터 워크플로의 일부로 미리 기능 엔지니어링, 기능 추출 및 데이터 정리를 수행합니다.

    [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] 또는 RStudio와 같은 전용 R 개발 환경에서 작업하는 경우 일반적인 워크플로는 데이터를 컴퓨터로 끌어오고 반복적으로 데이터를 분석한 다음 결과를 출력하거나 표시하는 것입니다. 
    
    그러나 독립 실행형 R 코드를 SQL Server로 마이그레이션하면 이 프로세스 중 상당 부분을 간소화하거나 다른 SQL Server 도구에 위임할 수 있습니다. 

+ 안전한 비동기 시각화 전략을 사용합니다.

    SQL Server 사용자가 종종 서버의 파일에 액세스할 수 없으며, 일반적으로 SQL 클라이언트 도구는 R 그래픽 디바이스를 지원하지 않습니다. 플롯 또는 기타 그래픽을 솔루션의 일부로 생성하는 경우 플롯을 이진 데이터로 내보내고 테이블에 저장하거나 기록하는 것이 좋습니다.

+ 애플리케이션에서 직접 액세스하기 위해 예측 및 채점 함수를 저장 프로시저에 래핑합니다.

### <a name="other-resources"></a>기타 리소스

SQL Server에 R 솔루션을 배포하는 방법에 대한 예제를 보려면 다음 샘플을 참조하세요.

+ [Build a predictive model for  ski rental business using R and SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)(R 및 SQL Server를 사용하여 스키 임대 비즈니스에 대한 예측 모델 빌드)

+ [SQL 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md) 저장 프로시저에 래핑하여 R 코드를 더 모듈식으로 만들 수 있는 방법을 보여 줍니다.

+ [포괄적인 데이터 과학 솔루션](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) R 및 T-SQL의 기능 엔지니어링 비교를 포함합니다.
