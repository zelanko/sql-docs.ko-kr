---
title: "Power BI 통합 (웹 포털)을 위한 내 설정 | Microsoft Docs"
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- pbi
- power bi
- power bi integration
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 8e627f20918a4d6ee5f882677ccc7b2c26616e2f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/17/2017

---

# <a name="my-settings-for-power-bi-integration-web-portal"></a>Power BI 통합을 위한 내 설정(웹 포털)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]의 **내 설정** 페이지는 개별 사용자가 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]를 통한 로그인을 관리하는 데 사용됩니다. 보고서 항목을 고정하는 단계를 진행할 때는 로그인하라는 메시지가 자동으로 표시됩니다.  그러나 수동으로 로그인해야 하거나 로그아웃해야 하는 경우 **내 설정** 페이지를 사용할 수 있습니다.  **내 설정** 메뉴 옵션이 표시되지 않는 경우 보고서 서버가  [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]에 통합되지 않은 것입니다.  자세한 내용은 [Power BI 보고서 서버 통합&#40;구성 관리자&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)를 통한 로그인을 관리하는 데 사용됩니다.  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## <a name="why-sign-in"></a>로그인해야 하는 이유

 로그인하면 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 사용자 계정과 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 계정 간에 관계가 설정됩니다.  로그인 시에는 90일 동안 유효한 보안 토큰이 생성됩니다. 토큰이 만료되는 경우 Power BI에 고정된 항목이 있으면 알림이 표시됩니다.  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 대시보드 내의 타일은 **MySettings**를 통해 다시 로그인한 다음에야 새로 고쳐집니다.  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
로그인하고 나면 새 보안 토큰이 생성됩니다.  대시보드 타일은 이전에 구성한 일정으로 업데이트되기 시작합니다.  

## <a name="next-steps"></a>다음 단계

[Power BI 보고서 서버 통합](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
[Power BI 대시보드에 Reporting Services 항목 고정](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
[Power BI의 대시보드](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
[웹 포털](../reporting-services/web-portal-ssrs-native-mode.md)  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
