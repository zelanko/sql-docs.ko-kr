---
title: "보고서 데이터 원본 관리 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], data
- published reports [Reporting Services], data source connections
- shared data sources [Reporting Services]
- data sources [Reporting Services], managing
ms.assetid: 0475aded-c8fe-4337-a2b5-4df0ec4c46af
caps.latest.revision: "52"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 443b1f6a2249fd836555bb7cb6822d3dbbae199d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="manage-report-data-sources"></a>보고서 데이터 원본 관리
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 보고서, 보고서 모델 및 데이터 기반 구독은 외부 데이터 원본에서 데이터를 검색합니다. 보고서 서버는 외부 데이터 원본에 연결하기 위해 보고서, 모델 또는 구독에 정의되어 있거나 참조된 데이터 원본 연결 정보를 사용합니다. 데이터 원본 연결 속성은 보고서 또는 모델을 만들 때 항상 함께 정의되지만 보고서 또는 모델이 보고서 서버에 게시된 후에 독립적으로 관리할 수 있습니다.  
  
 보고서 데이터 원본은 기본 모드 보고서 서버에 대한 보고서 관리자를 사용하거나 보고서 서버를 SharaPoint 통합 모드로 배포한 경우 SharePoint 사이트의 응용 프로그램 페이지를 사용하여 관리할 수 있습니다.  
  
 데이터 원본 연결 관리는 다음과 같은 태스크를 특징으로 하며 이 항목에서는 이러한 특징에 대해 설명합니다.  
  
-   연결 문자열 변경  
  
-   자격 증명 변경  
  
-   보고서 서버에서 공유 데이터 원본 만들기 및 사용(공유 데이터 원본에 대해 포함된 데이터 원본 전환 포함)  
  
-   사용 중인 보고서, 모델 또는 공유 데이터 원본에 사용 권한을 설정하여 데이터 원본 속성에 대한 액세스 제어  
  
 쿼리 수정은 데이터 원본 연결 관리에 속하지 않습니다. 보고서 또는 모델에 대한 쿼리를 수정하려면 제작 도구를 사용해야 하며 보고서 또는 모델 정의에서 변경을 수행해야 합니다.  
  
## <a name="managed-properties-data-source-type-connection-strings-and-credentials"></a>관리되는 속성: 데이터 원본 유형, 연결 문자열 및 자격 증명  
 보고서 서버에서 관리할 수 있는 데이터 원본 속성은 다음과 같습니다.  
  
|속성|Description|관리 방법|  
|--------------|-----------------|----------------------|  
|데이터 원본 유형|보고서 서버의 데이터 처리 확장 프로그램에 따라 지원되는 데이터 원본 유형이 달라집니다. 데이터 프로세서의 예로는 SQL Server, Analysis Services, Oracle 등이 있습니다.|데이터 원본 유형은 구성 가능하므로 관리되는 속성입니다. 그러나 새 공유 데이터 원본을 만들 경우에만 데이터 원본 유형을 구성해야 합니다.<br /><br /> 게시된 보고서 또는 모델의 속성 페이지에서 데이터 원본 유형을 변경하지 마십시오. 변경할 경우 거의 항상 연결이 무효화됩니다. 보고서 또는 모델에 필요한 데이터 구조가 다른 데이터 플랫폼에서도 동일할 가능성은 희박합니다.|  
|연결 문자열|외부 데이터 원본에 대한 초기 연결을 설정합니다. 보고서는 정적 또는 동적 연결 문자열을 사용할 수 있습니다.<br /><br /> *정적 연결 문자열* 은 보고서가 실행될 때마다 동일한 데이터 원본에 연결하기 위해 보고서에서 항상 사용하는 값 집합입니다.<br /><br /> *동적 연결 문자열* 은 보고서에 만들어 넣는 식으로, 사용자가 런타임에 사용할 데이터 원본을 선택할 수 있도록 합니다. 보고서 디자이너에서 보고서를 만들 경우 식과 데이터 원본 선택 목록을 작성하여 보고서에 넣어야 합니다.|연결 문자열 변경은 데이터 원본을 다른 컴퓨터로 이동하는 경우 또는 테스트 데이터를 사용하여 보고서를 만들었으나 프로덕션 데이터베이스로 보고서를 배포하려는 경우 유용합니다.<br /><br /> 정적 연결 문자열은 원본 문자열을 다른 문자열로 대체하여 관리할 수 있습니다.<br /><br /> 보고서 관리자 또는 SharePoint 사이트에서 동적 연결 문자열을 관리하는 경우 정적 연결 문자열로 대체하는 방법만 사용할 수 있습니다. 식 자체를 편집하거나 데이터 원본 선택 목록을 변경할 수 없습니다. 식 또는 유효한 값 목록을 변경하려면 보고서 정의를 편집하여 보고서 서버에 다시 게시해야 합니다. 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)을 참조하세요.|  
|자격 증명|데이터 원본의 데이터를 읽을 권한이 있는 사용자의 이름과 암호를 제공합니다.<br /><br /> 데이터 원본에서 인증을 지원하지 않는 경우(예: 데이터 원본이 파일 시스템의 XML 파일인 경우) 무인 실행 계정을 구성하여 보고서 서버가 자격 증명을 전달하지 않고 외부 데이터 원본에 연결하도록 허용할 수 있습니다.|사용자 계정 또는 암호가 만료된 경우 이를 업데이트하여 자격 증명을 관리할 수 있습니다.<br /><br /> 또한 자격 증명을 가져오는 방법을 변경할 수도 있습니다(예: 런타임에 사용자에게 자격 증명을 입력하도록 요청).<br /><br /> 사용자가 보고서를 구독할 수 있도록 하려면 저장된 자격 증명을 사용하도록 보고서를 구성해야 합니다.|  
  
