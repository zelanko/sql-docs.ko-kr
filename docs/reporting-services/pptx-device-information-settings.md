---
title: "PPTX 장치 정보 설정 | Microsoft Docs"
ms.custom: 
ms.date: 09/11/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- render
- powerpoint
- pptx
- export
ms.assetid: 4dc2045f-8025-41a3-8f9d-5635fb24cf4a
caps.latest.revision: "6"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0b83a1cd9142dab2b74f5dbb3148576d851faf24
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="pptx-device-information-settings"></a>PPTX 장치 정보 설정
  다음 표는 PPTX 형식으로 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서를 렌더링하기 위한 장치 정보 설정을 나열합니다.  
  
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
|**PageHeight**|보고서에 대해 설정할 페이지 높이(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: **11in**). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**PageWidth**|보고서에 대해 설정할 페이지 너비(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: **8.5in**). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**StartPage**|렌더링할 보고서의 첫 페이지입니다. **0** 값은 모든 페이지가 렌더링됨을 나타냅니다. 기본값은 **1**입니다.|  
|**UseReportPageSize**|UseReportPageSize =**false** 인 경우 기본 슬라이드 크기는 13.333” x 7.5”(16:9 가로 세로 비율)의 PowerPoint의 기본값입니다. UseReportPageSize =true인 경우 기본 슬라이드 크기는 보고서의 정의 페이지 크기입니다.<br /><br /> 기본값은 **false**입니다.<br /><br /> PageWidth 및 PageHeight 설정은 기본 너비와 높이를 재정의합니다.|  
  
## <a name="see-also"></a>참고 항목  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [장치 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
