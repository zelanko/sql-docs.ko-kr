---
title: "R Services에서 사용할 R 코드 변환 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed5f9052467492fe4bbbfb4ac0682c08a7ba8062
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="converting-r-code-for-use-in-r-services"></a>R Services에서 사용할 R 코드 변환

SQL server R Studio 또는 다른 환경에서 R 코드를 이동 하면 대개 코드가 작동에 추가 될 때 추가 수정 없이  *@script*  의 매개 변수 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. 사용 하 여 솔루션을 개발한 경우에 특히 그렇습니다는 **RevoScaleR** 비교적 간단 하 게 실행 컨텍스트를 변경 하는 함수입니다.

그러나 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와의 긴밀한 통합을 활용하고 비용이 많이 드는 데이터 전송을 방지하기 위해 SQL Server에서 실행되도록 R 코드를 수정하려고 합니다.

SQL Server에서 R 코드를 실행할 수 있는 방법의 예를 보려면 다음 연습을 참조하세요.

+ [SQL 개발자를 위한 In-database 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md) 를 만드는 방법을 R 코드가 더욱 모듈화 저장된 프로시저에 래핑하여 보여 줍니다.

+ [종단 간 데이터 과학 솔루션](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) T-SQL R의 기능 엔지니어링의 비교를 포함 합니다.

## <a name="how-the-data-science-process-changes-in-sql-server"></a>SQL Server에서 변경 내용을 데이터 과학 프로세스

작업할 때는 전용된 R 개발 환경에서와 같은 [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] 또는 RStudio, 일반적인 워크플로에서 컴퓨터에 데이터를 가져올, 분석 데이터를 반복적으로 및 다음 출력 또는 결과 표시 합니다. 그러나 패키지가 마이그레이션되면 독립 실행형 R 코드는 SQL Server로 대부분이 프로세스의 수 수 간소화 되거나 다른 SQL Server 도구에 위임 합니다. 또한 이렇게 하면 성능이 향상 대부분의 경우.

| 외부 코드 | SQL Server의 R |
|-------|-------|
| 데이터 수집| 입력된 데이터를 SQL 쿼리로 정의 합니다. 데이터 이동을 하지 마십시오. |
| 데이터 요약 및 시각화| 점도 이미지로 내보낼 하거나 원격 워크스테이션에 보낼 수 있습니다.|
|기능 엔지니어링| 쿼리 최적화를 확인 하지만 사용자 코드를 변경 하지 않으려는 경우 데이터베이스에서 R을 사용 합니다. 조사 여부 T-SQL 함수 또는 사용자 지정 Udf를 호출 하려면 더 효율적일 수 있습니다.|
|분석 프로세스의 일부인 데이터 정리| 기능 엔지니어링, 기능 추출 및 데이터 워크플로의 일부로 데이터 사전에 정리를 수행 합니다.|
|파일에 예측 출력| 데이터 이동을 방지 하도록 테이블에 예측을 출력 합니다. 응용 프로그램에서 직접 액세스 하기 위해 저장된 프로시저의 함수를 예측 하는 줄 바꿈 합니다.|

## <a name="best-practices"></a>최선의 구현 방법

+ 필수 패키지 등의 종속성을 미리 기록합니다. 개발 및 테스트 환경에서는 코드의 일부로 패키지를 설치해도 되지만 프로덕션 환경에서는 바람직하지 않습니다. 코드를 배포하기 전에 패키지를 설치 및 테스트할 수 있도록 관리자에게 알립니다.

+ 가능한 데이터 형식 문제의 검사 목록을 확인합니다. 코드의 각 섹션에 필요 합니다. 결과의 스키마를 문서화 합니다.

+ 모델 학습 데이터 또는 입력 데이터와 같은 예측의 기본 데이터 원본과 인수, 추가 그룹화 변수 등의 보조 원본을 식별합니다. 가장 큰 데이터 집합을 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 입력 매개 변수에 매핑합니다.

+ 데이터베이스에서 직접 작동하도록 입력 데이터 문을 변경합니다. 로컬 CSV 파일로 데이터를 이동 하거나 ODBC 호출을 반복 하지 않고 데이터를 이동 하지 않고 더 나은 성능을 SQL 쿼리 또는 데이터베이스에 대해 직접 실행할 수 있는 뷰를 사용 하 여 얻을 수 있습니다.

+ SQL Server 쿼리 계획을 사용하여 병렬로 수행할 수 있는 작업을 식별합니다. 입력된 쿼리를 병렬화 할 수 있습니다 설정 `@parallel=1` 인수를 프로그램의 일부로 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. 이 플래그를 사용한 병렬 처리는 일반적으로 SQL Server에서 분할된 테이블로 작업하거나 여러 프로세스에 쿼리를 분산하고 끝에 결과를 집계할 때마다 수행할 수 있습니다.

  일반적으로 모든 데이터를 읽어야 하는 알고리즘을 통해 모델을 학습하거나 집계를 만들어야 하는 경우에는 이 플래그를 사용한 병렬 처리를 수행할 수 없습니다.

