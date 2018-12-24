---
title: 이미지 디바이스 정보 설정 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- images [Reporting Services], rendering
- device information settings [Reporting Services], IMAGE rendering
ms.assetid: edad9498-69f7-4726-8699-fa615f704dff
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b59fcf947a283ef60f5dd34f60e2cf365092cfa7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738731"
---
# <a name="image-device-information-settings"></a>이미지 디바이스 정보 설정
  다음 표는 IMAGE 형식으로 렌더링하기 위한 디바이스 정보 설정을 나열합니다.  
  
|설정|값|  
|-------------|-----------|  
|**열**|보고서에 대해 설정할 열 수입니다. 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**ColumnSpacing**|보고서에 대해 설정할 열 간격입니다. 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**DpiX**|출력 이미지의 수평 해상도입니다. 기본값은 **96**입니다. **BMP**, **GIF**, **PNG**및 **TIFF** 출력 형식에 적용됩니다.|  
|**DpiY**|출력 이미지의 수직 해상도입니다. 기본값은 **96**입니다. **BMP**, **GIF**, **PNG**및 **TIFF** 출력 형식에 적용됩니다.|  
|**EndPage**|렌더링할 보고서의 마지막 페이지입니다. 기본값은 **StartPage**에 대한 값입니다.|  
|**MarginBottom**|보고서에 대해 설정할 아래쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: **1in**). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**MarginLeft**|보고서에 대해 설정할 왼쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: **1in**). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**MarginRight**|보고서에 대해 설정할 오른쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: **1in**). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**MarginTop**|보고서에 대해 설정할 위쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: **1in**). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**OutputFormat**|출력 형식에서 지원하는 [!INCLUDE[ndptecgdiexpanded](../includes/ndptecgdiexpanded-md.md)] ([!INCLUDE[ndptecgdi](../includes/ndptecgdi-md.md)])입니다. **BMP**, **EMF**, **GIF**, **JPEG**, **PNG**또는 **TIFF**|  
|**PageHeight**|보고서에 대해 설정할 페이지 높이(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: **11in**). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**PageWidth**|보고서에 대해 설정할 페이지 너비(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: **8.5in**). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**PrintDpiX**|출력 이미지의 수평 해상도입니다. 기본값은 **300**입니다. **EMF**(확장 메타파일) 출력 형식에 적용됩니다.|  
|**PrintDpiY**|출력 이미지의 수직 해상도입니다. 기본값은 **300**입니다. **EMF**(확장 메타파일) 출력 형식에 적용됩니다.|  
|**StartPage**|렌더링할 보고서의 첫 페이지입니다. **0** 값은 모든 페이지가 렌더링됨을 나타냅니다. 기본값은 **1**입니다.|  
  
## <a name="see-also"></a>참고 항목  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [장치 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
