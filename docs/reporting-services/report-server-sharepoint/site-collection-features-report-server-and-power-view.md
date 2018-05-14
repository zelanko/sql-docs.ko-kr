---
title: SharePoint에서 보고서 서버 및 파워 뷰 통합 사이트 모음 기능 활성화 | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c6c6c314ec55a01fb6f2884cd6a5baace396efaf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>SharePoint에서 보고서 서버 및 파워 뷰 통합 사이트 모음 기능 활성화

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  SharePoint 제품용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 추가 기능을 설치하면 Reporting Services 사이트 모음 기능이 기본적으로 활성화됩니다. 일부 경우에는 기능을 수동으로 활성화해야 하는 경우도 있습니다.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

 SharePoint 제품 설치 후에 SharePoint 2010 제품용 Reporting Services 추가 기능을 설치하면 보고서 서버 통합 기능 및 파워 뷰 통합 기능이 루트 사이트 모음에 대해서만 활성화됩니다. 기타 사이트 모음의 경우 기능을 수동으로 활성화해야 합니다. 예를 들어 **http://[내 서버 이름]/sites/[사이트 모음 이름]** 의 사이트 모음이 있는 경우 Reporting Services 사이트 모음 기능을 수동으로 활성화해야 합니다.  
  
 루트 사이트 모음이 없으면 Reporting Services 추가 기능이 다음과 유사한 메시지를 기록합니다.  
  
 "SharePoint 웹 응용 프로그램 80에는 루트 사이트 모음이 없습니다."  
  
 "RS_SP_ #.log"라는 추가 기능 설치 로그에서 메시지를 찾을 수 있습니다. 여기서 #는 증가 숫자입니다. 로그 파일은 현재 사용자 Temp 폴더(예: C:\Users\\[사용자 이름]\AppData\Local\Temp)에서 찾을 수 있습니다. 추가 기능의 로깅 옵션에 대한 자세한 내용은 [SharePoint용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)를 참조하세요.  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>보고서 서버 및 파워 뷰 통합 사이트 모음 기능 활성화
  
1.  Reporting Services 기능을 활성화하려는 사이트로 브라우저를 엽니다.  
  
2.  **사이트 작업**을 클릭합니다.  
  
3.  **사이트 설정**을 클릭합니다.  
  
4.  사이트 모음 관리 그룹에서 **사이트 모음 기능** 을 클릭합니다.  
  
5.  목록에서 **보고서 통합 기능** 이나 **파워 뷰 통합 기능** 을 찾습니다.  
  
6.  **활성화**를 클릭합니다.  
  
 기능을 비활성화하려면 동일한 절차를 수행하고 **활성화** 대신 **비활성화**를 클릭합니다.  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>Reporting Services 중앙 관리 사이트 모음 기능 활성화 또는 비활성화
  
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
