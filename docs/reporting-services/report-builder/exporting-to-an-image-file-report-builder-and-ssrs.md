---
title: 이미지 파일로 내보내기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f9357a7691a6e8f2af20aa7c2d5effa58c8ac105
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33019810"
---
# <a name="exporting-to-an-image-file-report-builder-and-ssrs"></a>이미지 파일로 내보내기(보고서 작성기 및 SSRS)
  이미지 렌더링 확장 프로그램은 페이지가 매겨진 보고서를 비트맵이나 메타 파일로 렌더링합니다. 기본적으로 이미지 렌더링 확장 프로그램은 보고서를 여러 페이지로 볼 수 있도록 TIFF 파일로 만듭니다. 클라이언트가 이미지를 수신하면 이미지 뷰어에서 확인하거나 인쇄할 수 있습니다. 이 항목에서는 이미지 렌더러 관련 정보를 제공하고 렌더링 규칙의 예외를 설명합니다.  
  
 이미지 렌더링 확장 프로그램은 [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]에서 지원하는 BMP, EMF, EMFPlus, GIF, JPEG, PNG 및 TIFF 형식으로 파일을 생성할 수 있습니다. TIFF 형식의 경우 기본 스트림의 파일 이름은 *ReportName*.tif입니다. 파일당 한 페이지로 렌더링되는 기타 모든 형식의 경우 파일 이름은 *ReportName_Page.ext* 입니다. 여기서*ext* 는 선택한 형식의 파일 확장명입니다. 다른 이미지 지원 형식으로 파일을 생성하려면 위에 나와 있는 문자열 중 하나를 **OutputFormatDeviceInfo** 설정에 지정합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="SupportedImageFormats"></a> 지원되는 이미지 형식  
 다음 표에는 각 이미지 렌더러 형식에 대한 파일 확장명과 MIMEType이 나와 있습니다.  
  
|**형식**|**확장명**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|BMP|image/bmp|  
|GIF|GIF|image/gif|  
|JPEG|JPEG|image/jpeg|  
|PNG|PNG|image/png|  
|TIFF|tif|image/tiff|  
|EMF|EMF|image/emf|  
|EMFPlus|emf|image/emf|  
  
  
##  <a name="RenderingMultiplePages"></a> 여러 페이지 렌더링  
 TIFF는 파일 하나에 여러 페이지 문서를 포함할 수 있는 유일한 형식입니다. JPG나 PNG 같은 다른 형식은 한 번에 한 페이지만 출력하며 매번 각 페이지에 대한 렌더링 확장 프로그램을 호출해야 합니다.  
  
  
##  <a name="Interactivity"></a> 상호 작용  
 상호 작용은 이 렌더러를 통해 생성되는 어떤 이미지 형식에서도 지원되지 않습니다. 다음 대화형 요소는 렌더링되지 않습니다.  
  
-   하이퍼링크  
  
-   표시 또는 숨기기  
  
-   문서 구조  
  
-   드릴스루 또는 클릭 광고 링크  
  
-   최종 사용자 정렬  
  
-   고정 머리글  
  
-   책갈피  
  
  
##  <a name="DeviceInfo"></a> 장치 정보 설정  
 장치 정보 설정을 변경하여 이 렌더러의 기본 설정을 일부 변경할 수 있습니다. 자세한 내용은 [Image Device Information Settings](../../reporting-services/image-device-information-settings.md)을(를) 참조하세요.  
  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [여러 보고서 렌더링 확장 프로그램의 대화형 기능&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [보고서 항목 렌더링&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
