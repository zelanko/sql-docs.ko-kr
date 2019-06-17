---
title: 행 표시 유형 대화 상자 (보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10126"
ms.assetid: 117fb20c-2fda-437e-bcc5-9010d6d4b53b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d5ad7e47457aa2d1f1d5e36adec7e988de7b8bbb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102345"
---
# <a name="row-visibility-dialog-box-report-builder"></a>행 표시 유형 대화 상자(보고서 작성기)
  **행 표시 유형** 대화 상자를 사용하면 보고서를 처음 실행할 때 선택된 행을 표시하거나 숨길 수 있고 다른 보고서 항목을 사용하여 행의 표시 유형을 전환할 수 있습니다.  
  
## <a name="options"></a>변수  
 **보고서를 처음 실행할 때**  
 보고서에 행이 처음 표시되는 방식을 나타내는 옵션을 선택합니다.  
  
 **표시**  
 행을 표시하려면 이 옵션을 선택합니다.  
  
 **숨기기**  
 행을 숨기려면 이 옵션을 선택합니다.  
  
 **식에 따라 표시 또는 숨기기**  
 식을 사용하여 초기 표시 유형을 변경하려면 이 옵션을 선택합니다.  
  
 `Boolean` 값을 반환하는 식을 입력합니다. `True`는 항목을 숨기고 `False`는 항목을 표시합니다. 식을 편집하려면 **식** 단추(*fx*)를 클릭합니다.  
  
 **이 보고서 항목으로 표시 또는 숨기기 가능**  
 사용자가 이 행을 HTML 보고서 뷰어에 표시하거나 숨길 수 있도록 토글 이미지를 표시하려면 이 옵션을 선택합니다.  
  
 보고서에서 토글 이미지를 표시할 입력란 이름(예: Textbox1)을 입력하거나 선택해야 합니다. 선택한 입력란은 현재 보고서 항목과 동일한 범위 또는 포함 범위에 있는 입력란이어야 합니다. 예를 들어 자식 그룹과 연결된 행의 표시 유형을 전환하려면 부모 그룹과 연결된 행에 있는 입력란을 선택합니다. 차트의 표시 유형을 전환하려면 차트와 동일한 포함 범위(예: 보고서 본문 또는 사각형)에 있는 입력란을 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [식 예&#40;보고서 작성기 및 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [항목에 확장 또는 축소 동작 추가&#40;보고서 작성기 및 SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [이미지&#40;보고서 작성기 및 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [대화 상자, 창 및 마법사에 대한 보고서 작성기 도움말](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [이미지 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
