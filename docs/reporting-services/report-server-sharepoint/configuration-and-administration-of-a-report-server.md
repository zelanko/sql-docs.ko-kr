---
title: 보고서 서버의 구성 및 관리(SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 6e39153fb15c79cdbc07dc7d97407e2880bdc156
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65574417"
---
# <a name="configuration-and-administration-of-a-sql-server-reporting-services-ssrs-report-server"></a>SSRS(SQL Server Reporting Services) 보고서 서버의 구성 및 관리

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
  
    -   [공유 데이터 세트 관리](../../reporting-services/report-data/manage-shared-datasets.md)  
  
    -   [게시된 보고서에 매개 변수 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)  
  
    -   [처리 옵션 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
-   [Reporting Services 사이트 모음 기능](../../reporting-services/report-server-sharepoint/site-collection-features-reporting-services.md)  
  
-   [SharePoint에서 보고서 서버 및 파워 뷰 통합 사이트 모음 기능 활성화](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)  
  
-   [Reporting Services 사이트 설정 및 사이트 기능&#40;SharePoint 모드&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)  
  
-   [SharePoint 중앙 관리에서 보고서 서버 파일 동기화 기능 활성화](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  
  
-   [SharePoint 라이브러리에 Reporting Services 콘텐츠 형식 추가](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
-   [보고서 뷰어의 로컬 모드와 보고서 뷰어의 연결 모드 보고서&#40;SharePoint 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)  
  
-   [SharePoint 라이브러리에 문서 업로드&#40;SharePoint 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
-   [처리 옵션 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
