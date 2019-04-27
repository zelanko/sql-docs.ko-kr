---
title: 저장된 프로시저-SQL Server Machine Learning Services에 대 한 R 코드 변환
description: 관계형 데이터에 SQL Server 솔루션 배포 및 데이터 액세스에 대 한 SQL Server 저장 프로시저에 R 코드를 마이그레이션하십시오.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: a3348058b03ff1441256cc8298ddc1b5b2216b0d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642794"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>SQL Server (In-database) 인스턴스의 실행을 위해 R 코드 변환
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server에서 작동 하는 R 코드를 수정 하는 방법에 높은 수준의 지침을 제공 합니다. 

SQL Server에 R Studio 또는 다른 환경에서 R 코드를 이동할 때 가장 자주 코드를 추가 수정 없이 이루어집니다: 예를 들어, 간단한 코드 인 경우와 같은 일부를 사용 하는 함수 입력 값을 반환 합니다. 사용 하는 포트 솔루션도 쉽습니다 합니다 **RevoScaleR** 또는 **MicrosoftML** 패키지 최소한 변경 하 여 다른 실행 컨텍스트에서 실행을 지원 합니다.

그러나 코드 중 하나가 다음 적용 하는 경우 상당한 변화가 필요할 수 있습니다.

+ 사용할 R 라이브러리는 네트워크에 액세스 하거나 SQL Server에 설치할 수 없습니다.
+ 코드에서는 Excel 워크시트, 공유에 파일 및 다른 데이터베이스와 같은 SQL Server, 외부 데이터 원본에 대 한 별도 호출 합니다. 
+ 코드를 실행 하려는 합니다 *@script* 의 매개 변수 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 또한 저장된 프로시저 매개 변수화 합니다.
+ 원래 솔루션에는 데이터 준비 기능 엔지니어링 및 모델 학습 또는 점수 매기기, 보고 등 독립적으로 실행 하는 경우 프로덕션 환경에서 더 효율적일 수 있습니다 하는 여러 단계가 포함 됩니다.
+ 개선 하려는 라이브러리를 변경, 병렬 실행을 사용 하 여 또는 SQL Server에 몇 가지 처리 작업 오프 로드 하 여 성능을 최적화 합니다. 

## <a name="step-1-plan-requirements-and-resources"></a>1단계. 계획 요구 사항 및 리소스

**패키지**

+ 패키지가 필요를 확인 하 고 SQL Server에서 작동 하는지 확인 합니다.
 
+ Machine Learning 서비스에서 사용 하는 기본 패키지 라이브러리에 패키지를 사전에 설치 합니다. 사용자 라이브러리 지원 되지 않습니다.

**데이터 원본** 

+ R 코드를 포함 하려는 경우 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), 기본 및 보조 데이터 원본 식별 합니다. 

    + **기본** 데이터 소스는 모델 학습 데이터 또는 예측에 대 한 입력된 데이터와 같은 큰 데이터 집합입니다. 가장 큰 데이터 집합의 입력 매개 변수에 매핑할 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

    + **보조** 데이터 소스는 요인에 따른 추가 그룹화 변수의 목록과 같은 일반적으로 작은 데이터 집합입니다. 
    
    현재, sp_execute_external_script 저장된 프로시저에 대 한 입력으로만 단일 데이터 집합을 지원합니다. 그러나 여러 스칼라 또는 이진 입력을 추가할 수 있습니다.

    EXECUTE 뒤 저장된 프로시저 호출에 대 한 입력으로 사용할 수 없습니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. 쿼리, 뷰 또는 다른 유효한 SELECT 문에 사용할 수 있습니다.

+ 필요한 출력을 확인 합니다. Sp_execute_external_script를 사용 하 여 R 코드를 실행 하는 경우 저장된 프로시저는 하나의 데이터 프레임을 결과적으로 출력할 수 있습니다. 단, 그림을 비롯 한 여러 스칼라 출력을 출력할 수 있습니다 하 고 매개 변수에서 R 코드 또는 SQL에서 파생 된 다른 스칼라 값 뿐만 아니라 이진 형식으로 모델.

**데이터 형식**

+ 가능한 데이터 형식 문제의 검사 목록을 확인합니다.

    SQL Server machine Learning 서비스에서 모든 R 데이터 형식이 지원 됩니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 더욱 다양 한 데이터 형식 R과는 지원 보낼 때 일부 암시적 데이터 형식 변환이 수행 됩니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 R로 이동 하 고 그 반대의 경우도 마찬가지입니다. 명시적으로 캐스팅 하거나 일부 데이터를 변환 해야 합니다. 

    NULL 값이 지원됩니다. 그러나 R 사용을 `na` null 비슷합니다 누락 값을 나타내는 데이터 구조입니다.

