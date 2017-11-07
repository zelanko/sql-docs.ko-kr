---
title: "Power Pivot 서버 관리 및 중앙 관리의 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2cdbfdc5-45a9-4000-a03d-318cc7ac8fe9
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3dd5476281506f84282fb8b6b6a534820ebea078
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="power-pivot-server-administration-and-configuration-in-central-administration"></a>중앙 관리에서 파워 피벗 서버 관리 및 구성
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 서버 관리 및 구성을 수행합니다.  
  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 은 먼저 구성해야 사용할 수 있습니다. SharePoint용 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 은 SQL Server 설치 프로그램을 사용하여 설치한 후 다음 중 원하는 방식으로 구성할 수 있습니다.  
  
-   [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 구성 도구 또는 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint 2013 구성 도구  
  
-   SharePoint 중앙 관리  
  
-   PowerShell cmdlet  
  
 세 방법 모두 서버를 완벽하게 구성합니다.  
  
 이 섹션에는 중앙 관리를 사용하여 소프트웨어를 구성하는 태스크가 포함됩니다. 최소한 아래 목록에 있는 세 가지 필수 구성 태스크를 모두 수행해야 합니다.  
  
> [!IMPORTANT]  
>  SharePoint 2010의 경우 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 데이터베이스 서버를 사용하는 SharePoint 팜이나 SharePoint용 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 을 구성하려면 먼저 SharePoint 2010 SP1(서비스 팩 1)을 설치해야 합니다. 서비스 팩을 아직 설치하지 않았으면 서버를 구성하기 전에 지금 설치합니다.  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-central-administration"></a>중앙 관리를 사용하여 SharePoint용 PowerPivot을 구성할 때의 이점  
 SharePoint 중앙 관리는 SharePoint 팜 관리 응용 프로그램입니다. 팜 관리자라면 SharePoint용 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 인스턴스를 팜에 추가할 때 익숙한 도구를 사용하려고 할 것입니다.  
  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 구성 도구 또는 PowerShell cmdlet과 달리 중앙 관리에서는 응용 프로그램 또는 서버를 구성할 때 설정할 수 있는 모든 옵션을 완전히 지정하는 페이지를 제공합니다. 다른 방법에서는 구성 워크플로를 몇 개의 단계로 압축하거나 PowerShell을 사용하여 SharePoint 서버를 구성하는 방법을 미리 알고 있어야 합니다.  
  
## <a name="related-content"></a>관련 내용  
 [Windows PowerShell을 사용하여 파워 피벗 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 [파워 피벗 구성 도구](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>관련 작업  
  
|링크|형식|태스크 설명|  
|----------|----------|----------------------|  
|[SharePoint에 PowerPivot 솔루션 배포](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)|필수임|이 단계에서는 팜 및 사이트 모음에 프로그램 파일과 응용 프로그램 페이지를 추가하는 솔루션 파일을 설치합니다.|  
|[중앙 관리에서 PowerPivot 서비스 응용 프로그램 만들기 및 구성](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)|필수임|이 단계에서는 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 시스템 서비스를 프로비전합니다.|  
|[중앙 관리에서 사이트 모음에 대해 파워 피벗 기능 통합 활성화](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)|필수임|이 단계에서는 사이트 모음 수준에서 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 기능을 설정합니다.|  
|[MSOLAP.5를 Excel 서비스에서 신뢰할 수 있는 데이터 공급자로 추가](../../analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|필수임|이 단계에서는 Analysis Services OLE DB 공급자를 Excel 서비스에 신뢰할 수 있는 공급자로 추가합니다.|  
|[SharePoint 2010에서 파워 피벗 데이터 새로 고침](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)|권장|데이터 새로 고침은 선택 사항이지만 사용하는 것이 좋습니다. 게시한 Excel 통합 문서 내의 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 데이터에 대한 무인 업데이트를 예약할 수 있습니다.|  
|[Power Pivot 무인 데이터 새로 고침 계정 구성(SharePoint용 Power Pivot)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)|권장|이 단계에서는 서버에서 데이터 새로 고침 작업을 실행하는 데 사용할 수 있는 특수 용도 계정을 프로비전합니다.|  
|[사용 현황 데이터 수집 구성&#40;SharePoint용 파워 피벗](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|선택 사항|사용 데이터 컬렉션은 기본적으로 구성되어 있습니다. 이 단계를 사용하여 기본 설정을 수정할 수 있습니다.|  
|[전용 데이터 새로 고침 또는 쿼리만 처리 구성(SharePoint용 PowerPivot)](http://msdn.microsoft.com/en-us/5e027605-1086-4941-bb01-f315df8f829b)|선택 사항|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 인스턴스를 데이터 새로 고침 작업 또는 쿼리 전용으로 사용할 수 있습니다. 또한 병렬 데이터 새로 고침 작업에 대한 기본 설정을 수정할 수 있습니다.|  
|[Power Pivot 서비스 계정 구성](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)|선택 사항|암호를 업데이트하거나 서비스 계정을 변경하는 방법에 대해 설명합니다.|  
|[중앙 관리에서 SharePoint 웹 응용 프로그램에 파워 피벗 서비스 응용 프로그램 연결](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|선택 사항|서비스 연결을 수정하는 방법에 대해 설명합니다.|  
|[중앙 관리에서 파워 피벗 사이트에 대한 신뢰할 수 있는 위치 만들기](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|선택 사항|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 갤러리를 신뢰할 수 있는 위치로 추가하는 방법에 대해 설명합니다.|  
|[SharePoint 로그 파일과 진단 로깅 구성 및 보기&#40;SharePoint용 파워 피벗&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)|선택 사항|이벤트 로깅은 기본적으로 구성되어 있습니다. 이 단계를 사용하여 기본 설정을 수정할 수 있습니다.|  
|[PowerPivot 상태 규칙 구성](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md)|선택 사항|서버 상태 규칙은 기본적으로 구성되어 있습니다. 이 단계를 사용하여 일부 기본 설정을 수정할 수 있습니다.|  
|[Power Pivot 갤러리 만들기 및 사용자 지정](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)|선택 사항|수동으로 구성하는 설치에 대해 이 절차에서는 포함된 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 통합 문서의 축소판 이미지를 보여 주는 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 갤러리 라이브러리를 만드는 방법에 대해 설명합니다.|  
|[라이브러리에 BI 의미 체계 모델 연결 콘텐츠 형식 추가&#40;SharePoint용 파워 피벗&#41;](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md)|선택 사항|BI 의미 체계 모델 연결 파일 만들기를 지원하도록 문서 라이브러리를 확장하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SharePoint 2010용 Power Pivot 설치](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)   
 [구성 설정 참조&#40;SharePoint용 파워 피벗&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [SharePoint 용 파워 피벗에 대 한 재해 복구](http://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  

