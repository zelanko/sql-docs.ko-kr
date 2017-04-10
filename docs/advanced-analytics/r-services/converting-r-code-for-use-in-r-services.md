---
title: "R 서비스에서 사용 하기 위해 R 코드 변환 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# R 서비스에서 사용 하기 위해 R 코드 변환
SQL Server에 R Studio 또는 다른 환경에서 R 코드를 이동 하면 자주 코드는 작동에 추가 하는 경우 더 이상의 수정 없이 *@script* 의 매개 변수 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. 실행 컨텍스트를 변경 하는 비교적 간단 하므로 ScaleR 함수를 사용 하 여 솔루션 개발한 경우 특히 유용 합니다.    
    
그러나 일반적으로 수정 하려는 R 코드와의 긴밀 한 통합을 활용 하기 위해 모두 SQL Server에서 실행 되도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 비용이 많이 드는 데이터 전송을 방지 하기 위해.   
   
   
## 리소스  
  
SQL Server에서 R 코드를 실행할 수는 방법의 예를 보려면이 연습을 참조 하십시오.   
+ [SQL 개발자에 대 한 데이터베이스에서 분석](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)    
  활용 하는 방법을 R 코드를 모듈식 저장된 프로시저에 래핑하여 보여 줍니다.  
+ [종단 간 데이터 과학 솔루션](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)    
  R 및 T-SQL 기능 엔지니어링의 비교를 포함합니다.

## SQL Server의 데이터 과학 프로세스에 대 한 변경 내용  
  
작업 하는 경우 [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)], RStudio, 또는 다른 환경에서는 일반적인 워크플로 사용자 컴퓨터에 데이터를 가져올, 반복적으로 데이터를 분석 하 고 다음 출력 또는 결과 표시 합니다. 그러나 패키지가 마이그레이션되면 독립 실행형 R 코드는 SQL Server에이 프로세스 중 상당 부분은 단순화 하거나 수 다른 SQL Server 도구에 위임:

| 외부 코드 | SQL Server의 R |
|-------|-------|
| 데이터를 수집 합니다.| 데이터베이스 내에 SQL 쿼리 입력된 데이터를 정의 합니다. | 
| 요약 및 데이터 시각화| 변경 되지 않습니다. 도표 이미지로 내보낼 하거나 원격 워크스테이션에 보낼 수|
|기능 엔지니어링| R에서 데이터베이스를 사용할 수 있지만 효율적으로 T-SQL 함수 또는 사용자 지정 Udf를 호출할 수 있습니다.|
|데이터 분석 프로세스의 일부를 정리 합니다.| ETL 프로세스에 위임 및 사전에 수행할 수 데이터 정리|
|파일에 출력 예측| 테이블 또는 줄 바꿈 하는 예측을 출력 `predict` 응용 프로그램에서 직접 액세스 하기 위해 저장된 프로시저에서|
  

  
## 최선의 구현 방법  
  
+ 사전에 필요한 패키지와 같은 종속성 메모를 확인 합니다. 개발 및 테스트 환경에서를 코드의 일부로 패키지를 설치 해도 수도 있지만이 프로덕션 환경에서 잘못 된 방법. 패키지를 설치 하 고 코드를 배포 하기 전에 테스트할 수 있도록 관리자를 알립니다.  
+ 가능한 데이터의 문제를 형식 검사 목록을 확인 하십시오. 코드의 각 섹션에 예상 결과의 스키마를 문서화 합니다.  
+ 모델 학습 데이터 또는 요소, 추가 그룹 변수 및 그와 같은 보조 원본 및 예측에 대 한 입력된 데이터와 같은 기본 데이터 원본을 확인 합니다. 가장 큰 데이터 집합의 입력 매개 변수에 매핑할 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.  
+ 데이터베이스에서 직접 작업 하 여 입력된 데이터 문을 변경 합니다. 로컬 CSV 파일에 데이터를 이동 하거나 반복 ODBC 호출을 대신 얻게 더 나은 성능을 SQL 쿼리 또는 데이터베이스에 대해 직접 실행할 수 있는 뷰를 사용 하 여 데이터 이동이 방지 됩니다.  
+ 동시에 수행할 수 있는 작업을 사용 하 여 SQL Server의 쿼리 계획입니다. 입력된 쿼리를 병렬화 할 수 있는 경우 설정 `@parallel=1` 일부로 sp_execute_external_script에 대 한 인수입니다. 병렬 처리이 플래그를 사용은 일반적으로 가능한 언제 든 지는 SQL Server 수 분할 된 테이블 작업 또는 여러 프로세스 간에 쿼리를 배포 및 끝에 결과 집계 합니다. 
   병렬 처리이 플래그를 사용 불가능 일반적으로 모든 데이터를 읽을 수 하는 알고리즘을 사용 하 여 학습 모델 없거나 필요한 집계를 만드는 경우 합니다. 
