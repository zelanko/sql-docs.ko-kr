---
title: Excel 디바이스 정보 설정 | Microsoft Docs
description: Microsoft Excel 형식으로 렌더링하기 위한 다양한 디바이스 정보 설정을 자세히 알아봅니다.
ms.date: 01/23/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], Excel rendering
- Excel [Reporting Services], rendering
ms.assetid: bb5f3566-f033-4470-be87-1f52fb7a4ab6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c4d84c98923a3cee94f64fed863e621821bd7a39
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245132"
---
# <a name="excel-device-information-settings"></a>Excel 디바이스 정보 설정
  다음 표는 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 형식으로 렌더링하기 위한 디바이스 정보 설정을 나열합니다.  
  
|설정|값|  
|-------------|-----------|  
|**OmitDocumentMap**|지원하는 보고서에 대한 문서 구조를 생략할지 여부를 나타냅니다. 기본 값은 **false**입니다.|  
|**OmitFormulas**|렌더링된 보고서에서 수식을 생략할지 여부를 나타냅니다. 기본 값은 **false**입니다.|  
|**SimplePageHeaders**|보고서의 페이지 머리글이 Excel 페이지 머리글로 렌더링되는지 여부를 나타냅니다. **false** 값은 페이지 머리글이 워크시트의 첫 행에 렌더링됨을 나타냅니다. 기본 값은 **false**입니다.|  
|**DynamicImageDpi**|차트, 계기 및 지도와 같은 동적 이미지의 해상도입니다. 기본값은 **96**입니다. (Power BI Report Server(2020년 1월) 이상에서 사용 가능)|  

  
## <a name="see-also"></a>참고 항목  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [디바이스 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
