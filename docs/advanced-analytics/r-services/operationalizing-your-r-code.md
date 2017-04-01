---
title: "작업에서 R 코드 활용 | Microsoft Docs"
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
ms.assetid: f15696b1-2479-4e5f-ac5e-4beaf958a043
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 작업에서 R 코드 활용
  데이터베이스 개발자는 여러 기술을 통합하고 엔터프라이즈 전체에서 공유할 수 있도록 통합 결과를 취합합니다. 그리고 응용 프로그램 개발자, SQL 개발자 및 데이터 과학자와 협력하여 솔루션을 설계하고 권장 데이터 관리 방법을 제시하고 솔루션을 구축/배포합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서는 데이터 과학자와 함께 작업을 하는 개발자를 위해 많은 이점을 제공합니다.  
  
-   **R 스크립트를 사용 하 여 상호 작용할 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.** 보고서를 작성 하는 분석가 뿐만 아니라 응용 프로그램 및 데이터베이스 개발자는 시스템 저장 프로시저에서 호출 하 여 R 스크립트를 호출할 수 있습니다.  
  
     기본 구문에 대 한 자세한 내용은 참조 [sp_execute_external_script & #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 및 [T-SQL에서 R 코드를 사용 하 여](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)합니다.  
 
    확장된 된 예제 R 운영할 수 있도록 하는 방법에 대 한 저장된 프로시저를 사용 하는 코드를 참조 하십시오 [SQL 개발자에 대 한 데이터베이스에서 분석](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)합니다.
  
     R 스크립트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 통합하는 경우에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 통해 R 스크립트를 실행하고 결과를 응용 프로그램에 포함할 수도 있습니다. 예를 들어 R 스크립트를 실행하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서를 만든 다음 그림과 예측 내용을 보고서에 표시할 수 있습니다.  
  
-   **뛰어난 성능과 확장성.** RevoScaleR 패키지 Api에서 제공 되는 오픈 소스 R 언어 제한 사항이에 알려져 있지만 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 큰 데이터 집합에 작동 하며 다중 스레드, 다중 코어 및 다중 프로세스에 해당 하는 데이터베이스에서의 계산에서 이점을 얻을 수 있습니다.  
  
     사용 중인 R 솔루션이 복합 집계를 사용하거나 큰 데이터 집합에서 실행되는 경우에는 효율성이 뛰어난 SQL의 메모리 내 집계 및 columnstore 인덱스를 활용할 수 있으며 R 코드가 통계 계산 및 점수 매기기를 수행하도록 지정할 수 있습니다.  
  
-   **표준 개발 및 관리 도구.** 관리나 개발을 위한 도구가 추가로 필요하지 않습니다. 저장 프로시저를 호출하여 모든 R 작업을 호출할 수 있습니다.  
  
     뿐만 아니라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터에 대해 실행하는 것과 같은 R 코드를 Hadoop 등의 다른 데이터 원본에 사용할 수도 있습니다.  
  
 이 섹션에서는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 사용하여 R 솔루션을 올바르게 변환하고 프로덕션 환경으로 배포하기 위해 이해해야 하는 개념을 설명합니다.  
  
## 섹션 내용

[R 데이터 형식 사용](../../advanced-analytics/r-services/working-with-r-data-types.md)

[R 서비스에서 사용 하기 위해 R 코드 변환](../../advanced-analytics/r-services/converting-r-code-for-use-in-r-services.md)

##  <a name="bkmk_RelatedTasks"></a> 관련 태스크  
  
[성능 조정 R SQL Server 서비스](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
## 참고 항목  
 [SQL Server R Services 기능 및 태스크](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 [sp_execute_external_script & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  
  