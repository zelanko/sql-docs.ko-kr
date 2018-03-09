---
title: "SQL Server Reporting Services 보고서 서버의 구성 및 관리 | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server-sharepoint
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: efb98dd68a61c2952de23dde6d6c61086d5e4207
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="configuration-and-administration-of-a-sql-server-reporting-services-report-server"></a>SQL Server Reporting Services 보고서 서버의 구성 및 관리

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services는 조직에서 사용할 보고서를 작성, 배포 및 관리하는 데 도움이 되는 다양하고 간편한 도구와 서비스뿐만 아니라 보고 기능을 확장하고 사용자 지정할 수 있는 프로그래밍 기능도 제공하는 서버 기반 보고 플랫폼입니다. 보고 환경을 SharePoint 제품과 통합하면 SharePoint 사이트에서 제공하는 공동 작업 환경을 사용하는 이점을 얻을 수 있습니다.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

다음 섹션을 통해 Reporting Services 환경과 SharePoint 제품 또는 기술의 통합에 대한 개념, 배포 시나리오, 절차 등을 더 잘 이해할 수 있습니다.  
  
-   SharePoint 문서 라이브러리의 메뉴 옵션  
  
    -   [SharePoint 사용자용 데이터 경고 관리자](../../reporting-services/data-alert-manager-for-sharepoint-users.md)  
  
    -   [SharePoint 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
    -   [SharePoint 사이트의 보고서 데이터 원본에서 자격 증명 업데이트](../../reporting-services/report-data/update-credentials-in-report-data-sources-from-a-sharepoint-site.md)  
  
    -   [공유 데이터 집합 관리](../../reporting-services/report-data/manage-shared-datasets.md)  
  
    -   [게시된 보고서에 매개 변수 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)  
  
    -   [처리 옵션 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
    -   [캐시 새로 고침 옵션&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6)  
  
-   [Reporting Services 사이트 모음 기능](../../reporting-services/report-server-sharepoint/site-collection-features-reporting-services.md)  
  
-   [SharePoint에서 보고서 서버 및 파워 뷰 통합 사이트 모음 기능 활성화](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)  
  
-   [Reporting Services 사이트 설정 및 사이트 기능&#40;SharePoint 모드&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)  
  
-   [SharePoint 중앙 관리에서 보고서 서버 파일 동기화 기능 활성화](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  
  
-   [SharePoint 라이브러리에 Reporting Services 콘텐츠 형식 추가](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
-   [보고서 뷰어의 로컬 모드와 보고서 뷰어의 연결 모드 보고서&#40;SharePoint 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)  
  
-   [SharePoint 라이브러리에 문서 업로드&#40;SharePoint 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
-   [처리 옵션 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
 Reporting Services에 대한 일반적인 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 [Reporting Services](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)를 참조하세요. 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소, 도구 및 리소스에 대한 자세한 내용은 [SQL Server 온라인 설명서](../../sql-server/sql-server-technical-documentation.md)를 참조하십시오.  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
