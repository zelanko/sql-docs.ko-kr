---
title: "Reporting Services 사이트 모음 기능 | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server-sharepoint
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4d3a72452ef0383c4d05d1758bab92570db0df51
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="reporting-services-site-collection-features"></a>Reporting Services 사이트 모음 기능

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Reporting Services SharePoint 모드는 세 가지 SharePoint 사이트 모음 기능을 제공합니다. 이 기능은 일반적인 Reporting Services SharePoint 모드 보고 환경, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], SQL Server 2016 Reporting Services 추가 기능 및 SharePoint 중앙 관리의 Reporting Services에 대한 관리 작업을 지원합니다.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.
  
## <a name="site-collection-features"></a>사이트 모음 기능

 다음 표에서는 Reporting Services 사이트 모음 기능에 대해 설명합니다.  
  
|기능|Description|  
|-------------|-----------------|  
|**보고서 서버 중앙 관리 기능**|Reporting Services 보고서 서버와의 통합을 관리하기 위한 기능을 사용합니다. 이 기능은 SharePoint 중앙 관리 사이트 모음에서만 설치 및 사용됩니다.<br /><br /> SharePoint 제품용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 추가 기능을 설치하면 보고서 서버 통합 기능이 SharePoint 중앙 관리 사이트 모음에서 자동으로 활성화됩니다. 일부 경우에는 기능을 수동으로 활성화해야 하는 경우도 있습니다. 보고서 서버 기능을 활성화하려면 SharePoint 중앙 관리의 사이트 설정 페이지에서 Reporting Services 페이지를 사용합니다.<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Reporting Services 버전 이상의 SharePoint 제품용 추가 기능은 추가 기능이 설치될 때 기존의 모든 사이트 모음에 대해 보고서 서버 통합 기능을 활성화합니다. 또한 이 기능은 새 사이트 모음에 대해 자동으로 활성화됩니다.|  
|**보고서 서버 통합 기능**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Reporting Services를 사용하여 다양한 보고 기능을 활성화합니다.<br /><br /> 이 기능은 기본적으로 활성화되어 있습니다.|  
|**파워 뷰 통합 기능**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서 및 Analysis Services 테이블 형식 데이터베이스에 대해 대화형 데이터 탐색 및 시각적 표현을 사용합니다.<br /><br /> 이 기능은 다음 데이터 원본의 상황에 맞는 메뉴에서 액세스할 수 있습니다.<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> **.bism** 연결 파일<br /><br /> <br /><br /> 상황에 맞는 메뉴에 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 가 표시되지 않으면 **파워 뷰 통합 기능** 이 활성화되어 있는지 확인합니다.<br /><br /> 이 기능은 기본적으로 비활성화되어 있습니다.|  

## <a name="next-steps"></a>다음 단계

[SharePoint에서 보고서 서버 및 파워 뷰 통합 사이트 모음 기능 활성화](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Reporting Services 사이트 설정 및 사이트 기능&#40;SharePoint 모드&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[SharePoint 중앙 관리에서 보고서 서버 파일 동기화 기능 활성화](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