## <a name="creating-and-using-shared-data-sources"></a>공유 데이터 원본 만들기 및 사용  
 보고서에 데이터 원본 속성을 포함하여 보고서를 게시하는 경우 공유 데이터 원본 속성으로 전환하는 것을 고려하십시오. 공유 데이터 원본의 경우 자격 증명과 연결 문자열을 한 페이지에서 업데이트할 수 있으므로 관리하기가 더 쉽습니다. 데이터 원본을 사용하는 모든 보고서, 모델 및 데이터 기반 구독은 즉시 변경 내용을 포착합니다. 또한 공유 데이터 원본을 오프라인 상태로 만들어 보고서 또는 구독을 일시 중지함으로써 문제를 해결하거나 조사할 동안 실행을 차단할 수 있습니다.  
  
## <a name="controlling-access-data-source-properties"></a>데이터 원본 속성 액세스 제어  
 기본적으로 보고서 관리 권한을 가진 모든 사용자는 데이터 원본 유형, 연결 문자열, 자격 증명, 그리고 포함된 데이터 원본과 공유 데이터 원본 중 보고서가 연결 정보를 받을 대상을 결정하는 속성을 포함한 모든 속성을 설정할 수 있습니다. 기본 모드 보고서 서버의 데이터 원본 속성에 대한 액세스를 제어하는 태스크 및 사용 권한에 대한 자세한 내용은 [공유 데이터 원본 항목 보안 설정](../../reporting-services/security/secure-shared-data-source-items.md) 및 [보고서 및 리소스 보안](../../reporting-services/security/secure-reports-and-resources.md)을 참조하세요.  
  
 SharePoint 라이브러리의 항목에 대한 속성을 보고 편집할 수 있는 권한은 사이트 관리자에 의해 결정됩니다. 데이터 원본 연결 속성에 대한 액세스를 제어하는 사용 권한에 대한 자세한 내용은 [보고서 서버 항목에 대한 SharePoint 사이트 및 목록 사용 권한 참조](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)를 참조하세요.  
  
## <a name="how-to-work-with-data-source-properties-on-a-report-server"></a>보고서 서버에서 데이터 원본 속성을 사용하는 방법  
 다양한 도구를 사용하여 데이터 원본 속성을 만들고 수정할 수 있습니다. 다음 표에서는 접근 방법과 도구를 요약하여 설명하고 추가 지침에 대한 링크를 제공합니다.  
  
|태스크|도구|링크|  
|----------|----------|----------|  
|연결 문자열의 예를 봅니다.||[데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)|  
|데이터 원본에 연결하기 위한 자격 증명을 가져오는 방법을 선택합니다.||[보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)|  
|보고서 정의(.rdl) 파일에 데이터 원본 연결 속성을 추가합니다.|보고서 디자이너|[포함된 데이터 원본 또는 공유 데이터 원본 만들기&#40;SSRS&#41;](http://msdn.microsoft.com/library/b111a8d0-a60d-4c8b-b00a-51644b19c34b)|  
|보고서 프로젝트의 공유 데이터 원본(.rds) 파일을 추가하고 연결합니다.|보고서 디자이너|[공유 데이터 원본 만들기, 수정 및 삭제&#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)|  
|사용자가 런타임에 선택할 수 있는 미리 정의된 데이터 원본 목록을 만듭니다. 사용자가 보고서를 요청하면 보고서는 데이터 원본 목록을 제공합니다. 사용자는 보고서를 실행하기 전에 사용할 데이터 원본을 선택해야 합니다. 보고서에 데이터 원본 선택 목록을 추가하려면 식을 사용합니다.<br /><br /> 이를 동적 데이터 원본 연결이라고 합니다.|보고서 디자이너|[데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)|  
|보고서 서버에 공유 데이터 원본 항목을 만듭니다.|보고서 관리자|[공유 데이터 원본 만들기, 삭제 또는 수정&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)|  
|자격 증명을 구독 또는 보고서 스냅숏을 만들기 위한 선행 조건으로 저장합니다.|보고서 관리자|[Reporting Services 데이터 원본에 자격 증명 저장](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)|  
|게시된 보고서의 데이터 원본 연결 속성을 편집합니다.|보고서 관리자|[보고서의 데이터 원본 속성 구성&#40;보고서 관리자&#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)|  
|보고서 서버에 공유 데이터 원본 항목을 만듭니다.|SharePoint 사이트|[공유 데이터 원본 만들기 및 관리&#40;SharePoint 통합 모드의 Reporting Services&#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)|  
|보고서에 기존 .odc 연결 정보를 사용합니다.|SharePoint 사이트|[보고서에 Office 데이터 연결&#40;.odc&#41; 사용&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-data/use-an-office-data-connection-odc-with-reports.md)|  
  
> [!NOTE]  
>  보고서 데이터 원본에 대한 데이터 원본 연결 관리는 보고서 서버 데이터베이스에 대한 보고서 서버 연결 관리와는 다릅니다. 내부 데이터 저장소로의 보고서 서버 연결에 대한 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 또는 모델을 공유 데이터 원본에 바인딩&#40;SSRS&#41;](../../reporting-services/report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [공유 데이터 원본 만들기, 삭제 또는 수정&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Reporting Services 데이터 원본에 자격 증명 저장](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)   
 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)   
 [보고서 서버 콘텐츠 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
