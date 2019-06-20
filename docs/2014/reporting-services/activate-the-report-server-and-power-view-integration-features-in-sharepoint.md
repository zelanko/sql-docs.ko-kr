---
title: 보고서 서버 및 SharePoint에서 Power View 통합 기능 활성화 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c7f64a54-c555-4d31-bf99-3abe57dc8626
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e30ae6ea0e7fa314748c4da265650273c0a7d56e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110032"
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>SharePoint에서 보고서 서버 및 파워 뷰 통합 사이트 모음 기능 활성화
  SharePoint 제품용 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 추가 기능을 설치하면 일반적으로 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 사이트 모음 기능이 기본적으로 활성화됩니다. 일부 경우에는 기능을 수동으로 활성화해야 하는 경우도 있습니다.  
  
 SharePoint 제품의 설치 이후에 SharePoint 2010 제품용 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능을 설치하면 보고서 서버 통합 기능 및 파워 뷰 통합 기능이 루트 사이트 모음에 대해서만 활성화됩니다. 기타 사이트 모음의 경우 기능을 수동으로 활성화해야 합니다. 예를 들어 **http://[내 서버 이름]/sites/[사이트 모음 이름]** 의 사이트 모음이 있는 경우 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 사이트 모음 기능을 수동으로 활성화해야 합니다.  
  
 루트 사이트 모음이 없으면 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능이 다음과 유사한 메시지를 기록합니다.  
  
 "SharePoint 웹 응용 프로그램 80에는 루트 사이트 모음이 없습니다."  
  
 "RS_SP_ #.log" 라는 여기서 #은 증분 번호 추가 기능 설치 로그에 메시지를 찾을 수 있습니다. 로그 파일은 현재 사용자 Temp 폴더(예: C:\Users\\[사용자 이름]\AppData\Local\Temp)에서 찾을 수 있습니다. 추가 기능을 사용 하 여 로깅 옵션에 대 한 자세한 내용은 참조 하세요. [설치 또는 SharePoint 용 Reporting Services 추가 기능에 제거 &#40;SharePoint 2010 및 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)합니다.  
  
 항목 내용  
  
-   [보고서 서버 및 파워 뷰 통합 사이트 모음 기능을 활성화하려면](#bkmk_features)  
  
-   [사이트 모음에서 Reporting Services 중앙 관리 사이트 모음 기능을 활성화 또는 비활성화하려면](#bkmk_centraladmin)  
  
##  <a name="bkmk_features"></a> 보고서 서버 및 파워 뷰 통합 사이트 모음 기능을 활성화하려면  
  
1.  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능을 활성화하려는 사이트로 브라우저를 엽니다.  
  
2.  **사이트 작업**을 클릭합니다.  
  
3.  **사이트 설정**을 클릭합니다.  
  
4.  사이트 모음 관리 그룹에서 **사이트 모음 기능** 을 클릭합니다.  
  
5.  목록에서 **보고서 통합 기능** 이나 **파워 뷰 통합 기능** 을 찾습니다.  
  
6.  **활성화**를 클릭합니다.  
  
 기능을 비활성화하려면 동일한 절차를 수행하고 **활성화** 대신 **비활성화**를 클릭합니다.  
  
##  <a name="bkmk_centraladmin"></a> 사이트 모음에서 Reporting Services 중앙 관리 사이트 모음 기능을 활성화 또는 비활성화하려면  
  
1.  SharePoint 중앙 관리로 브라우저를 엽니다.  
  
2.  **사이트 작업**을 클릭합니다.  
  
3.  **사이트 설정**을 클릭합니다.  
  
4.  사이트 모음 관리 그룹에서 **사이트 모음 기능** 을 클릭합니다.  
  
5.  목록에서 **보고서 서버 중앙 관리 기능** 을 찾습니다.  
  
6.  **활성화**를 클릭합니다.  
  
 기능을 비활성화하려면 동일한 절차를 따르면서 **활성화** 대신 **비활성화**를 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 기능이 활성화된 후에는 계속해서 서버 통합을 수행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [설치 또는 제거는 Reporting Services 추가-SharePoint 용 &#40;SharePoint 2010 및 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
