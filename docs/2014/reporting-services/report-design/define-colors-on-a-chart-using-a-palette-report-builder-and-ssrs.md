---
title: 색상표를 사용하여 차트에 대한 색 정의(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d95efc22-5a32-43d4-9bd2-12753e7fd395
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 59fc4a9e46e0dbe0f88047a2804330ba1c6ba18d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106078"
---
# <a name="define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs"></a>색상표를 사용하여 차트에 대한 색 정의(보고서 작성기 및 SSRS)
  미리 정의된 색상표를 선택하거나 사용자 지정 색상표를 정의하여 차트의 색상표를 변경할 수 있습니다. 사용자 지정 색상표는 이를 지정한 보고서에 대해서만 적용됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-colors-on-the-chart-using-a-built-in-color-palette"></a>기본 제공 색상표를 사용하여 차트의 색을 변경하려면  
  
1.  속성 창을 엽니다.  
  
2.  디자인 화면에서 차트를 클릭합니다. 차트 개체의 속성이 속성 창에 표시됩니다.  
  
     개체 이름(기본적으로**Chart1** )이 속성 창 위쪽에 있는 드롭다운 목록에 표시됩니다.  
  
3.  **차트** 섹션의 드롭다운 목록에서 Palette 속성에 대해 새 색상표를 선택합니다.  
  
    > [!NOTE]  
    >  미리 정의된 색상표의 색이나 순서를 변경할 수는 없습니다.  
  
### <a name="to-define-your-own-colors-on-the-chart-using-a-custom-color-palette"></a>사용자 지정 색상표를 사용하여 차트에 사용자 고유의 색을 정의하려면  
  
1.  속성 창을 엽니다.  
  
2.  디자인 화면에서 차트를 클릭합니다. 차트 개체의 속성이 속성 창에 표시됩니다.  
  
3.  에 **차트** 섹션에 대 한 합니다 `Palette` 속성을 선택 **사용자 지정**합니다.  
  
4.  CustomPaletteColors 속성에서 컬렉션 편집(**...**) 단추를 클릭합니다. **ReportColorExpression 컬렉션 편집기** 가 열립니다.  
  
5.  색을 추가하려면 **추가** 를 클릭합니다. 드롭다운 목록에서 색을 선택하거나 식을 선택한 다음 특정 색의 16진수 값을 지정합니다. 예를 들어 ff6600은 "주황색"을 의미합니다.  
  
     16진수 값에 대한 자세한 내용은 MSDN에서 [색상표(Color Table)](https://go.microsoft.com/fwlink/?linkid=9258) 를 참조하십시오.  
  
6.  색상표에 다른 색을 더 추가하려면 **추가** 를 클릭합니다.  
  
7.  완료되면 **확인**을 클릭합니다.  
  
 사용자 지정 색상표를 사용하면 색의 순서를 변경하여 차트의 다른 계열 색을 변경할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [여러 셰이프 차트에 일관된 색 지정&#40;보고서 작성기 및 SSRS&#41;](shape-charts-report-builder-and-ssrs.md)  
  
  
