---
title: "SQL 개발자를 위한 데이터베이스 내 고급 분석(자습서) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: c18cb249-2146-41b7-8821-3a20c5d7a690
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# SQL 개발자를 위한 데이터베이스 내 고급 분석(자습서)
이 연습의 목적은 SQL 프로그래머에게 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하여 고급 분석 솔루션을 빌드하는 실습 경험을 제공하는 것입니다. 이 연습에서는 저장 프로시저에 R 코드를 래핑하여 응용 프로그램 또는 BI 솔루션에 R을 통합하는 방법을 알아봅니다.  
  
## 개요  
일반적으로 종단 간 솔루션을 빌드하는 프로세스는 데이터 가져오기 및 정리, 데이터 탐색 및 기능 엔지니어링, 모델 학습 및 튜닝, 마지막으로 프로덕션에 모델 배포로 구성됩니다. 실제 R 코드 개발 및 테스트는 RStudio 또는 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)] 등의 R용으로 빌드된 개발 환경을 사용하여 수행하는 것이 가장 좋습니다. 그러나 솔루션을 만든 후 익숙한 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 쉽게 배포할 수 있습니다.  
  
따라서 이 연습에서는 솔루션에 필요한 모든 R 코드가 제공되었다고 가정하고 이미 R로 코딩된 고급 분석 솔루션 빌드 및 배포에 집중합니다.  
  
-   [1단계: 샘플 데이터 다운로드](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md).    샘플 데이터 집합 및 샘플 SQL 스크립트 파일을 로컬 컴퓨터로 다운로드합니다.  
  
-   [2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md).  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스에서 데이터베이스와 테이블을 만들고 샘플 데이터를 테이블에 로드하는 PowerShell 스크립트를 실행합니다.  
  
-   [3단계: 데이터 탐색 및 시각화](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md).   [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에서 R 패키지 및 함수를 호출하여 기본 데이터 탐색 및 시각화를 수행합니다.  
  
-   [4단계: T-SQL을 사용하여 데이터 기능 만들기](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md).  사용자 지정 SQL 함수를 사용하여 새 데이터 기능을 만듭니다.  
  
-   [5단계: T-SQL을 사용하여 모델 학습 및 저장](../../advanced-analytics/r-services/step-5-train-and-save-a-model-using-t-sql.md).  저장 프로시저를 사용하여 Machine Learning 모델을 빌드 및 저장합니다.  
  
-   [6단계: 모델 운영화](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md).  모델을 데이터베이스에 저장한 후 저장 프로시저를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 예측을 위해 모델을 호출합니다.  
  
> [!NOTE]  
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 R 코드를 작성하거나 테스트하지 않는 것이 좋습니다. 저장 프로시저에 포함하는 R 코드에 문제가 있을 경우 일반적으로 저장 프로시저에서 반환된 정보는 오류의 원인을 파악하기에 적합하지 않습니다.   
>   
> 디버깅을 위해 RStudio 또는 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)] 등의 도구를 사용하는 것이 좋습니다. 이 자습서에서 제공하는 R 스크립트는 기존 R 도구를 사용하여 이미 개발 및 디버그되었습니다.  
>   
> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 실행할 수 있는 R 스크립트를 개발하는 방법을 알아보려면 [데이터 과학 종단 간 연습](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md) 자습서를 참조하세요.  
  
### 시나리오  
이 연습에서는 잘 알려진 NYC Taxi 데이터 집합을 사용합니다. 이 공용 데이터 집합에는 17,300만건 이상의 2013년 개별 택시 여정과 각 여정에 대해 지불된 요금에 대한 세부 정보를 설명하는 20GB의 압축된 CSV 파일(압축되지 않은 경우 ~48GB)이 포함되어 있습니다. 이 연습을 쉽고 빠르게 수행하기 위해 데이터의 1%, 즉 1,703,957개 행과 23개 열로 구성된 대표 샘플링을 만들었습니다. 이 연습에서는 이 데이터를 사용하여 하루 중의 시간, 거리, 승차 위치 등의 열에 따라 특정 여정이 팁을 받을 가능성이 있는지 여부를 예측하는 이진 분류 모델을 작성합니다.  
  
  
### 요구 사항  
이 연습은 데이터베이스 및 테이블 만들기, 테이블로 데이터 가져오기, SQL 쿼리 만들기 등의 기본적인 데이터베이스 작업에 이미 익숙한 사용자를 대상으로 합니다. 모든 R 코드가 제공되므로 R 개발 환경은 필요하지 않습니다. 숙련된 SQL 프로그래머는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하거나 제공된 PowerShell 스크립트를 실행하여 이 연습을 완료할 수 있습니다.  
  
그러나 이 연습을 시작하기 전에 다음과 같은 준비 작업을 완료해야 합니다.  
  
-   SQL Server R Services를 사용할 수 있는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스에 연결합니다(CTP 3 이상 필요). 자세한 내용은 [SQL Server R Services(In-Database) 설치](https://msdn.microsoft.com/library/mt696069.aspx)의 설치 지침을 참조하세요.  
  
 -   이 연습에 사용하는 로그인에 데이터베이스 및 기타 개체를 만들고, 데이터를 업로드하고, 데이터를 선택하고, 저장 프로시저를 실행할 수 있는 권한이 있어야 합니다.  
  
## 다음 단계  
[1단계: 샘플 데이터 다운로드](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)  
  
## 참고 항목  
[SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
  
