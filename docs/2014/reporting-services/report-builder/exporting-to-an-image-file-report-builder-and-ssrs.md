---
title: 이미지 파일로 내보내기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fd3a6e7126775479ae7ca0c6b6d138a0625476af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107887"
---
# <a name="exporting-to-an-image-file-report-builder-and-ssrs"></a>이미지 파일로 내보내기(보고서 작성기 및 SSRS)
  이미지 렌더링 확장 프로그램은 보고서를 비트맵이나 메타파일로 렌더링합니다. 기본적으로 이미지 렌더링 확장 프로그램은 보고서를 여러 페이지로 볼 수 있도록 TIFF 파일로 만듭니다. 클라이언트가 이미지를 수신하면 이미지 뷰어에서 확인하거나 인쇄할 수 있습니다. 이 항목에서는 이미지 렌더러 관련 정보를 제공하고 렌더링 규칙의 예외를 설명합니다.  
  
 이미지 렌더링 확장 프로그램은 [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]에서 지원하는 BMP, EMF, EMFPlus, GIF, JPEG, PNG 및 TIFF 형식으로 파일을 생성할 수 있습니다. TIFF 형식의 경우 기본 스트림의 파일 이름은 *ReportName*.tif입니다. 파일당 한 페이지로 렌더링되는 기타 모든 형식의 경우 파일 이름은 *ReportName_Page.ext* 입니다. 여기서*ext* 는 선택한 형식의 파일 확장명입니다. 다른 이미지 지원 형식으로 파일을 생성하려면 위에 나와 있는 문자열 중 하나를 **OutputFormatDeviceInfo** 설정에 지정합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="supported-image-formats"></a><a name="SupportedImageFormats"></a> 지원되는 이미지 형식  
 다음 표에는 각 이미지 렌더러 형식에 대한 파일 확장명과 MIMEType이 나와 있습니다.  
  
|**Type**|**확장명**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|BMP|image/bmp|  
|GIF|GIF|image/gif|  
|JPEG|JPEG|image/jpeg|  
|PNG|png|image/png|  
|TIFF|tif|image/tiff|  
|EMF|EMF|image/emf|  
|EMFPlus|EMF|image/emf|  
  
  
##  <a name="rendering-multiple-pages"></a><a name="RenderingMultiplePages"></a> 여러 페이지 렌더링  
 TIFF는 파일 하나에 여러 페이지 문서를 포함할 수 있는 유일한 형식입니다. JPG나 PNG 같은 다른 형식은 한 번에 한 페이지만 출력하며 매번 각 페이지에 대한 렌더링 확장 프로그램을 호출해야 합니다.  
  
  
##  <a name="interactivity"></a><a name="Interactivity"></a>대화형 작업  
 상호 작용은 이 렌더러를 통해 생성되는 어떤 이미지 형식에서도 지원되지 않습니다. 다음 대화형 요소는 렌더링되지 않습니다.  
  
-   하이퍼링크  
  
-   표시 또는 숨기기  
  
-   문서 구조  
  
-   드릴스루 또는 클릭 광고 링크  
  
-   최종 사용자 정렬  
  
-   고정 머리글  
  
-   책갈피  
  
  
##  <a name="device-information-settings"></a><a name="DeviceInfo"></a>장치 정보 설정  
 디바이스 정보 설정을 변경하여 이 렌더러의 기본 설정을 일부 변경할 수 있습니다. 자세한 내용은 [Image Device Information Settings](../image-device-information-settings.md)을(를) 참조하세요.  
  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services &#40;보고서 작성기 및 SSRS의 페이지 매김&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [보고서 작성기 및 SSRS&#41;&#40;렌더링 동작](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [여러 보고서 렌더링 확장 프로그램에 대 한 대화형 기능 &#40;보고서 작성기 및 SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [보고서 항목 &#40;보고서 작성기 및 SSRS&#41;렌더링](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
