---
title: 보고서 매개 변수의 순서 변경(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e3647e52c7042d24d34605d85f17593b669df7c0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649521"
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>보고서 매개 변수의 순서 변경(보고서 작성기 및 SSRS)
  종속 매개 변수가 종속 대상 매개 변수 앞에 나열된 경우 보고서 매개 변수의 순서를 변경합니다. 매개 변수 순서는 연계 매개 변수가 있거나 사용자가 한 매개 변수의 기본값을 본 다음 다른 매개 변수의 값을 선택하도록 하려는 경우 중요합니다. 종속 보고서 매개 변수에는 쿼리 매개 변수에 대한 참조가 기본값 쿼리 또는 유효한 값 쿼리에 포함됩니다. 이 쿼리 매개 변수는 **보고서 데이터** 창의 매개 변수 목록에서 해당 매개 변수 뒤에 오는 보고서 매개 변수를 가리킵니다.  
  
 보고서를 실행할 때 보고서 뷰어 도구 모음에서 매개 변수가 표시되는 순서는 **보고서 데이터** 창의 매개 변수 순서와 사용자 지정 매개 변수 창의 매개 변수 위치에 의해 결정됩니다. 자세한 내용은 [보고서에서 매개 변수 창 사용자 지정&#40;보고서 작성기&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-order-of-report-parameters"></a>보고서 매개 변수의 순서를 변경하려면  
  
보고서 매개 변수의 순서를 변경하려면 다음 중 하나를 수행합니다.  
  
-   **보고서 데이터** 창에서 매개 변수를 클릭하고 다음 그림에 나와 있는 것처럼 위쪽 및 아래쪽 화살표 단추를 사용하여 매개 변수를 목록에서 위 또는 아래 위치로 이동합니다.  **보고서 데이터** 창에서 매개 변수 순서를 변경하면 매개 변수 창에서 매개 변수 위치가 변경됩니다.  
  
     ![보고서 데이터 창에서 매개 변수 순서 변경](../../reporting-services/report-design/media/ssrs-changeorderofparameters-reportdata.png "보고서 데이터 창에서 매개 변수 순서 변경")  
  
-   매개 변수 창에서 창의 새 열이나 행으로 매개 변수를 끕니다. 창에서 매개 변수의 위치를 변경하면 **보고서 데이터** 창에서 매개 변수 순서가 변경됩니다. 창에서 매개 변수 이동에 대한 자세한 내용은 [보고서에서 매개 변수 창 사용자 지정&#40;보고서 작성기&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [보고서에 연계 매개 변수 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [자습서: 보고서에 매개 변수 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [매개 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