+ R: 예를 들어 rowid에서 사용할 수 없는 데이터에 대 한 종속성을 제거 하는 것이 좋습니다. 및 SQL Server에서 GUID 데이터 형식을 R에서 사용할 수 없습니다 오류를 생성 합니다.

    자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md) 을 참조합니다.

## <a name="step-2-convert-or-repackage-code"></a>2단계. 변환 또는 코드를 다시 작성

코드를 변경 하는 정도 SQL Server 계산 컨텍스트에서 실행 하기 위해 원격 클라이언트에서 R 코드를 제출 하려면 또는 더 나은 성능 및 데이터 보안을 제공할 수 있는 저장된 프로시저의 일환으로 코드를 배포 하려고 하는지 여부에 따라 달라 집니다. 저장된 프로시저에 코드를 래핑하는 몇 가지 추가 요구 사항을 적용 합니다. 

+ 데이터 이동을 방지 하려면 가능한 한 기본 입력된 데이터를 SQL 쿼리로 정의 합니다.

+ 저장된 프로시저에서 R을 실행 하는 경우에 여러 전달할 수 있습니다 **스칼라** 입력 합니다. 출력에 사용 하려는 모든 매개 변수를 추가 합니다 **출력** 키워드입니다. 

    예를 들어, 다음 스칼라 입력 `@model_name` 출력 결과에 해당 열에는 모델 이름을 포함 합니다.

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 에 저장된 프로시저의 매개 변수로 전달 하는 모든 변수 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) R 코드의 변수에 매핑해야 합니다. 기본적으로, 변수는 이름으로 매핑됩니다.

    또한 입력된 데이터 집합의 모든 열은 R 스크립트의 변수에 매핑해야 합니다.  예를 들어 R 스크립트에는 다음과 같은 수식이 포함 되어 있다고 가정 합니다.

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    입력된 데이터 집합에 ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour 및 DayOfWeek 일치 하는 이름 가진 열이 없는 경우 오류가 발생 합니다.

+ 일부 경우에는 출력 스키마를 결과 대 한 미리 정의 되어야 합니다.

    예를 들어 테이블에 데이터를 삽입할 사용 해야 합니다 **사용 하 여 결과 집합** 스키마를 지정 하는 절.

    R 스크립트 인수를 사용 하는 경우 출력 스키마가 필요한도 `@parallel=1`합니다. 이유는 SQL Server에서 여러 프로세스를 만들어 병렬로 쿼리를 실행하고 끝에 결과를 수집할 수 있기 때문입니다. 따라서 출력 스키마 병렬 프로세스를 만들기 전에 준비 되어야 합니다.
    
    다른 경우에는 옵션을 사용 하 여 결과 스키마를 생략할 수 있습니다 **WITH RESULT SETS UNDEFINED**합니다. 이 문은 열 이름 또는 SQL 데이터 형식 지정 없이 R 스크립트에서 데이터 집합을 반환 합니다.

+ R. 보다는 T-SQL을 사용 하 여 타이밍 또는 추적 데이터를 생성 하는 것이 좋습니다.

    예를 들어 시스템 시간 또는 R 스크립트에서 유사한 데이터를 생성 하는 것이 아니라 결과에 전달 되는 T-SQL 호출을 추가 하 여 감사 및 저장소에 대 한 기타 정보를 전달할 수 있습니다. 

**성능 및 보안 향상**

+ 예측 또는 파일에 대 한 중간 결과 작성 하지 마세요. 데이터 이동을 방지 하려면 테이블에 예측을 대신 작성 합니다.

+ 사전에 모든 쿼리를 실행 하 고 병렬로 수행할 수 있는 작업을 식별 하려면 SQL Server 쿼리 계획을 검토 합니다.

    입력된 쿼리를 병렬 처리할 수 설정 `@parallel=1` 에 대 한 인수의 일부로 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. 

    이 플래그를 사용한 병렬 처리는 일반적으로 SQL Server에서 분할된 테이블로 작업하거나 여러 프로세스에 쿼리를 분산하고 끝에 결과를 집계할 때마다 수행할 수 있습니다. 일반적으로 모든 데이터를 읽어야 하는 알고리즘을 통해 모델을 학습하거나 집계를 만들어야 하는 경우에는 이 플래그를 사용한 병렬 처리를 수행할 수 없습니다.

+ R 코드를 검토하여 독립적으로 수행하거나 별도의 저장 프로시저 호출을 사용하여 보다 효율적으로 수행할 수 있는 단계가 있는지 확인합니다. 예를 들어, 기능 엔지니어링 이나 기능 추출을 별도로 수행 하는 테이블에 값을 저장 하 여 성능을 향상 시킬 수 있습니다.

