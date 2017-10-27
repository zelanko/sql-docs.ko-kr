---
title: "보고서 서버와 SharePoint의 Power View 통합 기능을 활성화 | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: e97378914a59fab938fc3e4c7926847effcffc94
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>보고서 서버와 SharePoint의 Power View 통합 기능 활성화

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  설치 후 기본적으로 Reporting Services 사이트 모음 기능 활성화 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] SharePoint 제품 용 추가 기능을 합니다. 경우에 따라 기능을 수동으로 활성화 해야 합니다.  

> [!NOTE]
> SQL Server 2016 후 SharePoint와 reporting Services 통합을 사용할 수 없습니다.

 SharePoint 제품의 설치 후 Reporting Services에 추가 기능에 대 한 SharePoint 2010 제품 설치 하는 경우 다음 보고서 서버 통합 기능 및 Power View 통합 기능이 활성화 됩니다 루트 사이트 모음에 대 한 합니다. 기타 사이트 모음의 경우 기능을 수동으로 활성화 해야 합니다. 예를 들어, 사이트 모음에 있는 경우 **http://[my 서버 이름] /sites/ [사이트 모음 이름]** Reporting Services 사이트 모음 기능을 수동으로 활성화 해야 합니다.  
  
 루트 사이트 모임이 없으면 되는 경우 Reporting Services 추가 기능에 메시지를 기록 합니다 다음과 비슷합니다.  
  
 "SharePoint 웹 응용 프로그램 80에는 루트 사이트 모음이 없습니다."  
  
 메시지를 "RS_SP_ #.log" #는 증가 숫자 이라는 추가 기능 설치 로그에서 찾을 수 있습니다. 예를 들어 C:\Users는 현재 사용자 Temp 폴더에 로그 파일이\\[사용자 이름] \AppData\Local\Temp 합니다. 추가 기능의 로깅 옵션에 대한 자세한 내용은 [SharePoint용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)를 참조하세요.  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>보고서 서버 및 Power View 통합 사이트 모음 기능 활성화
  
1.  저장할 Reporting Services 기능 활성화 사이트로 브라우저를 엽니다.  
  
2.  **사이트 작업**을 클릭합니다.  
  
3.  **사이트 설정**을 클릭합니다.  
  
4.  사이트 모음 관리 그룹에서 **사이트 모음 기능** 을 클릭합니다.  
  
5.  목록에서 **보고서 통합 기능** 이나 **파워 뷰 통합 기능** 을 찾습니다.  
  
6.  **활성화**를 클릭합니다.  
  
 기능을 비활성화하려면 동일한 절차를 수행하고 **활성화** 대신 **비활성화**를 클릭합니다.  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>활성화 또는 비활성화 하는 Reporting Services 중앙 관리 사이트 모음 기능
  
1.  SharePoint 중앙 관리로 브라우저를 엽니다.  
  
2.  **사이트 작업**을 클릭합니다.  
  
3.  **사이트 설정**을 클릭합니다.  
  
4.  사이트 모음 관리 그룹에서 **사이트 모음 기능** 을 클릭합니다.  
  
5.  목록에서 **보고서 서버 중앙 관리 기능** 을 찾습니다.  
  
6.  **활성화**를 클릭합니다.  
  
 기능을 비활성화하려면 동일한 절차를 따르면서 **활성화** 대신 **비활성화**를 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계

기능이 활성화된 후에는 계속해서 서버 통합을 수행할 수 있습니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)