+ 가능한 경우, 기본 R 함수를 대체 **ScaleR** 분산된 실행을 지 원하는 기능입니다. 자세한 내용은 참조 [비교의 함수 R 규모 및 CRAN R](Summary%20of%20rx%20Functions.md)합니다.
+ 경우에 독립적으로 수행 하거나 별도 저장된 프로시저 호출을 사용 하 여 보다 효율적으로 수행할 수 있는 단계를 확인 하는 R 코드를 검토 합니다. 예를 들어, 기능 엔지니어링 이나 기능 추출을 개별적으로 수행 하 고 새 열에 값을 추가 하는 수도 있습니다. 집합 기반 계산을 위한 R 코드 보다는 T-SQL을 사용 합니다. 기능 엔지니어링 작업에 대 한 Udf 및 R의 성능을 비교 하는 R 솔루션의 한 예에 대 한이 자습서를 참조 하십시오.: [데이터 과학 종단 간 연습](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)합니다.  
  
    
## 제한 사항    
 고려할 사항은 다음과 같은 제한 사항이 R 코드를 변환할 때 같습니다.    
   
**데이터 형식**    
-   R 데이터 형식은 모두 지원 됩니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 더욱 다양 한 데이터 형식 보다 R을 보낼 때 일부 암시적 데이터 형식 변환을 수행 하도록 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R로 그리고 반대로 데이터입니다. 또한 해야 명시적으로 캐스팅 또는 변환 일부 데이터입니다.    
    
- NULL 값이 지원 됩니다. 사용 하 여 R는 `na` null과 비슷한 누락 된 값을 나타내는 데이터 생성 합니다.    
    
- 자세한 내용은 참조 [R 데이터 형식 작업](../../advanced-analytics/r-services/working-with-r-data-types.md)합니다.    
 
 **입/출력**   
+ 저장된 프로시저 매개 변수 중 하나만 입력된 데이터 집합을 정의할 수 있습니다. 저장된 프로시저에 대 한 입력된이 쿼리는 유효한 단일 SELECT 문 수 있습니다. 이 입력을 사용 하 여 가장 큰 데이터 집합에 대 한 RODBC에 대 한 호출을 사용 하 여 필요한 경우 더 작은 데이터 집합 가져오기 하는 것이 좋습니다. 

+ 저장 프로시저 호출 앞에 EXECUTE sp_execute_external_script에 대 한 입력으로 사용할 수 없습니다.    
    
+ R 스크립트의 변수에 입력된 데이터 집합의 모든 열을 매핑해야 합니다. 변수 이름으로 자동으로 매핑됩니다. 예를 들어 R 스크립트는 다음과 같은 수식을 포함 합니다.    
    
    ```    
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek    
    ```    
    
     입력된 데이터 집합 열, CRSDepTime, DayOfWeek, CRSDepHour, 및 DayOfWeek 일치 하는 이름 가진 열을 포함 되지 않은 경우 오류가 발생 합니다.    

+ 또한 여러 스칼라 매개 변수를 입력으로 제공할 수 있습니다. 그러나 저장된 프로시저의 매개 변수로 전달 된 모든 변수가 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) R 코드의 변수에 매핑되어야 합니다. 기본적으로, 변수 이름으로 매핑됩니다.
+ R 코드의 출력에 스칼라 입력된 변수를 포함 하려면 방금 추가 된 **출력** 키워드를 변수를 정의 합니다.             
+  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R 코드를 data.frame 개체로 단일 데이터 집합을 출력 하는 중 제한 됩니다. 그러나 여러 스칼라 출력을 도표를 포함 하 여 이진 형식으로 하 고, varbinary 형식으로 모델링을 출력할 수도 있습니다.    
    
+ 일반적으로 RESULT SETS UNDEFINED 옵션을 사용 하 여 출력 열의 이름을 지정 하지 않고 R 스크립트에서 반환 된 데이터 집합을 출력할 수 있습니다. 그러나 SQL 출력 매개 변수를 출력 하는 R 스크립트의 변수에 매핑해야 합니다.
    
+ R 스크립트의 인수를 사용 하는 경우 `@parallel=1`, 출력 스키마를 정의 해야 합니다. 이유는 끝에 수집 된 결과 함께 병렬로 쿼리를 실행 하려면 SQL Server에서 여러 프로세스를 만들 수 있습니다. 따라서 병렬 프로세스를 만들기 전에 출력 스키마에 정의 되어야 합니다.

 **종속성**
 + R 코드에서 패키지를 설치 하지 않습니다. SQL Server에서 패키지를 사전에 설치 해야 합니다.  
  
  
  

