---
title: 지원 되는 SharePoint 및 Reporting Services 서버와 추가 기능 조합 (SQL Server 2014) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 05f0997cb73a156e54b22ad280fa5d6eb0ec7d73
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108647"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server-and-add-in-sql-server-2014"></a>지원되는 SharePoint와 Reporting Services 서버 및 추가 기능의 조합(SQL Server 2014)
  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버는 SharePoint 모드로 설치하고 SharePoint 배포와 통합할 수 있습니다. 보고서 서버, SharePoint용 Reporting Services 추가 기능 및 SharePoint 제품의 모든 조합에서 모든 기능이 지원되는 것은 아닙니다. 이 항목에는 지원되는 조합이 요약되어 있습니다. 
  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 통합은 다음과 같은 조합의 결과입니다.  
  
-   SharePoint 모드로 구성된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 버전  
  
-   SharePoint 제품  
  
-   SharePoint 서버에 설치하는 SharePoint 제품을 위한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Sharepoint 2013 &#124; SharePoint 2010 &#124; SharePoint 2007|  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>지원되는 SharePoint와 Reporting Services 구성 요소의 조합  
 다음 표에서는 보고서 서버, SharePoint 제품용 Reporting Services 추가 기능, SharePoint 제품에 대해 지원되는 조합 형태를 요약해서 보여 줍니다. 다음 표에 나열되지 않은 조합은 지원되지 않습니다.  
  
### <a name="supported-combinations"></a>지원되는 조합  
  
||보고서 서버|추가 기능|SharePoint 버전|지원됨|  
|-|-------------------|-------------|------------------------|---------------|  
|1|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|yes|  
|2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|yes|  
|3|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|yes|  
|4|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|yes<br /><br /> 예외: 파워 뷰 통합은 지원 되지 않습니다.|  
|5|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|yes|  
|6|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|yes|  
|7|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|yes|  
|8|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|yes|  
|9|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]2|SharePoint 2007|yes|  
|10|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]이상을|SharePoint 2010|yes|  
|11|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]및 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|yes|  
  
 기능 및 보고서 서버 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 모드에 대 한 자세한 내용은 [Reporting Services report server](../reporting-services-report-server.md)를 참조 하십시오.  
  
 **추가 참고 사항:**  
  
-   Power View 통합을 비롯한 SharePoint 2013 지원에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 SQL Server 2012 SP1 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 버전이 필요합니다.  
  
-   Power View는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 도입되었습니다. 따라서 SharePoint 2010과의 Power View 통합에는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상의 추가 기능이 필요합니다.  
  
-   SQL Server 2008 R2 추가 기능은 SQL Server 2012 이상의 보고서 서버에서 지원되지 않습니다. SharePoint 2010 필수 구성 요소 설치 관리자는 SQL Server 2008 R2 추가 기능을 자동으로 설치합니다. 이 추가 기능은 최신 버전의 추가 기능을 설치하기 전에 제거해야 합니다. 추가 기능의 내부 업그레이드는 지원되지 않습니다.  
  
-   **업그레이드:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능이 설치 된 sharepoint 2010는 sharepoint 2013로 바로 업그레이드할 수 없습니다. SharePoint 2013에는 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 및 보고서 서버가 필요합니다. 업그레이드에 대한 자세한 내용은 [Upgrade and Migrate Reporting Services](upgrade-and-migrate-reporting-services.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint 제품용 Reporting Services 추가 기능을 찾을 수 있는 위치](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Upgrade and Migrate Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
  
