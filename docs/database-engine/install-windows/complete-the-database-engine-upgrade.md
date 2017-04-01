---
title: "데이터베이스 엔진 업그레이드 완료 | Microsoft Docs"
ms.custom: ""
ms.date: "09/22/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: 10
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 10
---
# 데이터베이스 엔진 업그레이드 완료
  SQL Server 2016으로 업그레이드를 완료한 후에는 여러 추가 단계를 수행해야 할 수 있습니다. 여기에는 다음과 같은 옵션이 포함됩니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드한 후에 다음 태스크를 완료하세요.  
  
-   **데이터베이스 백업:** 업그레이드된 각 데이터베이스의 전체 백업을 수행합니다.  
  
-   **새 기능 설정:** SQL Server 2016에서는 데이터베이스에 대한 DATABASE_COMPATIBILITY 수준을 130으로 변경해야 일부 변경 내용이 활성화됩니다.  자세한 내용 및 권장되는 워크플로는 [데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)을 참조하세요.  
  
-   **Integration Services:**  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 형식으로 Integration Services 패키지를 마이그레이션합니다. 자세한 내용은 [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md)를 참조하세요.  
  
-   **Reporting Services:** 새로 설치한 SQL Server를 업그레이드하는 경우 Reporting Services 암호화 키를 복원합니다. 자세한 내용은 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/back-up-and-restore-reporting-services-encryption-keys.md)을 참조하세요.  
  
-   **Master Data Services:**  MDS 데이터베이스 스키마를 업그레이드하고 SQL Server 2016 웹 응용 프로그램을 만듭니다. 자세한 내용은 [Upgrade Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md)를 참조하세요.  
  
-   **Data Quality Services:** DQS 데이터베이스 스키마를 업그레이드하고 DQS 데이터베이스 스키마 업그레이드를 확인합니다. 자세한 내용은 [Upgrade Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)를 참조하세요.  
  
-   **전체 텍스트 검색:** 쿼리 결과의 의미 일관성을 유지하기 위해 전체 텍스트 카탈로그를 다시 채웁니다. 자세한 내용은 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)를 참조하세요.  
  
## 이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Complete%20the%20Database%20Engine%20Upgrade%20page)으로 보내 주세요.  
  
  