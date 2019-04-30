---
title: 경고 담당자용 데이터 경고 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: 32fd968f-1c0c-4ba8-851c-8a3b5e1fbbf2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4096d6fed3d73faffdc8798c475954bdb031dd68
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63165081"
---
# <a name="data-alert-manager-for-alerting-administrators"></a>경고 담당자를 위한 데이터 경고 관리자입니다.
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에는 데이터 경고를 관리할 수 있도록 SharePoint 경고 담당자를 위한 데이터 경고 관리자가 제공됩니다. 경고 담당자는 사이트에 저장된 모든 경고에 대한 정보를 보고, 경고를 삭제할 수 있습니다. 다음 그림에서는 데이터 경고 관리자에서 SharePoint 경고 담당자가 사용할 수 있는 기능을 보여 줍니다.  
  
 ![SharePoin 사이트 관리자용 경고 관리자](media/rs-alertmanagersite.gif "SharePoin 사이트 관리자용 경고 관리자")  
  
 사이트가 데이터 경고 기능을 사용하도록 설정된 경우 MyDataAlerts.aspx 및 SiteDataAlerts.aspx라는 두 SharePoint 페이지가 만들어지고 SharePoint 사이트에 추가됩니다. SiteDataAlerts.aspx는 경고 담당자를 위한 데이터 경고 관리자입니다. 경고 담당자는 사이트 설정 SharePoint 페이지에서 데이터 경고 관리자를 열 수 있습니다. 데이터 경고 관리자를 열려면 경고 담당자에게 SharePoint 경고 관리 권한이 있어야 합니다.  
  
 URL을 사용하여 데이터 경고 관리자를 직접 열 수도 있습니다. 다음은 URL의 구문을 보여 줍니다.  
  
 `http: //<site name>/_layouts/ReportServer/ SiteDataAlerts.aspx`  
  
> [!NOTE]  
>  경고 관리자는 정보 근로자에게 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 데이터 경고 기능에 대한 액세스 권한을 부여할 수 있습니다. 필요한 사용 권한에 대한 자세한 내용은 [Reporting Services 데이터 경고](../ssms/agent/alerts.md)를 참조하세요.  
  
##  <a name="ViewingAlerts"></a> 데이터 경고 정보 보기  
 SharePoint에 Reporting Services가 설치 및 구성되면 사이트 설정 SharePoint 페이지에 **Reporting Services** 옵션이 포함됩니다. 경고 담당자는 Reporting Service 내에서 **데이터 경고 관리** 옵션을 클릭하여 데이터 경고 관리자를 열 수 있습니다. 다음 그림에서는 사이트 설정 페이지에서 데이터 경고 관리자를 여는 방법을 보여 줍니다.  
  
 ![사이트 설정 페이지의 Reporting Services 섹션](media/rs-sitesettings.gif "사이트 설정 페이지의 Reporting Services 섹션")  
  
 데이터 경고 관리자에는 경고 이름, 보고서 이름, 경고 소유자 이름, 경고 메시지를 보낸 횟수, 경고가 마지막으로 실행된 시간, 경고 정의가 마지막으로 수정된 시간 및 경고 메시지 상태를 나열하는 테이블이 포함되어 있습니다. 경고를 생성하거나 보낼 수 없으면 상태 열에 오류에 대한 정보가 포함되어 경고 문제를 해결하도록 돕습니다. 자세한 내용은 [데이터 경고 관리자에서 SharePoint 사이트의 모든 데이터 경고 관리](manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)을(를) 참조하세요.  
  
 다음 표에서는 데이터 경고 관리자에 있는 테이블의 예제 데이터를 보여 줍니다. 오류가 발생한 경우 오류 메시지와 로그의 항목 식별자(GUID)가 테이블의 **상태** 필드에 포함되어 있습니다.  
  
|경고 이름|보고서 이름|만든 사람|보낸 경고|마지막 실행|마지막으로 수정한 날짜|상태|  
|----------------|-----------------|----------------|-----------------|--------------|-------------------|------------|  
|SalesQTR|SalesByTerritoryAndQTR|Lauren Johnson|4|6/12/2011|6/1/2011|마지막 경고가 성공적으로 실행되고 경고가 전송되었습니다.|  
|UnitsSold|ProductsSalesByQTR|Michael Blythe|2|7/1/2011|6/28/2011|마지막 경고가 성공적으로 실행되었지만 데이터가 변경되지 않아서 경고를 보내지 않았습니다.|  
|InventoryCount|StockStatusByQTR|Lauren Johnson|7|7/10/2011|7/2/2011|\<오류 메시지>로그 파일에 오류에 대한 자세한 내용이 포함되어 있습니다. 식별자를 사용 하 여 로그 항목을 참조 하세요. \<GUID>.|  
|TopPromotion|PromotionTracking|Cristian Petculescu|0||5/23/2011|경고를 만들었습니다.|  
  
 자세한 내용은 [데이터 경고 관리자에서 SharePoint 사이트의 모든 데이터 경고 관리](manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)를 참조하세요.  
  
 사이트 사용자가 만든 모든 경고를 볼 수 있습니다. 사용자를 선택한 다음 해당 사용자의 모든 경고를 보거나 특정 보고서에 대한 경고만 보도록 선택할 수 있습니다.  
  
  
##  <a name="DeleteAlerts"></a> 데이터 경고 삭제  
 데이터 경고 관리자에서 경고 정의를 삭제합니다. 모든 데이터 경고 정의에는 경고 정의를 만든 SharePoint 사용자인 소유자가 있습니다. 소유자는 자신이 만든 경고 정의만 삭제할 수 있습니다. 자세한 내용은 [데이터 경고 관리자에서 내 데이터 경고 관리](manage-my-data-alerts-in-data-alert-manager.md)를 참조하세요.  
  
 SharePoint 경고 담당자는 사이트의 모든 사용자가 만든 경고 정의를 나열한 다음 삭제할 수 있습니다. 자세한 내용은 [데이터 경고 관리자에서 SharePoint 사이트의 모든 데이터 경고 관리](manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)를 참조하세요.  
  
 경고 정의를 삭제하면 더 이상 경고가 전송되지 않습니다. 하지만 경고 데이터베이스를 쿼리하면 경고 정의가 계속 존재하는 것을 확인할 수 있습니다. 경고 서비스는 예약에 따라 정리를 수행하며 다음 정리 작업 시 경고 정의가 영구적으로 삭제됩니다. 기본 정리 간격은 20분입니다. 이러한 정리 간격은 구성할 수 있습니다. 자세한 내용은 [Reporting Services 데이터 경고](../ssms/agent/alerts.md)를 참조하세요.  
  
  
##  <a name="HowTo"></a> 관련 작업  
 이 섹션에는 경고를 관리하는 방법을 보여 주는 절차가 들어 있습니다.  
  
-   [데이터 경고 관리자에서 SharePoint 사이트의 모든 데이터 경고 관리](manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)  
  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 데이터 경고](../ssms/agent/alerts.md)  
  
  
