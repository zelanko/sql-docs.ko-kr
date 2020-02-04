---
title: 디바이스 정보 설정을 렌더링 확장 프로그램에 전달 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- device information settings [Reporting Services]
- Render method
- Report Server Web service, device information settings
- Web service [Reporting Services], device information settings
- XML Web service [Reporting Services], device information settings
- passing device information [Reporting Services]
- rendering extensions [Reporting Services], device information settings
- rendering [Reporting Services], settings
- device information settings [Reporting Services], about device information settings
- extensions [Reporting Services], device information settings
ms.assetid: fe718939-7efe-4c7f-87cb-5f5b09caeff4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4171fcbc01b7dfd36003bef6c4fa5d90c74600d3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63128884"
---
# <a name="passing-device-information-settings-to-rendering-extensions"></a>디바이스 정보 설정을 렌더링 확장 프로그램에 전달
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 디바이스 정보 설정을 사용하여 렌더링 매개 변수를 렌더링 확장 프로그램으로 전달할 수 있습니다. 보고서 서버 웹 서비스의 설정이 **DeviceInfo** XML 요소로 전달되고 보고서 서버에서 처리됩니다. 디바이스 정보 설정은 기본값을 가지므로 렌더링 프로세스에서 선택적 인수로 간주됩니다. 그러나 디바이스 정보 설정을 사용하여 렌더링을 사용자 지정하고 서버에서 공급한 기본값을 무효화할 수 있습니다.  
  
 다양한 방법으로 디바이스 정보 설정을 지정할 수 있습니다. 프로그래밍 방식에서는 Render 메서드를 사용할 수 있습니다. URL을 통해 보고서에 액세스하는 경우 디바이스 정보를 URL 매개 변수로 지정할 수 있습니다. 또한 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 파일에서 디바이스 정보 설정을 편집하여 렌더링 매개 변수를 전역으로 지정할 수 있습니다. 렌더링 매개 변수를 전역으로 지정하는 방법에 대한 자세한 내용은 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수 사용자 지정](../../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)을 참조하세요.  
  
## <a name="passing-device-information-using-the-render-method"></a>Render 메서드를 사용하여 디바이스 정보 전달  
 렌더링 확장 프로그램에 디바이스 정보 설정을 전달하려면 **M:Microsoft.WSSUX.ReportingServicesWebService.RSExecutionService2005.ReportExecutionService.Render(System.String,System.String,System.String@,System.String@,System.String@,Microsoft.WSSUX.ReportingServicesWebService.RSExecutionService2005.Warning[]@,System.String[]@)** 메서드를 사용합니다. 예를 들어, 다음 XML 문자열을 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 메서드로 전달하여 HTML에 렌더링할 때 HTML 조각을 만들 수 있습니다.  
  
```  
<DeviceInfo>  
   <HTMLFragment>True</HTMLFragment>  
</DeviceInfo>  
```  
  
 보고서가 HTML 조각으로 렌더링되면 HTML 또는 BODY 요소를 사용하지 않고 TABLE 요소 안에 보고서의 내용이 포함됩니다. HTML 조각을 사용하여 보고서를 기존 HTML 문서로 통합할 수 있습니다. HTML 출력용 디바이스 정보 설정에 대한 자세한 내용은 [HTML Device Information Settings](../../../reporting-services/html-device-information-settings.md)을 참조하십시오.  
  
## <a name="passing-device-information-using-url-access"></a>URL 액세스를 사용하여 디바이스 정보 전달  
 URL 액세스를 통해서도 디바이스 정보 설정을 전달할 수 있습니다. 디바이스 정보 설정이 URL 매개 변수로 전달됩니다. 다음 URL 액세스 문자열을 보고서 서버로 전달하여 HTML 뷰어 도구 모음 없이 렌더링된 보고서를 생성할 수 있습니다.  
  
```  
https://<Server Name>/reportserver?/SampleReports/Sales Order Detail&rs:Command=Render&rs:Format=HTML4.0&rc:Toolbar=False  
```  
  
 자세한 내용은 [URL에 디바이스 정보 설정 지정](../../../reporting-services/specify-device-information-settings-in-a-url.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [렌더링 확장 프로그램에 대한 디바이스 정보 설정&#40;Reporting Services&#41;](../../../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](../../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [웹 서비스 및 .NET Framework를 사용하여 애플리케이션 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
