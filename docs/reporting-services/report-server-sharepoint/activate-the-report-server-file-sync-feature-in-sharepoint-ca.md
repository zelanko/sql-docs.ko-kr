---
title: "SharePoint CA에 보고서 서버 파일 동기화 기능 활성화 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 32d1988d-07e7-41c2-b636-e65ecfae4677
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d9f1b75bc40693248526282a6565db340930601b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-ca"></a>SharePoint CA에 보고서 서버 파일 동기화 기능 활성화
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 파일 동기화 기능은 SharePoint 이벤트 처리기를 활용하여 보고서 서버 카탈로그를 문서 라이브러리의 항목과 동기화합니다. 이 기능은 사용자가 게시된 보고서 항목을 SharePoint 문서 라이브러리에 직접 자주 업로드하는 경우에 유용합니다. 파일 동기화 기능이 활성화되지 않은 경우 내용이 동기화되지만 자주 동기화되지는 않습니다.  
  
 파일 동기화 기능은 SharePoint 제품용 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 추가 기능을 설치한 후 SharePoint 사이트 관리에서 활성화할 수 있습니다.  
  
 이 기능은 사이트별로 수동으로 활성화하고 비활성화할 수 있으나 사이트 모음 수준에서는 이렇게 할 수 없습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 SharePoint용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치해야 합니다. 추가 기능이 설치되어 있지 않으면 파일 동기화 기능이 사이트 기능 목록에 표시되지 않습니다.  
  
 설치를 확인하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows **제어판**에서 설치된 응용 프로그램 목록을 확인합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능이 설치되어 있으면 이 항목의 지침에 따라 보고서 서버 파일 동기화 기능을 활성화합니다.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>사이트에서 Reporting Services 파일 동기화 기능을 활성화 또는 비활성화하려면  
  
1.  사이트의 주 페이지에서 **사이트 동작** 메뉴를 클릭하고 **사이트 설정**을 클릭합니다.  
  
2.  **사이트 동작** 에서 **사이트 기능 관리**를 클릭합니다.  
  
3.  목록에서 **보고서 서버 파일 동기화** 를 찾습니다.  
  
4.  **활성화**를 클릭합니다.  
  
> [!NOTE]  
>  보고서 서버 파일 동기화 기능을 비활성화하려면 동일한 절차를 따르면서 **비활성화**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 파트 문제 해결(보고서 작성기 및 SSRS)](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [SharePoint에서 보고서 서버 및 파워 뷰 통합 사이트 모음 기능 활성화](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
 [SharePoint용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [SharePoint용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
