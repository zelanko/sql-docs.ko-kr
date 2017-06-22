---
title: "IRenderingExtension 인터페이스 구현 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- IRenderingExtension interface
- rendering extensions [Reporting Services], IRenderingExtension interface
ms.assetid: 74b2f2b7-6796-42da-ab7d-b05891ad4001
caps.latest.revision: 43
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3b5772901cfaabedab1b42db39dcd85c49119509
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

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
  
-   *보고서* 를 렌더링 합니다. 이 개체에는 보고서에 대한 속성, 데이터 및 레이아웃 정보가 포함됩니다. 보고서는 보고서 개체 모델 트리의 루트입니다.  
  
-   *ServerParameters* 있는 경우 보고서 서버에 대 한 매개 변수를 사용 하는 문자열 사전 개체를 포함 하는 합니다.  
  
-   *deviceInfo* 장치 설정을 포함 하는 매개 변수입니다. 자세한 내용은 참조 [장치 정보 설정을 렌더링 확장 프로그램에 전달](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)합니다.  
  
-   *clientCapabilities* 매개 변수를 포함 하는 <xref:System.Collections.Specialized.NameValueCollection> 렌더링 하는 클라이언트에 대 한 정보가 포함 된 사전 개체입니다.  
  
-   *RenderProperties* 렌더링 결과 대 한 정보가 들어 있는입니다.  
  
-   *createAndRegisterStream* 렌더링할 스트림을 가져오기 위해 호출 되는 대리자 함수입니다.  
  
### <a name="deviceinfo-parameter"></a>deviceInfo 매개 변수  
 *deviceInfo* 렌더링 매개 변수를 포함 하는 매개 변수, 매개 변수를 보고 하지 않습니다. 이러한 렌더링 매개 변수는 렌더링 확장 프로그램에 전달됩니다. *deviceInfo* 값으로 변환 된는 <xref:System.Collections.Specialized.NameValueCollection> 보고서 서버에서 개체입니다. 항목에 *deviceInfo* 매개 변수는 대/소문자 구분 값으로 처리 됩니다. 렌더링 요청이 액세스 결과로 이루어진 경우 URL, URL 매개 변수 형태로 `rc:key=value` 키/값 쌍으로 변환 된 *deviceInfo* 사전 개체입니다. 브라우저 감지 코드의 다음 항목에 제공 된 *clientCapabilities* 사전: EcmaScriptVersion, JavaScript, MajorVersion, MinorVersion, Win32, 유형 및 acceptlanguage 항목을 제공 합니다. 모든 이름/값 쌍의 *deviceInfo* 렌더링 확장 프로그램에서 인식할 수 없는 매개 변수가 무시 됩니다. 다음 코드 예제는 아이콘을 검색하는 예제 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 메서드를 보여 줍니다.  
  
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
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 메서드는 보고서의 전체 렌더링을 실행하지 않고 정보를 검색합니다. 보고서에서 보고서 자체가 렌더링되지 않아도 되는 정보가 필요할 때가 있습니다. 예를 들어 렌더링 확장 프로그램과 연결 된 아이콘이 필요한 경우 사용 하 여는 *deviceInfo* 단일 태그를 포함 하는 매개 변수  **\<아이콘 >**합니다. 이러한 경우 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> 메서드를 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [렌더링 확장 프로그램 구현](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [렌더링 확장 프로그램 개요](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
  
  
