---
title: 채우기 대화 상자 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportbody.fill.f1
- "10065"
- "10501"
- sql12.rtp.rptdesigner.shared.filldv.f1
- sql12.rtp.rptdesigner.rectangleproperties.fill.f1
- "10064"
- sql12.rtp.rptdesigner.textboxproperties.fill.f1
- "10124"
ms.assetid: 93a91d02-d558-4a0e-8d17-3fdf21e208d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c8feeb496948b34abd3bd4205e52854211cde5d5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59960269"
---
# <a name="fill-dialog-box-report-builder-and-ssrs"></a>채우기 대화 상자(보고서 작성기 및 SSRS)
  **채우기** 탭에서 데이터 영역이나 입력란 내의 단일 셀 또는 여러 셀의 배경에 대한 색 옵션을 지정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **채우기 색**  
 사각형의 채우기 색을 선택하려면 색 단추를 클릭합니다. 식을 편집하려면 **식**_(fx)_ 단추를 클릭합니다. 식은 RGB 색을 나타내는 16진수 값이거나 **식** 대화 상자에 제공되는 미리 정의된 색 이름 중 하나일 수 있습니다. 미리 정의된 색 목록을 보려면 **항목** 창에서 **웹**을 선택합니다. **제목** 창에 나열된 색 이름을 식 텍스트 창에 입력할 수 있습니다. 색 이름을 입력할 때 등호(=) 또는 큰따옴표("")를 사용하지 마십시오.  
  
 **이미지 원본 선택**  
 이미지를 저장할 위치를 나타내어 보고서를 렌더링할 때 보고서 처리기에서 이미지를 표시할 수 있도록 합니다.  
  
-   **외부** 보고서 서버 또는 웹 서버에서 이미지를 파일로 유지하려면 이 옵션을 선택합니다.  
  
-   **포함** 이미지를 보고서에 포함하려면 이 옵션을 선택합니다.  
  
-   **데이터베이스** 보고서에 포함할 이미지를 나타내는 데이터베이스 필드 이름을 포함하려면 이 옵션을 선택합니다.  
  
 **이 이미지 사용**  
 **포함** 또는 **외부** 옵션을 선택하면 이 옵션이 나타납니다.  
  
 이미지를 포함하려는 경우 드롭다운 목록에서 보고서에 추가할 그림을 선택합니다. **가져오기** 를 클릭하여 드롭다운 목록에 이미지를 추가합니다. **데이터** 창에 이미지를 추가한 경우 **포함** 을 선택한 다음 드롭다운 목록에서 해당 이미지를 선택하여 이미지를 선택할 수 있습니다.  
  
 **외부** 옵션을 선택할 경우 이미지의 URL을 입력합니다. 기본 모드로 구성 된 보고서 서버에 게시 된 보고서를 사용할 경우 전체 경로나 상대 경로 (예를 들어, http://*\<서버 이름 >*  /images/image1.jpg). SharePoint 통합 모드로 구성 된 보고서 서버에 게시 된 보고서를 사용 하 여 정규화 된 URL (예를 들어, http://*\<SharePointservername > /\<사이트 >* 문서/이미지 / / image1.jpg)입니다.  
  
 **가져오기**  
 **포함**을 선택하면 사용할 수 있습니다. **이 이미지 사용** 드롭다운 목록에 이미지를 추가하려면 클릭합니다.  
  
 **이 필드 사용**  
 **데이터베이스**를 선택하면 사용할 수 있습니다. 필드 이름을 선택합니다.  
  
 **이 MIME 형식 사용**  
 데이터베이스에 포함된 그림에 적합한 형식을 선택합니다(예: .bmp, .jpeg, .gif, .png, .x-png).  
  
## <a name="see-also"></a>관련 항목  
 [보고서 항목 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [텍스트 및 자리 표시자 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [이미지&#40;보고서 작성기 및 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)  
  
  
