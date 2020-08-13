---
title: RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정 | Microsoft Docs
description: RSReportServer 구성 파일에서 렌더링 확장 프로그램 매개 변수를 지정하여 Reporting Services 보고서의 기본 보고서 렌더링 동작을 재정의합니다.
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- configuration options [Reporting Services]
- DeviceInfo settings
- rendering extensions [Reporting Services], overriding behaviors
- parameters [Reporting Services], report rendering
- overriding report rendering behavior
- extensions [Reporting Services], rendering
ms.assetid: 3bf7ab2b-70bb-41c8-acda-227994d15aed
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ae82af83d1933e204e405995864c9f17cfe3521a
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242493"
---
# <a name="customize-rendering-extension-parameters-in-rsreportserverconfig"></a>RSReportServer.Config의 렌더링 확장 프로그램 매개 변수 사용자 지정
  RSReportServer 구성 파일에서 렌더링 확장 프로그램 매개 변수를 지정하여 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 서버에서 실행되는 보고서의 기본 보고서 렌더링 동작을 재정의할 수 있습니다. 다음과 같은 목적으로 렌더링 확장 프로그램 매개 변수를 수정할 수 있습니다.  
  
-   보고서 도구 모음의 내보내기 목록에 렌더링 확장 프로그램 이름이 표시되는 방식을 변경하거나(예: "웹 보관 파일"을 "MHTML"로 변경) 이 이름을 기본 언어로 지역화합니다.  
  
-   같은 렌더링 확장 프로그램의 여러 인스턴스를 만들어 각기 다른 보고서 표시 옵션(예: 이미지 렌더링 확장 프로그램의 세로 및 가로 모드 버전)을 지원합니다.  
  
-   기본 렌더링 확장 프로그램 매개 변수를 다른 값으로 변경합니다. 예를 들어 이미지 렌더링 확장 프로그램에서 TIFF를 기본 출력 형식으로 사용하는 경우 EMF를 대신 사용하도록 확장 프로그램 매개 변수를 수정할 수 있습니다.  
  
 렌더링 확장 프로그램 매개 변수를 변경하면 보고서 서버의 렌더링 작업에만 영향이 미칩니다. 보고서 디자이너의 보고서 미리 보기에서는 렌더링 확장 프로그램 설정을 재정의할 수 없습니다.  
  
 구성 파일에서 렌더링 확장 프로그램 매개 변수를 지정하면 렌더링 확장 프로그램에 전체적으로 영향이 미칩니다. 특정 렌더링 확장 프로그램을 사용하는 경우 구성 파일의 설정이 기본값 대신 사용됩니다. 특정 보고서 또는 렌더링 작업에 대한 렌더링 확장 프로그램 매개 변수를 설정하려면 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 메서드를 사용하여 프로그래밍 방식으로 또는 보고서 URL에 디바이스 정보 설정을 지정하여 디바이스 정보를 지정해야 합니다. 렌더링 작업에 대한 디바이스 정보 설정을 지정하고 전체 디바이스 정보 설정 목록을 보는 방법에 대한 자세한 내용은 [디바이스 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)을 참조하세요.  
  
## <a name="finding-and-modifying-rsreportserverconfig"></a>RSReportServer.config 찾기 및 수정  
 보고서 출력 형식에 대한 구성 설정은 RSReportServer.config 파일에서 렌더링 확장 프로그램 매개 변수로 지정됩니다. 구성 파일에서 렌더링 확장 프로그램 매개 변수를 지정하려면 렌더링 매개 변수를 설정하는 XML 구조의 정의 방법을 알고 있어야 합니다. 다음 두 가지 XML 구조를 수정할 수 있습니다.  
  
-   **OverrideNames** 요소는 렌더링 확장 프로그램의 표시 이름과 언어를 정의합니다.  
  
-   **DeviceInfo** XML 구조는 렌더링 확장 프로그램에서 사용하는 디바이스 정보 설정을 정의합니다. 대부분의 렌더링 확장 프로그램 매개 변수는 디바이스 정보 설정으로 지정됩니다.  
  
 이 파일은 텍스트 편집기를 사용하여 수정할 수 있습니다. RSReportServer.config 파일은 \Reporting Services\Report Server\Bin 폴더에 있습니다. 구성 파일을 수정하는 방법에 대한 자세한 내용은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)을 참조하세요.  
  
## <a name="changing-the-display-name"></a>표시 이름 변경  
 렌더링 확장 프로그램의 표시 이름은 보고서 도구 모음의 내보내기 목록에 나타납니다. 기본 표시 이름의 예로는 웹 보관 파일, TIFF 파일 및 Acrobat(PDF) 파일이 있습니다. 구성 파일에서 **OverrideNames** 요소를 지정하여 기본 표시 이름을 사용자 지정 값으로 바꿀 수 있습니다. 또한 단일 렌더링 확장 프로그램의 인스턴스를 두 개 정의하는 경우 **OverrideNames** 요소를 사용하여 내보내기 목록의 각 인스턴스를 구별할 수 있습니다.  
  
 표시 이름은 지역화되므로 기본 표시 이름을 사용자 지정 값으로 바꿀 경우 **Language** 특성을 설정해야 합니다. 그렇지 않으면 사용자가 지정한 이름이 모두 무시됩니다. 설정하는 언어 값은 보고서 서버 컴퓨터에 유효한 값이어야 합니다. 예를 들어 보고서 서버가 프랑스어 운영 체제에서 실행되고 있으면 "fr-FR"을 특성 값으로 지정해야 합니다.  
  
 다음 예에서는 영어 버전 보고서 서버에 사용자 지정 이름을 제공하는 방법을 보여 줍니다.  
  
