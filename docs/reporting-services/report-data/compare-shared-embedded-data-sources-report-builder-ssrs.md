---
title: 공유 및 포함된 데이터 원본 비교 - 보고서 작성기 및 Reporting Services(SSRS) | Microsoft Docs
ms.date: 11/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5ae21994a83659204f6a5053288ff632ce44be06
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74196785"
---
# <a name="compare-shared-and-embedded-data-sources---report-builder--reporting-services-ssrs"></a>공유 및 포함된 데이터 원본 비교 - 보고서 작성기 및 Reporting Services(SSRS)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]
 
공유 또는 포함된 데이터 원본을 데이터에 연결할 수 있습니다. *공유 데이터 원본*은 보고서와 별개로 정의됩니다. 보고서 서버 또는 SharePoint 사이트의 여러 보고서에서 이를 사용할 수 있습니다. *포함된 데이터 원본*은 보고서에 정의되어 있으며 해당 보고서에만 사용할 수 있습니다. 

 공유 데이터 원본은 자주 사용하는 데이터 원본이 있는 경우에 유용합니다. 가능한 한 공유 데이터 원본을 만들고 사용하는 것이 좋습니다. 공유 데이터 원본을 사용하면 보고서 및 보고서 액세스 관리가 더 쉬울 뿐만 아니라 보고서 및 보고서에서 액세스하는 데이터 원본을 보다 안전하게 유지할 수 있습니다. 공유 데이터 원본이 필요한 경우에는 공유 데이터 원본을 만들어 주도록 시스템 관리자에게 요청해야 할 수 있습니다.  
  
 *보고서별 데이터 원본*으로도 알려진 포함된 데이터 원본은 보고서 정의에 저장되는 데이터 연결입니다. 포함된 데이터 원본 연결 정보는 해당 정보가 포함된 보고서에서만 사용될 수 있습니다. 포함된 데이터 원본을 정의하고 관리하려면 보고서의 **데이터 원본 속성** 대화 상자를 사용합니다.  
  
 포함된 데이터 원본과 공유 데이터 원본은 작성, 저장 및 관리되는 방법이 다릅니다.  
  
-   보고서 디자이너에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 프로젝트의 일부분으로 포함된 데이터 원본 또는 공유 데이터 원본을 만듭니다. 이러한 데이터 원본을 미리 보기용으로 로컬에서 사용할지 아니면 프로젝트의 일부분으로 보고서 서버 또는 SharePoint 사이트에 배포할지를 제어할 수 있습니다. 보고서를 배포하는 보고서 서버 또는 SharePoint 사이트와 사용 중인 컴퓨터에 설치한 사용자 지정 데이터 확장 프로그램을 사용할 수 있습니다.  
  
     시스템 관리자는 추가적인 데이터 처리 확장 프로그램 및 .NET Framework 데이터 공급자를 설치하고 구성할 수 있습니다. 자세한 내용은 [데이터 처리 확장 프로그램과 .NET Framework 데이터 공급자&#40;SSRS&#41;](../../reporting-services/report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)를 참조하세요.  
  
     개발자는 <xref:Microsoft.ReportingServices.DataProcessing> API를 사용하여 다른 유형의 데이터 원본을 지원하는 데이터 처리 확장을 만들 수 있습니다.  
  
-   [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]에서 보고서 서버 또는 SharePoint 사이트를 찾은 다음 보고서에서 포함된 데이터 원본을 만들거나 공유 데이터 원본을 선택합니다. [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]에서는 공유 데이터 원본을 만들 수 없습니다. 또한 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]에서는 사용자 지정 데이터 확장 프로그램을 사용할 수 없습니다.  

## <a name="summary-of-differences"></a>차이점 요약
  
 다음 표에는 포함된 데이터 원본과 공유 데이터 원본의 차이점이 요약되어 있습니다.  
  
|Description|포함된<br /><br /> 데이터 원본|공유됨<br /><br /> 데이터 원본|  
|-----------------|------------------------------|----------------------------|  
|데이터 연결이 보고서 정의에 포함되어 있습니다.|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")||  
|보고서 서버의 데이터 연결에 대한 포인터가 보고서 정의에 포함되어 있습니다.||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|  
|보고서 서버에서 관리됩니다.|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|  
|공유 데이터 세트에 필요합니다.||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|  
|구성 요소에 필요합니다.||![사용 가능](../../reporting-services/report-data/media/greencheck.gif "사용 가능")|  

## <a name="next-steps"></a>다음 단계

[공유 데이터 원본 만들기 및 관리](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
[포함된 데이터 원본 만들기 및 수정](../../reporting-services/report-data/create-and-modify-embedded-data-sources.md)   
[배포 속성 설정](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
[보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