+ 가능한 경우, 분산 실행을 지원하는 **ScaleR** 함수로 기본 R 함수를 대체합니다. 자세한 내용은 참조 [비교의 기본 R 및 R 함수 배율](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler-compared-to-base-r)합니다.

+ R 코드를 검토하여 독립적으로 수행하거나 별도의 저장 프로시저 호출을 사용하여 보다 효율적으로 수행할 수 있는 단계가 있는지 확인합니다. 예를 들어 기능 엔지니어링이나 기능 추출을 별도로 수행하고 새 열에 값을 추가할 수도 있습니다. 

  집합 기반 계산에 R 코드 보다는 T-SQL을 사용 합니다. 예를 보려면 기능 엔지니어링 작업에 대 한 Udf 및 R을 비교 하는 R 솔루션 참조 [데이터 과학 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)합니다.

+ R 패키지를 사용 하 여 **sqlrutils** 명확 하 게 정의 된 입 / 출력 매개 변수 저장된 프로시저에 쉽게 매핑할 수 있는 하나의 함수에 코드를 변환할 수 있습니다. 자세한 내용 및 예제에 대 한 참조 [SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)합니다.


## <a name="restrictions"></a>제한 사항

 R 코드를 변환할 때는 다음과 같은 제한 사항에 유의하세요.

### <a name="data-types"></a>데이터 형식

-   모든 R 데이터 형식이 지원됩니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 R보다 다양한 데이터 형식을 지원하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 R로 보내거나 그 반대로 보낼 때 일부 암시적 데이터 형식 변환이 수행됩니다. 명시적으로 캐스팅 하거나 일부 데이터를 변환 하려면 할 수도 있습니다.

- NULL 값이 지원됩니다. 사용 하 여 R의 `na` null 비슷한 누락 값을 나타내는 데이터 구조입니다.

자세한 내용은 참조 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)합니다.

### <a name="inputs-and-outputs"></a>입/출력

+ 저장 프로시저 매개 변수의 일부로 입력 데이터 집합 하나만 정의할 수 있습니다. 저장 프로시저에 대한 이 입력 쿼리는 유효한 단일 SELECT 문일 수 있습니다. 이 입력을 사용 하 여 가장 큰 데이터 집합에 대 한 RODBC에 대 한 호출을 사용 하 여 필요에 따라 더 작은 데이터 집합 가져오기 하는 것이 좋습니다.

+ 앞에 EXECUTE 저장된 프로시저 호출에 대 한 입력으로 사용할 수 없습니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

+ 입력 데이터 집합의 모든 열을 R 스크립트의 변수에 매핑해야 합니다. 변수는 이름으로 자동 매핑됩니다. 예를 들어 R 스크립트에는이 이와 같은 수식을 포함 합니다.
    
    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
     입력된 데이터 집합에 ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour, 및 DayOfWeek 일치 하는 이름 가진 열이 포함 되어 있지 않으면 오류가 발생 합니다.

+ 여러 스칼라 매개 변수를 입력으로 제공할 수도 있습니다. 그러나 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 매개 변수로 전달하는 변수는 모두 R 코드의 변수에 매핑되어야 합니다. 기본적으로, 변수는 이름으로 매핑됩니다.

+ R 코드의 출력에 스칼라 입력 변수를 포함하려면 변수를 정의할 때 **OUTPUT** 키워드를 추가합니다.

+ [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 R 코드는 단일 데이터 집합을 data.frame 개체로 출력하도록 제한됩니다. 그러나 이진 형식의 그림, varbinary 형식의 모델 등 여러 스칼라 출력을 출력할 수도 있습니다.

+ 일반적으로 WITH RESULT SETS UNDEFINED 옵션을 사용하여 출력 열의 이름을 지정할 필요 없이 R 스크립트에서 반환된 데이터 집합을 출력할 수 있습니다. 그러나 출력하려는 R 스크립트의 모든 변수를 SQL 출력 매개 변수에 매핑해야 합니다.

+ R 스크립트에서 `@parallel=1` 인수를 사용하는 경우 출력 스키마를 정의해야 합니다. 이유는 SQL Server에서 여러 프로세스를 만들어 병렬로 쿼리를 실행하고 끝에 결과를 수집할 수 있기 때문입니다. 따라서 병렬 프로세스를 만들기 전에 출력 스키마를 정의 합니다.

### <a name="dependencies"></a>종속성

 + R 코드에서 패키지를 설치하지 마세요. SQL Server에서 패키지를 사전에 설치 해야 합니다.
 
  컴퓨터 학습 서비스에서 사용 하는 기본 패키지 라이브러리에 패키지를 설치 해야 합니다. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리](../r/r-package-management-for-sql-server-r-services.md)

