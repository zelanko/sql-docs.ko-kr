---
title: "지원되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합(SQL Server 2016) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SharePoint 모드"
  - "SharePoint 추가 기능"
  - "rsSharePoint"
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
caps.latest.revision: 39
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# 지원되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합(SQL Server 2016)
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  SharePoint 모드로 설치된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에는 SharePoint 서버에 설치하는 SharePoint의 버전과 SharePoint용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(rsSharePoint.msi) 제품이 필요합니다.  이 항목에는 지원되는 조합이 요약되어 있습니다.  
  
## 지원되는 SharePoint와 Reporting Services 구성 요소의 조합  
 다음 표에서는 보고서 서버, SharePoint 제품용 Reporting Services 추가 기능, SharePoint 제품에 대해 지원되는 조합 형태를 요약해서 보여 줍니다. 다음 표에 나열되지 않은 조합은 지원되지 않습니다.  
  
### 지원되는 조합  
  
||보고서 서버|추가 기능|SharePoint 버전|  
|-|-------------------|-------------|------------------------|  
|1|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|SharePoint 2016|  
|2|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|SharePoint 2013|  
|3|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|  
|4|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|5|SQL Server 2012 SP3|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 SQL Server 2012 SP3|SharePoint 2013|  
|6|SQL Server 2012 SP2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 SQL Server 2012 SP2|SharePoint 2013|  
|7|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|  
|8|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]*|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|9|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|  
|10|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|11|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|  
|12|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|  
|13|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|  
|14|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|  
|15|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 및 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|  
  
 *예외: 파워 뷰 통합은 지원되지 않습니다.  
  
 추가 기능 다운로드 페이지에 대한 자세한 내용은 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조하세요.  
  
 **참고 사항:**  

- 팜 내의 모든 SharePoint 서버를 업그레이드해야 합니다. 여기에는 앱 및 웹 프런트 엔드 서버가 포함됩니다.

-   Power View 통합을 비롯한 SharePoint 2016 지원에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 SQL Server 2016 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 버전이 필요합니다.  

-   Power View 통합을 비롯한 SharePoint 2013 지원에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 SQL Server 2012 SP1 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 버전이 필요합니다.  
  
-   Power View는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 도입되었습니다. 따라서 SharePoint 2010과의 Power View 통합에는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상의 추가 기능이 필요합니다.  
  
-   SQL Server 2008 R2 추가 기능은 SQL Server 2012 이상의 보고서 서버에서 지원되지 않습니다. SharePoint 2010 필수 구성 요소 설치 관리자는 SQL Server 2008 R2 추가 기능을 자동으로 설치합니다. 이 추가 기능은 최신 버전의 추가 기능을 설치하기 전에 제거해야 합니다. 추가 기능의 내부 업그레이드는 지원되지 않습니다.  
  
-   **업그레이드:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능이 설치된 SharePoint 2010은 SharePoint 2013으로 해당 위치에서 업그레이드할 수 없습니다. SharePoint 2013에는 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 및 보고서 서버가 필요합니다. 업그레이드에 대한 자세한 내용은 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)을 참조하십시오.  
  
## 관련 항목:  
 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [SQL Server 2016 버전에서 지원하는 기능](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)   
 [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)  
  
  