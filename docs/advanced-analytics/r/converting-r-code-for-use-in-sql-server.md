---
title: "R Services에서 사용할 R 코드 변환 | Microsoft 문서"
ms.date: 12/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 595bdb9cb16b02258d50d1f3d038ad988bbc4dd3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="converting-r-code-for-execution-in-database"></a>데이터베이스에서 실행에 대 한 R 코드 변환

이 문서는 SQL Server에서 작동 하는 R 코드를 수정 하는 방법에 대 한 자세한 지침을 제공 합니다. 

SQL server R Studio 또는 다른 환경에서 R 코드를 이동 하면 가장 자주 코드가 작동 하는 추가 수정 없이: 예를 들어 코드는 간단 하는 경우와 같은 일부를 사용 하는 함수 입력 값과 값을 반환 합니다. 사용 하는 포트 솔루션을 쉽게는 **RevoScaleR** 또는 **MicrosoftML** 변경 최소화 하면서 다른 실행 컨텍스트에 실행을 지원 하 여 패키지를 합니다.

그러나 코드 경우 다음 중 하나에 변경이 필요할 수 있습니다.

+ R 라이브러리는 네트워크에 액세스 하거나 SQL Server에 설치할 수 없습니다 사용.
+ 코드에서는 Excel 워크시트, 공유에 파일 및 다른 데이터베이스와 같은 SQL Server, 외부 데이터 원본에 대 한 별도 호출 합니다. 
+ 코드를 실행 하려는  *@script*  의 매개 변수 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 및 저장된 프로시저를 매개 변수화 할 수도 있습니다.
+ 원래 솔루션의 여러 단계 데이터 준비 작업이 나 모델을 학습, 점수 매기기, 또는 보고 및 기능 엔지니어링 같은 독립적으로 실행 하는 경우 프로덕션 환경에서 더 효율적일 수 있습니다를 포함 합니다.
+ 개선 하려면 라이브러리 변경, 병렬 실행을 사용 하 여 또는 SQL Server에 일부 처리 작업 오프 로드 하 여 성능을 최적화 합니다. 

## <a name="step-1-plan-requirements-and-resources"></a>1단계. 계획 요구 사항 및 리소스

**패키지**

+ 패키지는 필요한 확인 하 고 SQL Server에서 작동 하는지 확인 합니다.
 
+ 사전에 컴퓨터 학습 서비스에서 사용 하는 기본 패키지 라이브러리에서 패키지를 설치 합니다. 사용자 라이브러리 지원 되지 않습니다.

**데이터 원본** 

+ R 코드를 포함 하려는 경우 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), 기본 및 보조 데이터 원본을 확인 합니다. 

    + **기본** 데이터 소스는 모델 학습 데이터 또는 예측에 대 한 입력된 데이터와 같은 큰 데이터 집합입니다. 가장 큰 데이터 집합의 입력된 매개 변수에 매핑할 계획 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

    + **보조** 데이터 소스는 요소나 그룹화 변수 목록과 같이 일반적으로 더 작은 데이터 집합입니다. 
    
    현재 sp_execute_external_script 저장된 프로시저에 대 한 입력으로만 단일 데이터 집합을 지원합니다. 그러나 스칼라 또는 이진에 대 한 여러 입력을 추가할 수 있습니다.

    앞에 EXECUTE 저장된 프로시저 호출에 대 한 입력으로 사용할 수 없습니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. 쿼리, 뷰 또는 다른 유효한 SELECT 문에 사용할 수 있습니다.

+ 필요한 출력을 확인 합니다. Sp_execute_external_script를 사용 하 여 R 코드를 실행 하는 경우 저장된 프로시저 결과적으로 하나의 데이터 프레임에만 출력할 수 있습니다. 그러나도 표와 예측치를 비롯 한 여러 스칼라 출력을 출력 하 고 매개 변수 R 코드 또는 SQL에서 파생 된 다른 스칼라 값 뿐 아니라 이진 형식에서 모델.

**데이터 형식**

+ 가능한 데이터 형식 문제의 검사 목록을 확인합니다.

    모든 R 데이터 형식은 SQL Server 컴퓨터 학습 서비스에서 사용할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 더욱 다양 한 데이터 형식 r을 지원 합니다. 보낼 때 일부 암시적 데이터 형식 변환이 수행 됩니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 R로 그리고 반대로 합니다. 명시적으로 캐스팅 하거나 일부 데이터를 변환 해야 합니다. 

    NULL 값이 지원됩니다. 그러나 R에서 사용 된 `na` null 비슷한 누락 값을 나타내는 데이터 구조입니다.

