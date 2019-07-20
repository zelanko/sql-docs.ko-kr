---
title: 저장 프로시저에 대 한 R 코드 변환
description: 솔루션 배포를 위한 SQL Server 저장 프로시저와 SQL Server의 관계형 데이터에 대 한 데이터 액세스를 위한 R 코드를 마이그레이션합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5a3bd47d8a16a784115136935f669c420cb65e8f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345121"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>SQL Server (데이터베이스 내) 인스턴스에서 실행할 R 코드를 변환 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server에서 작동 하도록 R 코드를 수정 하는 방법에 대 한 고급 지침을 제공 합니다. 

R Studio 또는 다른 환경에서 SQL Server로 R 코드를 이동 하는 경우 코드는 추가 수정 없이 실행 됩니다. 예를 들어, 일부 입력을 사용 하 고 값을 반환 하는 함수와 같이 코드가 간단한 경우입니다. **RevoScaleR** 또는 **MicrosoftML** 패키지를 사용 하는 솔루션은 최소한의 변경으로 다른 실행 컨텍스트에서 실행을 지 원하는 것이 더 쉽습니다.

그러나 다음 중 하나가 적용 되는 경우 코드에서 상당한 변경이 필요할 수 있습니다.

+ 네트워크에 액세스 하거나 SQL Server에 설치할 수 없는 R 라이브러리를 사용 합니다.
+ 이 코드는 Excel 워크시트, 공유 파일 및 기타 데이터베이스와 같은 SQL Server 외부에 있는 데이터 원본에 대 한 별도의 호출을 수행 합니다. 
+ *@script* [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 의 매개 변수에서 코드를 실행 하 고 저장 프로시저를 매개 변수화 하려고 합니다.
+ 원본 솔루션에는 데이터 준비, 기능 엔지니어링 및 모델 학습, 점수 매기기 또는 보고와 같이 독립적으로 실행 되는 경우 프로덕션 환경에서 보다 효율적일 수 있는 여러 단계가 포함 됩니다.
+ 라이브러리를 변경 하거나 병렬 실행을 사용 하 여 성능을 최적화 하 고 SQL Server에 대 한 일부 처리를 오프 로드 합니다. 

## <a name="step-1-plan-requirements-and-resources"></a>1단계. 요구 사항 및 리소스 계획

**패키지**

+ 필요한 패키지를 확인 하 고 SQL Server에서 작동 하는지 확인 합니다.
 
+ Machine Learning Services에서 사용 하는 기본 패키지 라이브러리에 패키지를 미리 설치 합니다. 사용자 라이브러리는 지원 되지 않습니다.

**데이터 원본** 

+ R 코드를 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 포함 하려는 경우 기본 및 보조 데이터 원본을 식별 합니다. 

    + **주** 데이터 원본은 모델 학습 데이터와 같은 큰 데이터 집합 또는 예측을 위한 입력 데이터입니다. 가장 큰 데이터 집합을 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 입력 매개 변수에 매핑하도록 계획 합니다.

    + **보조** 데이터 원본은 일반적으로 요소 목록 또는 추가 그룹화 변수와 같은 작은 데이터 집합입니다. 
    
    현재 sp_execute_external_script는 저장 프로시저에 대 한 입력으로 단일 데이터 집합만 지원 합니다. 그러나 스칼라 또는 이진 입력을 여러 개 추가할 수 있습니다.

    EXECUTE 뒤에 오는 저장 프로시저 호출은 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 대 한 입력으로 사용할 수 없습니다. 쿼리, 뷰 또는 다른 유효한 SELECT 문을 사용할 수 있습니다.

+ 필요한 출력을 결정 합니다. Sp_execute_external_script를 사용 하 여 R 코드를 실행 하는 경우 저장 프로시저는 하나의 데이터 프레임만 결과로 출력할 수 있습니다. 하지만 R 코드 또는 SQL 매개 변수에서 파생 된 다른 스칼라 값 뿐만 아니라 이진 형식의 플롯 및 모델을 비롯 한 여러 스칼라 출력을 출력할 수도 있습니다.

**데이터 형식**

+ 가능한 데이터 형식 문제의 검사 목록을 확인합니다.

    모든 R 데이터 형식은 SQL Server machine Learning Services에서 지원 됩니다. 그러나는 R 보다 더 다양 한 데이터 형식을 지원합니다.[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 따라서 데이터를 R로 보낼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 때 일부 암시적 데이터 형식 변환이 수행 되며 그 반대의 경우도 마찬가지입니다. 일부 데이터를 명시적으로 캐스팅 하거나 변환 해야 할 수도 있습니다. 

    NULL 값이 지원됩니다. 그러나 R은 `na` 데이터 구문을 사용 하 여 누락 값을 나타냅니다 .이 값은 null과 비슷합니다.

+ R에서 사용할 수 없는 데이터에 대 한 종속성을 제거 하는 것이 좋습니다. 예를 들어 SQL Server의 rowid 및 GUID 데이터 형식을 R에서 사용 하 고 오류를 생성할 수 없습니다.

    자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md) 을 참조합니다.

## <a name="step-2-convert-or-repackage-code"></a>2단계. 코드 변환 또는 다시 패키징

코드를 변경 하는 양은 원격 클라이언트에서 R 코드를 전송 하 여 SQL Server 계산 컨텍스트에서 실행할지 아니면 저장 프로시저의 일부로 코드를 배포할지에 따라 달라 지 며 성능 및 데이터 보안을 향상 시킬 수 있습니다. 저장 프로시저에서 코드를 래핑하는 경우 몇 가지 추가 요구 사항이 적용 됩니다. 

+ 데이터 이동을 방지 하기 위해 가능한 한 SQL 쿼리로 기본 입력 데이터를 정의 합니다.

+ 저장 프로시저에서 R을 실행 하는 경우 여러 **스칼라** 입력을 통과할 수 있습니다. 출력에서 사용 하려는 매개 변수의 경우 **output** 키워드를 추가 합니다. 

    예를 들어 다음 스칼라 입력 `@model_name` 은 결과의 자체 열에도 출력 되는 모델 이름을 포함 합니다.

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 의 매개 변수로 전달 하는 모든 변수는 R 코드의 변수에 매핑되어야 합니다. 기본적으로, 변수는 이름으로 매핑됩니다.

    또한 입력 데이터 집합의 모든 열은 R 스크립트의 변수에 매핑되어야 합니다.  예를 들어 R 스크립트에 다음과 같은 수식이 포함 되어 있다고 가정 합니다.

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    입력 데이터 집합에 일치 하는 이름이 ArrDelay, CRSDepTime, DayOfWeek, Crsdepha 및 DayOfWeek 인 열이 포함 되어 있지 않으면 오류가 발생 합니다.

+ 출력 스키마를 결과에 대해 미리 정의 해야 하는 경우도 있습니다.

    예를 들어 테이블에 데이터를 삽입 하려면 **WITH RESULT SET** 절을 사용 하 여 스키마를 지정 해야 합니다.

    R 스크립트에서 인수 `@parallel=1`를 사용 하는 경우에도 출력 스키마가 필요 합니다. 이유는 SQL Server에서 여러 프로세스를 만들어 병렬로 쿼리를 실행하고 끝에 결과를 수집할 수 있기 때문입니다. 따라서 병렬 프로세스를 만들려면 먼저 출력 스키마를 준비 해야 합니다.
    
    다른 경우에는 **결과 집합이 UNDEFINED로 설정**된 옵션을 사용 하 여 결과 스키마를 생략할 수 있습니다. 이 문은 열의 이름을 지정 하거나 SQL 데이터 형식을 지정 하지 않고 R 스크립트에서 데이터 집합을 반환 합니다.

+ R이 아닌 T-sql을 사용 하 여 타이밍 또는 추적 데이터를 생성 하는 것이 좋습니다.

    예를 들어 R 스크립트에서 비슷한 데이터를 생성 하는 대신 결과에 전달 되는 T-sql 호출을 추가 하 여 감사 및 저장소에 사용 되는 시스템 시간 또는 기타 정보를 전달할 수 있습니다. 

**성능 및 보안 향상**

+ 예측 또는 중간 결과를 파일에 기록 하지 않습니다. 대신 테이블에 예측을 작성 하 여 데이터 이동을 방지 합니다.

+ 모든 쿼리를 미리 실행 하 고 SQL Server 쿼리 계획을 검토 하 여 병렬로 수행할 수 있는 태스크를 식별 합니다.

    입력 쿼리를 병렬화 할 수 있는 경우 `@parallel=1` [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 대 한 인수의 일부로를 설정 합니다. 

    이 플래그를 사용한 병렬 처리는 일반적으로 SQL Server에서 분할된 테이블로 작업하거나 여러 프로세스에 쿼리를 분산하고 끝에 결과를 집계할 때마다 수행할 수 있습니다. 일반적으로 모든 데이터를 읽어야 하는 알고리즘을 통해 모델을 학습하거나 집계를 만들어야 하는 경우에는 이 플래그를 사용한 병렬 처리를 수행할 수 없습니다.

+ R 코드를 검토하여 독립적으로 수행하거나 별도의 저장 프로시저 호출을 사용하여 보다 효율적으로 수행할 수 있는 단계가 있는지 확인합니다. 예를 들어 기능 엔지니어링 또는 기능 추출을 별도로 수행 하 고 값을 테이블에 저장 하 여 더 나은 성능을 얻을 수 있습니다.

+ 집합 기반 계산을 위해 R 코드 대신 T-sql을 사용 하는 방법을 찾습니다.

    예를 들어이 R 솔루션은 사용자 정의 T-sql 함수 및 R에서 동일한 기능 엔지니어링 작업을 수행할 수 있는 방법을 보여 줍니다. [데이터 과학 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

+ 가능 하면 기존 R 함수를 분산 실행을 지 원하는 **ScaleR** 함수로 바꿉니다. 자세한 내용은 [기본 r의 비교 및 r 함수 크기 조정](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)을 참조 하세요.

+ [메모리 최적화 테이블과](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)같은 SQL Server 기능을 사용 하 여 성능을 향상 시키는 방법 또는 Enterprise Edition이 있는 경우 [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor))를 사용 하 여 성능을 향상 시키는 방법을 확인 하려면 데이터베이스 개발자에 게 문의 하세요.

    자세한 내용은 [SQL Server 최적화 팁과 분석 서비스에 대 한 트릭](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services) 을 참조 하세요.

### <a name="step-3-prepare-for-deployment"></a>3단계. 배포 준비

+ 코드를 배포하기 전에 패키지를 설치 및 테스트할 수 있도록 관리자에게 알립니다. 

    개발 환경에서는 코드의 일부로 패키지를 설치 하는 것이 어려울 수 있지만 프로덕션 환경에서는이 방법이 좋지 않습니다. 

    저장 프로시저를 사용 하 든, SQL Server 계산 컨텍스트에서 R 코드를 실행 하는지에 관계 없이 사용자 라이브러리는 지원 되지 않습니다.

**저장 프로시저에서 R 코드 패키지**

+ 코드를 비교적 간단 하 게 수행 하는 경우 다음 예제에 설명 된 대로 수정 하지 않고 T-sql 사용자 정의 함수에 포함 시킬 수 있습니다.

    + [RxExec에서 실행 되는 R 함수 만들기](../tutorials/deepdive-create-a-simple-simulation.md)
    + [T-sql 및 R을 사용 하 여 기능 엔지니어링](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ 코드가 더 복잡 한 경우 R 패키지 **sqlrutils** 을 사용 하 여 코드를 변환 합니다. 이 패키지는 숙련 된 R 사용자가 적합 한 저장 프로시저 코드를 작성 하는 데 도움이 되도록 설계 되었습니다. 

    첫 번째 단계는 명확 하 게 정의 된 입력 및 출력을 사용 하 여 R 코드를 단일 함수로 다시 작성 하는 것입니다.

    그런 다음 **sqlrutils** 패키지를 사용 하 여 입력 및 출력을 올바른 형식으로 생성 합니다. **Sqlrutils** 패키지는 전체 저장 프로시저 코드를 생성 하 고 데이터베이스에 저장 프로시저를 등록할 수도 있습니다. 

    자세한 내용 및 예제는 [sqlrutils (SQL)](ref-r-sqlrutils.md)를 참조 하세요.

**다른 워크플로와 통합**

+ T-sql 도구 및 ETL 프로세스를 활용 합니다. 데이터 워크플로의 일부로 기능 엔지니어링, 기능 추출 및 데이터 정리를 미리 수행 합니다.

    또는 rstudio와 [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] 같은 전용 R 개발 환경에서 작업 하는 경우 데이터를 컴퓨터로 끌어오고 데이터를 반복적으로 분석 한 다음 결과를 작성 하거나 표시할 수 있습니다. 
    
    그러나 독립 실행형 R 코드가 SQL Server로 마이그레이션되면이 프로세스의 대부분을 간소화 하거나 다른 SQL Server 도구로 위임할 수 있습니다. 

+ 안전한 비동기 시각화 전략을 사용 합니다.

    SQL Server 사용자가 서버의 파일에 액세스할 수 없는 경우가 많으며, 일반적으로 SQL 클라이언트 도구는 R 그래픽 장치를 지원 하지 않습니다. 그리기 또는 다른 그래픽을 솔루션의 일부로 생성 하는 경우 플롯을 이진 데이터로 내보내고 테이블에 저장 하거나 작성 하는 것이 좋습니다.

+ 응용 프로그램에서 직접 액세스 하기 위해 저장 프로시저에서 예측 및 점수 매기기 함수를 래핑합니다.

### <a name="other-resources"></a>다른 리소스

SQL Server에서 R 솔루션을 배포 하는 방법에 대 한 예제를 보려면 다음 샘플을 참조 하세요.

+ [R 및 SQL Server를 사용 하 여 ski 임대 비즈니스에 대 한 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [SQL 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md) R 코드를 저장 프로시저에 래핑하여 모듈식으로 만드는 방법을 보여 줍니다.

+ [종단 간 데이터 과학 솔루션](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) R 및 T-sql의 기능 엔지니어링 비교를 포함 합니다.
