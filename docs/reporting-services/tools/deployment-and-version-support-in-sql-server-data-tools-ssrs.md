---
title: "배포 및 SQL Server Data Tools (SSRS)의 버전 지원 | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 36f5686d-7e40-4f31-be81-bd197ca33a02
caps.latest.revision: 19
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 29df783121de48e39d824b9b9e9666d764717ebc
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="deployment-and-version-support-in-sql-server-data-tools-ssrs"></a>SQL Server Data Tools의 배포 및 버전 지원(SSRS)
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 는 다음과 같은 시나리오를 지원합니다.  
  
-   보고서 정의(*.rdl) 및 보고서 서버 프로젝트(\*.rptproj) 열기  
  
-   보고서 정의 작성  
  
-   보고서 디자이너에서 보고서 미리 보기  
  
-   보고서 서버에 보고서 배포  
  
##  <a name="bkmk_ConfigurationandDeploymentProperties"></a> 구성 및 배포 속성  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서는 프로젝트 구성이 지원됩니다. 프로젝트 구성은 보고서를 미리 보거나 배포하는 단계로 프로젝트가 빌드될 때 위치와 동작을 지정하는 속성 집합으로 구성됩니다. 프로젝트 구성에 대한 자세한 내용은 Visual Studio 설명서를 참조하세요.  
  
 프로젝트 구성을 사용하면 보고서 정의를 대상 보고서 서버 호환 스키마 버전으로 업그레이드하는 작업을 제어할 수 있습니다. 프로젝트 구성으로 제어되는 속성에는 대상 보고서 서버, 오류 수준, 빌드 프로세스에서 미리 보기 및 배포용으로 보고서 정의를 임시 저장하는 폴더 등이 포함됩니다.  
  
 보고서는 보고서 디자이너에서 미리 보기로 렌더링되거나 보고서 서버에 배포되기 전에 빌드됩니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] **프로젝트 속성** 대화 상자에서 구성 속성을 설정합니다.  
  
 빌드 및 배포 속성에는 다음이 포함됩니다.  
  
-   OutputPath는 보고서의 빌드 확인, 배포 및 미리 보기에 사용되는 보고서 정의를 저장할 폴더의 경로를 식별하는 빌드 속성입니다.  
  
-   ErrorLevel은 오류로 보고되는 빌드 문제의 심각도를 식별하는 빌드 속성입니다. ErrorLevel 값보다 작거나 같은 심각도 수준을 가진 문제는 오류로 보고되고 그렇지 않은 문제는 경고로 보고됩니다. 자세한 내용은의 "보고서 유효성 검사 및 오류 수준" 섹션을 참조 하십시오. [보고서 디자이너 &#40; 보고서 디자인 Ssrs&#41; ](../../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
-   TargetServerVersion의 예상된 버전을 식별 하는 배포 속성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] TargetServerURL 속성에 지정 된 대상 보고서 서버에 설치 된 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 대화 상자에서 이전 버전의 **프로젝트 속성** 를 지정할 경우 보고서는 이전 버전으로 자동으로 되돌아가지 않습니다. 마찬가지로 보고서 서버 프로젝트는 두 가지 다른 버전인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]보고서를 포함할 수 있습니다. 보고서 서버 프로젝트가 배포될 경우 프로젝트의 모든 보고서는 TargetServerVersion에 지정된 버전으로 변환됩니다.  
  
 둘 이상의 프로젝트 구성을 프로젝트에 추가할 수 있으며 각 구성은 다른 버전의 보고서 서버에 배포하는 것과 같은 다양한 시나리오에 사용됩니다. 자세한 내용은 [배포 속성 설정&#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md) 및 [프로젝트 속성 페이지 대화 상자](../../reporting-services/tools/project-property-pages-dialog-box.md)를 참조하세요.  
  
##  <a name="bkmk_SupportedVersions"></a> Supported Versions  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]보고서 서버 프로젝트를 위한 32 비트 개발 환경에서 실행 하도록 설계 되지 않았습니다 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]-기반 컴퓨터에 설치 되지 않은 및 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]-기반 서버. x64 기반 컴퓨터에서는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 가 지원됩니다.  
  
 다음 표에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 보고서를 작성 및 게시할 때 지원되는 버전을 설명합니다.  
  
> [!NOTE]  
>  스키마는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]이후 변경되지 않았습니다.  
  
|프로젝트 또는 파일 유형|버전|보고서 작성|보고서 게시|참고|  
|--------------------------|-------------|--------------------|---------------------|-----------|  
|보고서 서버 프로젝트<br /><br /> 또는<br /><br /> 보고서 서버 마법사 프로젝트|[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]|2016 RDL 스키마|[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]||  
|보고서 서버 프로젝트<br /><br /> 또는<br /><br /> 보고서 서버 마법사 프로젝트|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|2014 RDL 스키마|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|보고서 서버 프로젝트<br /><br /> 또는<br /><br /> 보고서 서버 마법사 프로젝트|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|2012 RDL 스키마|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|보고서 서버 프로젝트<br /><br /> 또는<br /><br /> 보고서 서버 마법사 프로젝트|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|2008 R2 RDL 스키마|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|보고서 서버 프로젝트<br /><br /> 또는<br /><br /> 보고서 서버 마법사 프로젝트|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|2008 RDL 스키마|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버만|2003 RDL 및 2005 RDL을 2008 RDL 스키마로 로컬 업그레이드합니다.|  
  
 이전 버전의 보고서 정의 스키마에서 보고서를 여는 방법에 대한 자세한 내용은 [업그레이드 보고서](../../reporting-services/install-windows/upgrade-reports.md)를 참조하세요. 특정 보고서 정의 스키마에 대한 자세한 내용은 [Report Definition Language 사양(Report Definition Language Specification)](http://go.microsoft.com/fwlink/?linkid=116865)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 원본 및 보고서 게시](../../reporting-services/reports/publishing-data-sources-and-reports.md)  
  
  