+ 예를 들어 rowid r:에서 사용할 수 없는 데이터에 대 한 종속성을 제거 하는 것이 좋습니다. 및 SQL Server의 GUID 데이터 형식을 R에서 사용할 수 없습니다 및 오류를 생성 합니다.

    자세한 내용은 참조 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)합니다.

## <a name="step-2-convert-or-repackage-code"></a>2단계. 으로 변환 하거나 코드를 다시 패키지

얼마나 코드를 변경 하면 SQL Server 계산 컨텍스트에서 실행 되도록 원격 클라이언트에서 R 코드를 제출 하려면 또는 향상 된 성능 및 데이터 보안을 제공할 수 있는 저장된 프로시저의 일환으로 코드를 배포 하려는에 따라 달라 집니다. 저장된 프로시저에서 코드를 래핑하여 몇 가지 추가 요구 사항을 적용 합니다. 

+ 데이터 이동을 방지 하도록 가능 기본 입력된 데이터를 SQL 쿼리로 정의 합니다.

+ 여러 통과할 수, 저장된 프로시저에서 R을 실행할 때는 **스칼라** 입력 합니다. 출력에 사용 하려는 모든 매개 변수를 추가 하는 **출력** 키워드입니다. 

    예를 들어 다음과 같은 스칼라 입력 `@model_name` 출력 결과에 개별 열에 있는 모델 이름을 포함 합니다.

    ```SQL
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 저장된 프로시저의 매개 변수로 전달 하는 모든 변수 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) R 코드의 변수에 매핑되어야 합니다. 기본적으로, 변수는 이름으로 매핑됩니다.

    입력된 데이터 집합의 모든 열에는 R 스크립트의 변수도 매핑해야 합니다.  예를 들어 R 스크립트에는이 이와 같은 수식을 포함 합니다.

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    입력된 데이터 집합에 ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour, 및 DayOfWeek 일치 하는 이름 가진 열이 포함 되어 있지 않으면 오류가 발생 합니다.

+ 일부 경우에는 출력 스키마를 결과 대 한 사전에 정의 되어야 합니다.

    예를 들어 테이블에 데이터를 삽입 하려면 사용 해야는 **결과 집합으로** 스키마를 지정 하는 절.

    R 스크립트는 인수를 사용 하는 경우에 출력 스키마가 필요도 `@parallel=1`합니다. 이유는 SQL Server에서 여러 프로세스를 만들어 병렬로 쿼리를 실행하고 끝에 결과를 수집할 수 있기 때문입니다. 따라서 출력 스키마를 준비 해야 병렬 프로세스를 만들 수 있습니다.
    
    다른 경우에는 옵션을 사용 하 여 결과 스키마를 생략할 수 **와 RESULT SETS UNDEFINED**합니다. 이 문은 열 이름을 지정 하거나 SQL 데이터 형식 지정 하지 않고 R 스크립트에서 데이터 집합을 반환 합니다.

+ 오른쪽 것이 아니라 T-SQL을 사용 하 여 타이밍 또는 추적 데이터를 생성 하는 것이 좋습니다.

    예를 들어 시스템 시간 또는 R 스크립트에 유사한 데이터를 생성 하는 것이 아니라 결과 통해 전달 되는 T-SQL 호출을 추가 하 여 감사 및 저장을 위해 사용 되는 기타 정보를 전달할 수 있습니다. 

**성능 및 보안 향상**

+ 예측 또는 중간 결과 파일에 작성 하지 마십시오. 쓰려는 예측 테이블 대신, 데이터 이동을 방지 하도록 합니다.

+ 사전에 모든 쿼리를 실행 하 고 동시에 수행할 수 있는 작업을 SQL Server 쿼리 계획을 검토 합니다.

    입력된 쿼리를 병렬화 할 수 있습니다 설정 `@parallel=1` 인수를 프로그램의 일부로 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. 

    이 플래그를 사용한 병렬 처리는 일반적으로 SQL Server에서 분할된 테이블로 작업하거나 여러 프로세스에 쿼리를 분산하고 끝에 결과를 집계할 때마다 수행할 수 있습니다. 일반적으로 모든 데이터를 읽어야 하는 알고리즘을 통해 모델을 학습하거나 집계를 만들어야 하는 경우에는 이 플래그를 사용한 병렬 처리를 수행할 수 없습니다.

+ R 코드를 검토하여 독립적으로 수행하거나 별도의 저장 프로시저 호출을 사용하여 보다 효율적으로 수행할 수 있는 단계가 있는지 확인합니다. 예를 들어 테이블에 저장 하는 값을 별도로 기능 엔지니어링 이나 기능 추출을 수행 하 여 성능을 향상 시킬 수 있습니다.

+ 집합 기반 계산에 R 코드 보다는 T-SQL을 사용 하는 방법을 찾습니다.

    예를 들어이 R 솔루션을 사용자 지정 T-SQL 함수를 보여 줍니다. 및 R 동일한 기능 엔지니어링 작업을 수행할 수: [데이터 과학 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)합니다.

+ 가능 하면 사용 하는 기본 R 함수를 대체 **ScaleR** 분산된 실행을 지 원하는 함수입니다. 자세한 내용은 참조 [비교의 기본 R 및 R 함수 배율](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)합니다.

+ 와 같은 SQL Server 기능을 사용 하 여 성능을 향상 하는 방법을 결정 하는 데이터베이스 개발자와 상의 [메모리 액세스에 최적화 된 테이블](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables), 또는 Enterprise Edition의 경우 [리소스 관리자](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    자세한 내용은 참조 [SQL Server 최적화 팁과 요령 분석 서비스에 대 한](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>3단계. 배포 준비

+ 코드를 배포하기 전에 패키지를 설치 및 테스트할 수 있도록 관리자에게 알립니다. 

    개발 환경에서 사용자 코드의 일부로 패키지 설치를 않을 수 있지만이 프로덕션 환경에서 잘못 된 방법입니다. 

    저장된 프로시저를 사용 하 여 또는 SQL Server 계산 컨텍스트에서 R 코드 실행 여부에 관계 없이, 사용자 라이브러리 지원 되지 않습니다.

**저장된 프로시저에서 R 코드**

+ 코드 비교적 단순한 경우 이러한 예제에 설명 된 대로 수정 하지 않고 T-SQL 사용자 정의 함수에 포함할 수 있습니다.

    + [RxExec에서 실행 되는 R 함수 만들기](..\tutorials\deepdive-create-a-simple-simulation.md)
    + [T-SQL과 R을 사용 하 여 기능 엔지니어링](..\tutorials\sqldev-create-data-features-using-t-sql.md)

+ 보다 복잡 한 코드의 경우 R 패키지를 사용 하 여 **sqlrutils** 코드를 변환할 수 있습니다. 이 패키지는 숙련 된 R 사용자가 좋은 저장된 프로시저 코드를 작성할 수 있도록 설계 되었습니다. 

    R 코드를 명확 하 게 정의 된 입력 및 출력으로 단일 함수로 다시 작성 하는 첫 번째 단계가입니다.

    그런 다음 사용 하는 **sqlrutils** 올바른 형식으로 입력 및 출력을 생성 하는 패키지입니다. **sqlrutils** 패키지 완전 한 저장된 프로시저 코드가 자동으로 생성 및 저장된 프로시저는 데이터베이스에 등록할 수도 있습니다. 

    자세한 내용 및 예제에 대 한 참조 [SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)합니다.

**다른 워크플로와 통합**

+ T-SQL 도구 및 ETL 프로세스를 활용 합니다. 기능 엔지니어링, 기능 추출 및 데이터 워크플로의 일부로 데이터 사전에 정리를 수행 합니다.

    작업할 때는 전용된 R 개발 환경에서와 같은 [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] 또는 RStudio, 있습니다 수를 컴퓨터에 데이터를 가져올, 분석 데이터를 반복적으로 및 다음 작성 또는 결과 표시 합니다. 
    
    그러나 패키지가 마이그레이션되면 독립 실행형 R 코드는 SQL Server로 대부분이 프로세스의 수 수 간소화 되거나 다른 SQL Server 도구에 위임 합니다. 

+ 안전 하 고 비동기 시각화 전략을 사용 합니다.

    SQL Server의 사용자를 종종는 서버에서 파일에 액세스할 수 없습니다 및 SQL 클라이언트 도구는 R 그래픽 장치를 일반적으로 지원 하지 않습니다. 솔루션의 일부로 점도 또는 다른 그래픽을 생성 하는 경우는 점도 이진 데이터로 내보내는 및를 테이블에 저장 또는 쓰는 것이 좋습니다.

+ 예측 및 점수 매기기 함수에 직접 액세스 저장된 프로시저에서 응용 프로그램에서 줄 바꿈 합니다.

### <a name="other-resources"></a>기타 리소스

SQL Server에서 R 솔루션을 배포 하는 방법의 예를 보려면 다음이 샘플을 참조 합니다.

+ [R 및 SQL Server를 사용 하 여 ski 임대 비즈니스에 대 한 예상 모델을 작성](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [SQL 개발자를 위한 In-database 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md) 를 만드는 방법을 R 코드가 더욱 모듈화 저장된 프로시저에 래핑하여 보여 줍니다.

+ [종단 간 데이터 과학 솔루션](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) T-SQL R의 기능 엔지니어링의 비교를 포함 합니다.
