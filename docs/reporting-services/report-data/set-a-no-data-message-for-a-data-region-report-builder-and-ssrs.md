---
title: 데이터 영역에 대한 데이터 없음 메시지 설정(보고서 작성기) | Microsoft Docs
description: 렌더링된 보고서에서 데이터가 없는 데이터 영역 대신 표시할 데이터 없음 메시지를 설정하는 방법을 알아봅니다.
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 4b194714-46f7-4f0e-9632-7f89d9600762
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 504c0cffb8522503eba67308d34b3ad4a1333ff8
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458326"
---
# <a name="set-a-no-data-message-for-a-data-region-report-builder-and-ssrs"></a>데이터 영역에 대한 데이터 없음 메시지 설정(보고서 작성기 및 SSRS)
  렌더링된 보고서에서 데이터가 없는 데이터 영역의 자리에 텍스트가 표시되도록 지정하려면 테이블, 행렬 또는 목록 데이터 영역에 대해 NoRowsMessage 속성을 설정하거나 차트 데이터 영역에 대해 NoDataMessage를 설정하거나, 지도의 색 눈금에 대해 NoDataText를 설정합니다. 보고서 처리기는 런타임에 보고서의 각 데이터 세트에 대한 쿼리를 실행하며 해당 데이터 세트 쿼리에서 결과 집합이 생성되지 않을 수 있습니다. 빈 데이터 세트에 바인딩된 데이터 영역의 경우 빈 데이터 영역을 표시하는 대신 텍스트를 지정하여 표시할 수 있습니다. 또한 런타임에, 하위 보고서의 데이터 세트에 데이터가 없는 경우 하위 보고서의 NoRowsMessage 속성을 설정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-the-norowsmessage-property-for-a-table-matrix-or-list"></a>테이블, 행렬 또는 목록에 대해 NoRowsMessage 속성을 설정하려면  
  
1.  디자인 뷰에서 디자인 화면의 테이블, 행렬 또는 목록 데이터 영역이나 하위 보고서를 클릭하여 선택합니다. 선택한 항목의 속성이 속성 창에 표시됩니다.  
  
2.  속성 창에서 **NoRowsMessage** 속성 필드에 메시지로 표시할 텍스트를 입력합니다.  
  
     또는 드롭다운 목록에서 **식** 을 클릭하여 **식** 대화 상자를 열고 식을 작성합니다.  
  
### <a name="to-set-the-nodatamessage-property-for-a-chart"></a>차트에 대해 NoDataMessage 속성을 설정하려면  
  
1.  디자인 뷰에서 디자인 화면에 있는 차트를 클릭하여 선택합니다. 선택한 항목의 속성이 속성 창에 표시됩니다.  
  
2.  속성 창에서 **NoDataMessage**의 노드를 확장합니다.  
  
3.  **NoDataMessage**속성 필드에 메시지로 표시할 텍스트를 **캡션** 에 입력합니다.  
  
     또는 드롭다운 목록에서 **식** 을 클릭하여 **식** 대화 상자를 열고 식을 작성합니다.  
  
### <a name="to-set-the-norowsmessage-for-a-subreport"></a>하위 보고서에 대해 NoRowsMessage를 설정하려면  
  
1.  디자인 뷰에서 디자인 화면에 있는 하위 보고서를 클릭하여 선택합니다. 선택한 항목의 속성이 속성 창에 표시됩니다.  
  
2.  속성 창에서 **NoRowsMessage** 속성 필드에 메시지로 표시할 텍스트를 입력합니다.  
  
     또는 드롭다운 목록에서 **식** 을 클릭하여 **식** 대화 상자를 열고 식을 작성합니다.  
  
### <a name="to-set-the-nodatatext-property-for-a-color-scale-for-a-map"></a>지도의 색 눈금에 NoDataText 속성을 설정하려면  
  
1.  디자인 뷰에서 지도에 있는 색 눈금을 클릭하여 선택합니다. 선택한 항목의 속성이 속성 창에 표시됩니다.  
  
2.  속성 창의 **NoDataText**에 데이터 값이 없는 색의 레이블로 표시할 텍스트를 입력합니다.  
  
     또는 드롭다운 목록에서 **식** 을 클릭하여 **식** 대화 상자를 열고 식을 작성합니다.  
  
## <a name="see-also"></a>참고 항목  
 [하위 보고서&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [지도&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [하위 보고서&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)  
  
  