+ 집합 기반 계산을 위해 R 코드 대신 T-SQL을 사용 하는 방법에 대 한 확인 합니다.

    예를 들어이 R 솔루션 T-SQL 함수를 사용자 정의 하는 방법을 보여 줍니다. 및 R 동일한 기능 엔지니어링 작업을 수행할 수 있습니다.: [데이터 과학 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)합니다.

+ 가능한 경우 기본 R 함수를 대체 **ScaleR** 분산된 실행을 지 원하는 함수입니다. 자세한 내용은 [비교의 기본 R 및 R 기능 확장](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)합니다.

+ 와 같은 SQL Server 기능을 사용 하 여 성능을 향상 하는 방법을 결정 하는 데이터베이스 개발자와 상의 [메모리 최적화 테이블](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables), 또는 Enterprise edition [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    자세한 내용은 참조 하세요. [분석 서비스의 SQL Server 최적화 팁과 요령](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>3단계. 배포 준비

+ 코드를 배포하기 전에 패키지를 설치 및 테스트할 수 있도록 관리자에게 알립니다. 

    개발 환경에서 코드의 일환으로 패키지를 설치 해도 되지만이 프로덕션 환경에서는 바람직하지 합니다. 

    저장된 프로시저를 사용 하거나 SQL Server 계산 컨텍스트에서 R 코드를 실행 하는지 여부에 관계 없이, 사용자 라이브러리 지원 되지 않습니다.

**저장된 프로시저에서 R 코드를 패키지 합니다.**

+ 코드 비교적 단순한 경우 이러한 샘플에 설명 된 대로 수정 하지 않고 T-SQL 사용자 정의 함수에 포함할 수 있습니다.

    + [RxExec에서 실행 되는 R 함수 만들기](../tutorials/deepdive-create-a-simple-simulation.md)
    + [T-SQL 및 R을 사용한 기능 엔지니어링](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ R 패키지를 사용 하 여 코드를 더 복잡 한 경우 **sqlrutils** 코드를 변환 합니다. 이 패키지는 경험이 많은 R 사용자가 적절 한 저장된 프로시저 코드를 작성 하도록 설계 되었습니다. 

    첫 번째 단계 명확히 정의 된 입력 및 출력을 사용 하 여 단일 함수로 R 코드를 다시 작성 하는 것입니다.

    그런 다음 사용 합니다 **sqlrutils** 올바른 형식으로 입력 및 출력을 생성 하는 패키지 합니다. 합니다 **sqlrutils** 패키지 하면 전체 저장된 프로시저 코드를 생성 하 고 데이터베이스에서 저장된 프로시저를 등록할 수도 있습니다. 

    자세한 내용 및 예제를 참조 하세요 [sqlrutils (SQL)](ref-r-sqlrutils.md)합니다.

**다른 워크플로와 통합**

+ T-SQL 도구 및 ETL 프로세스를 활용 합니다. 기능 엔지니어링, 기능 추출 및 데이터 워크플로의 일부로 데이터 사전에 정리를 수행 합니다.

    작업할 때는 전용된 R 개발 환경에서와 같은 [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] 또는 RStudio 수 컴퓨터에 데이터를 끌어오는, 반복적으로 데이터를 분석 하 고 다음 작성 또는 결과 표시 합니다. 
    
    그러나 독립 실행형 R 코드 SQL 서버로 마이그레이션되면이 프로세스의 대부분 또는 수 있습니다 간체 다른 SQL Server 도구에 위임. 

+ 안전 하 고 비동기 시각화 전략을 사용 합니다.

    SQL Server의 사용자를 종종 파일 서버에서 액세스할 수 없습니다 및 SQL 클라이언트 도구 일반적으로 R 그래픽 장치를 지원 하지 않습니다. 솔루션의 일부로 그림 또는 다른 그래픽을 생성 하는 경우 이진 데이터로 플롯 내보내기 및 테이블에 저장 하거나 작성 것이 좋습니다.

+ 응용 프로그램에서 직접 액세스 하기 위해 저장된 프로시저에서 예측 및 점수 매기기 함수를 래핑하십시오.

### <a name="other-resources"></a>기타 리소스

SQL Server에서 R 솔루션을 배포할 수 있습니다 하는 방법의 예제를 보려면 다음이 샘플을 참조 합니다.

+ [R 및 SQL Server를 사용 하 여 ski 사업에 대 한 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [SQL 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md) 를 만드는 방법을 R 코드 모듈식 저장된 프로시저에 래핑하여 방법을 보여 줍니다.

+ [종단 간 데이터 과학 솔루션](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) R 및 T-SQL의 기능 엔지니어링 비교를 포함 합니다.
