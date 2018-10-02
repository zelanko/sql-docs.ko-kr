---
title: IRenderingExtension 인터페이스 구현 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- IRenderingExtension interface
- rendering extensions [Reporting Services], IRenderingExtension interface
ms.assetid: 74b2f2b7-6796-42da-ab7d-b05891ad4001
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 594c1bf8f27e3ff48164368a2827238cad4fdd5c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47803221"
---
# <a name="implementing-the-irenderingextension-interface"></a>IRenderingExtension 인터페이스 구현
  렌더링 확장 프로그램은 실제 데이터와 결합된 보고서 정의에서 결과를 가져오고 결과 데이터를 사용 가능한 형식으로 렌더링합니다. 결합된 데이터의 변환과 형식 지정은 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension>을 구현하는 CLR(공용 언어 런타임) 클래스를 사용하여 수행됩니다. 이것은 개체 모델을 뷰어, 프린터 또는 기타 출력 대상에서 사용할 수 있는 출력 형식으로 변환합니다.  
  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension>에는 코딩해야 하는 메서드가 세 개 있습니다.  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> - 보고서를 렌더링합니다.  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> - 보고서에서 특정 스트림을 렌더링합니다.  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> - 보고서에 필요한 추가 정보(예: 아이콘)를 가져옵니다.  
  
 다음 섹션에서는 이러한 메서드에 대해 자세히 설명합니다.  
  
## <a name="render-method"></a>Render 메서드  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> 메서드에는 다음 개체를 나타내는 인수가 포함됩니다.  
  
-   렌더링할 *보고서* 자체. 이 개체에는 보고서에 대한 속성, 데이터 및 레이아웃 정보가 포함됩니다. 보고서는 보고서 개체 모델 트리의 루트입니다.  
  
-   보고서 서버에 대한 매개 변수(있는 경우)와 함께 문자열 사전 개체를 포함하는 *ServerParameters*.  
  
-   장치 설정을 포함하는 *deviceInfo* 매개 변수. 자세한 내용은 [장치 정보 설정을 렌더링 확장 프로그램에 전달](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)을 참조하세요.  
  
-   렌더링하는 클라이언트에 대한 정보가 들어 있는 <xref:System.Collections.Specialized.NameValueCollection> 사전 개체를 포함하는 *clientCapabilities* 매개 변수.  
  
-   렌더링 결과에 대한 정보가 들어 있는 *RenderProperties*.  
  
-   *createAndRegisterStream*은 렌더링할 스트림을 가져오기 위해 호출되는 대리자 함수입니다.  
  
### <a name="deviceinfo-parameter"></a>deviceInfo 매개 변수  
 *deviceInfo* 매개 변수에는 보고서 매개 변수가 아니라 렌더링 매개 변수가 포함됩니다. 이러한 렌더링 매개 변수는 렌더링 확장 프로그램에 전달됩니다. *deviceInfo* 값은 보고서 서버에서 <xref:System.Collections.Specialized.NameValueCollection> 개체로 변환됩니다. *deviceInfo* 매개 변수의 항목은 대소문자를 구분하지 않는 값으로 처리됩니다. 렌더링 요청이 URL 액세스 결과로 이루어진 경우 `rc:key=value` 형식의 URL 매개 변수가 *deviceInfo* 사전 개체의 키/값 쌍으로 변환됩니다. 브라우저 감지 코드는 *clientCapabilities* 사전에 EcmaScriptVersion, JavaScript, MajorVersion, MinorVersion, Win32, Type 및 AcceptLanguage 항목을 제공합니다. 렌더링 확장 프로그램에서 인식할 수 없는 *deviceInfo* 매개 변수의 이름/값 쌍은 무시됩니다. 다음 코드 예제는 아이콘을 검색하는 예제 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 메서드를 보여 줍니다.  
  
```csharp  
public void GetRenderingResource (CreateStream createStreamCallback, NameValueCollection deviceInfo)  
{  
    string[] iconTagValues = deviceInfo.GetValues("Icon");  
    if ((iconTagValues != null) && (iconTagValues.Length > 0) )  
    {  
        // Create a stream to output to.  
        Stream outputStream = createStreamCallback(m_iconResourceName, "gif", null, "image/gif", false);  
        // Get the GIF image for one of the buttons on the toolbar  
        Image requiredImage = (Image) m_resourcemanager.GetObject(m_iconResourceName  
        // Write the image to the output stream  
        requiredImage.Save(outputStream, requiredImage.RawFormat);  
    }  
    return;  
}  
```  
  
## <a name="renderstream-method"></a>RenderStream 메서드  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> 메서드는 보고서에서 특정 스트림을 렌더링합니다. 모든 스트림은 최초 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> 호출 중에 만들어지지만, 이 스트림이 처음에 클라이언트에 반환되지는 않습니다. 이 메서드는 보조 스트림(예: HTML 렌더링의 이미지) 또는 다중 페이지 렌더링 확장 프로그램의 추가 페이지(예: 이미지/EMF)에 사용됩니다.  
  
## <a name="getrenderingresource-method"></a>GetRenderingResource 메서드  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 메서드는 보고서의 전체 렌더링을 실행하지 않고 정보를 검색합니다. 보고서에서 보고서 자체가 렌더링되지 않아도 되는 정보가 필요할 때가 있습니다. 예를 들어 렌더링 확장 프로그램과 연결된 아이콘이 필요한 경우 단일 태그 **\<Icon>** 을 포함하는 *deviceInfo* 매개 변수를 사용합니다. 이러한 경우 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 메서드를 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [렌더링 확장 프로그램 구현](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [렌더링 확장 프로그램 개요](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
  
  
