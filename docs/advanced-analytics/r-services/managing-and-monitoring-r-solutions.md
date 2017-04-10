---
title: "R 솔루션 관리 및 모니터링 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# R 솔루션 관리 및 모니터링
  데이터베이스 관리자는 경쟁 프로젝트와 우선 순위를 단일 연락 지점 즉, 데이터베이스 서버로 통합해야 합니다. 이들은 운영 및 보고 데이터 저장소의 상태를 유지하면서 데이터 과학자뿐만 아니라 다양한 보고서 개발자, 비즈니스 분석가, 비즈니스 데이터 소비자에게 데이터 액세스를 제공해야 합니다. 엔터프라이즈에서 DBA는 데이터 과학을 위한 효과적인 인프라를 구축하고 배포하는 핵심적인 부분입니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 는 데이터 과학 임무를 지원하는 데이터베이스 관리자에게 많은 이점을 제공합니다.  
  
-   **보안.** 아키텍처 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 데이터베이스 보안을 유지 하 여 데이터베이스 인스턴스의 작업에서 R 세션의 실행을 격리 합니다.  
  
     R 스크립트 실행 권한을 갖는 사람을 지정하고 R 작업에 사용되는 데이터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 정의된 보안 역할과 같은 역할을 사용하여 관리되도록 할 수 있습니다.  
  
-   **안정성.** R 세션은 R 세션에 문제가 발생하더라도 서버가 평상시처럼 계속 실행되도록 하기 위해서 별도의 프로세스로 실행됩니다. 낮은 권한 실제 사용자 계정은 포함 하 고 R 인스턴스를 격리 하는 데 사용 됩니다.   
  
-   **리소스 관리.** 대규모 계산이 서버의 전반적인 성능을 저해하지 않도록 R 런타임에 할당된 리소스 양을 제어할 수 있습니다.  
  
  
## 섹션 내용  
 [R 서비스 모니터링](../../advanced-analytics/r-services/monitoring-r-services.md)
 
 [R 서비스에 대 한 리소스 관리](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
 
[설치 하 고 R 패키지를 관리 합니다.](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)
  
[구성](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 

+ [고급 분석 확장 구성 및 관리](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)  
  
+  [SQL Server R Services용 사용자 계정 풀 수정](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  

 [SQL Server의 R 런타임 관련 보안 고려 사항](../../advanced-analytics/r-services/security-considerations-for-the-r-runtime-in-sql-server.md)  
  
 
  
## 참고 항목  
 [SQL Server R Services 기능 및 태스크](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
  