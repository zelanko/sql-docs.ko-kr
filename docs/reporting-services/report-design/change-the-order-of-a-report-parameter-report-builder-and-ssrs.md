---
title: "보고서 매개 변수 (보고서 작성기 및 SSRS)의 순서를 변경 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3377e943ddf7d8c7bd06aeab52ee263a754af25c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>보고서 매개 변수의 순서 변경(보고서 작성기 및 SSRS)
  종속 매개 변수가 종속 대상 매개 변수 앞에 나열된 경우 보고서 매개 변수의 순서를 변경합니다. 매개 변수 순서는 연계 매개 변수가 있거나 사용자가 한 매개 변수의 기본값을 본 다음 다른 매개 변수의 값을 선택하도록 하려는 경우 중요합니다. 종속 보고서 매개 변수에는 쿼리 매개 변수에 대한 참조가 기본값 쿼리 또는 유효한 값 쿼리에 포함됩니다. 이 쿼리 매개 변수는 **보고서 데이터** 창의 매개 변수 목록에서 해당 매개 변수 뒤에 오는 보고서 매개 변수를 가리킵니다.  
  
 보고서를 실행할 때 보고서 뷰어 도구 모음에서 매개 변수가 표시되는 순서는 **보고서 데이터** 창의 매개 변수 순서와 사용자 지정 매개 변수 창의 매개 변수 위치에 의해 결정됩니다. 자세한 내용은 참조 [보고서 &#40;의 매개 변수 창을 사용자 지정 보고서 작성기 &#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-order-of-report-parameters"></a>보고서 매개 변수의 순서를 변경하려면  
  
보고서 매개 변수의 순서를 변경하려면 다음 중 하나를 수행합니다.  
  
-   **보고서 데이터** 창에서 매개 변수를 클릭하고 다음 그림에 나와 있는 것처럼 위쪽 및 아래쪽 화살표 단추를 사용하여 매개 변수를 목록에서 위 또는 아래 위치로 이동합니다.  **보고서 데이터** 창에서 매개 변수 순서를 변경하면 매개 변수 창에서 매개 변수 위치가 변경됩니다.  
  
     ![보고서 데이터 창에서 매개 변수의 순서 변경](../../reporting-services/report-design/media/ssrs-changeorderofparameters-reportdata.png "보고서 데이터 창에서 매개 변수의 순서 변경")  
  
-   매개 변수 창에서 창의 새 열이나 행으로 매개 변수를 끕니다. 창에서 매개 변수의 위치를 변경하면 **보고서 데이터** 창에서 매개 변수 순서가 변경됩니다. 창에서 매개 변수를 이동 하는 방법에 대 한 자세한 내용은 참조 [보고서 &#40;의 매개 변수 창을 사용자 지정 보고서 작성기 &#41; ](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수 사용 &#40; 보고서 작성기 및 보고서 디자이너 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [대화 상자, 창 및 마법사에 대 한 보고서 작성기 도움말](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [보고서 &#40; 연계 매개 변수 추가 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [자습서: 보고서 &#40; 매개 변수 추가 보고서 작성기 &#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 &#40; 추가 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [매개 변수 컬렉션 참조 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