```  
<Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering">  
   <OverrideNames>  
     <Name Language="en-US">My Custom Display Name for XML Rendering</Name>  
   </OverrideNames>  
</Extension>  
```  
  
## <a name="changing-device-information-settings"></a>디바이스 정보 설정 변경  
 보고서 서버에 이미 배포된 렌더링 확장 프로그램에서 사용하는 기본 디바이스 정보 설정을 수정하려면 **DeviceInfo** XML 구조를 구성 파일에 입력해야 합니다. 각 렌더링 확장 프로그램은 해당 확장 프로그램에 고유한 디바이스 정보 설정을 지원합니다. 디바이스 정보 설정의 전체 목록을 보려면 [디바이스 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)을 참조하세요.  
  
 다음 예에서는 이미지 렌더링 확장 프로그램의 기본 설정을 수정하는 XML 구조와 구문을 보여 줍니다.  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">Image (EMF)</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <ColorDepth>32</ColorDepth>  
                <DpiX>300</DpiX>  
                <DpiY>300</DpiY>  
                <OutputFormat>EMF</OutputFormat>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="configuring-multiple-entries-for-a-rendering-extension"></a>렌더링 확장 프로그램에 대해 여러 개의 항목 구성  
 같은 렌더링 확장 프로그램의 인스턴스를 여러 개 만들어 각기 다른 보고서 표시 옵션을 지원할 수 있습니다. 정의한 인스턴스마다 여러 매개 변수 값 조합을 가질 수 있습니다. 기존 렌더링 확장 프로그램의 새 인스턴스를 정의할 때는 다음을 수행해야 합니다.  
  
-   확장 프로그램에 고유 이름을 지정합니다.  
  
     인스턴스마다 **Name** 특성에 대한 고유 값이 있어야 합니다. 다음 예에서는 "IMAGE (EMF Landscape)" 및 "IMAGE (EMF Portrait)"라는 이름을 사용하여 두 인스턴스를 구별합니다.  
  
     이미 배포된 렌더링 확장 프로그램의 이름을 변경하는 경우에는 주의하십시오. 프로그래밍 방식으로 렌더링 확장 프로그램을 지정하는 개발자는 이 확장 프로그램 이름을 사용하여 특정 렌더링 작업에 사용할 인스턴스를 식별합니다. 보고서 서버에서 사용자 지정 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 애플리케이션을 실행하고 있는 경우 개발자는 사용자가 기존 확장 프로그램 이름을 수정하거나 새 확장 프로그램 이름을 추가할 경우 이를 알고 있어야 합니다.  
  
-   사용자가 각 출력 형식의 차이를 이해할 수 있도록 고유한 표시 이름을 지정합니다.  
  
     같은 확장 프로그램의 여러 버전을 구성하는 경우에는 **OverrideNames**에 값을 제공하여 각 버전에 고유한 이름을 지정할 수 있습니다. 그렇지 않으면 확장 프로그램의 모든 버전이 보고서 도구 모음의 내보내기 옵션 목록에 같은 이름으로 나타납니다.  
  
 다음 예에서는 TIFF 출력을 생성하는 기본 이미지 렌더링 확장 프로그램을 사용하여 보고서를 세로 모드에서 EMF를 출력하고 동시에 두 번째 인스턴스에서는 가로 모드에서 EMF로 출력하는 방법을 보여 줍니다. 각 확장 프로그램 이름은 고유합니다. 이 예를 테스트하려면 표시/숨기기 옵션, 행렬 또는 드릴스루 링크와 같은 대화형 기능이 포함되지 않은 보고서를 선택하십시오. 대화형 기능은 이미지 렌더링 확장 프로그램에서 작동하지 않습니다.  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF Landscape)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Landscape Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>8.5in</PageHeight>  
                <PageWidth>11in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
    <Extension Name="IMAGE (EMF Portrait)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Portait Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>11in</PageHeight>  
                <PageWidth>8.5in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="see-also"></a>참고 항목  
 [RSReportServer 구성 파일](../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [RSReportDesigner 구성 파일](../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [CSV 디바이스 정보 설정](../reporting-services/csv-device-information-settings.md)   
 [Excel 디바이스 정보 설정](../reporting-services/excel-device-information-settings.md)   
 [HTML 디바이스 정보 설정](../reporting-services/html-device-information-settings.md)   
 [이미지 디바이스 정보 설정](../reporting-services/image-device-information-settings.md)   
 [MHTML 디바이스 정보 설정](../reporting-services/mhtml-device-information-settings.md)   
 [PDF 디바이스 정보 설정](../reporting-services/pdf-device-information-settings.md)   
 [XML 디바이스 정보 설정](../reporting-services/xml-device-information-settings.md)  
  
  
