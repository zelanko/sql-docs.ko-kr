---
title: 보고서 매개 변수의 기본값 추가, 변경 또는 삭제 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10460"
- sql13.rtp.rptdesigner.reportparameters.defaultvalues.f1
- "10072"
ms.assetid: 6a87e069-b3a9-47b6-bcec-afcdd8aff65f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 902d28e7d37524ac0d1649642ca592b20ea5b3cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65582038"
---
# <a name="add-change-or-delete-default-values-for-a-report-parameter"></a>보고서 매개 변수의 기본값 추가, 변경 또는 삭제
  보고서 매개 변수를 만든 후에는 기본값 목록을 제공할 수 있습니다. 모든 매개 변수에 유효한 기본값이 있는 경우 보고서를 처음으로 보거나 미리 볼 때 해당 보고서가 자동으로 실행됩니다.  
  
 보고서 매개 변수는 단일 값이나 여러 값을 나타낼 수 있습니다. 단일 값의 경우 리터럴 또는 식을 제공할 수 있습니다. 여러 값의 경우에는 정적 목록 또는 보고서 데이터 세트의 목록을 제공할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 보고서를 게시한 후에는 보고서 서버에서 매개 변수 속성 값을 설정하여 보고서 제작 도구에서 보고서에 정의한 기본값을 재정의할 수 있습니다. 연결된 보고서를 만들어 여러 기본 매개 변수 값 집합을 제공할 수도 있습니다. 자세한 내용은  [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
### <a name="to-add-or-change-the-default-values-for-a-report-parameter"></a>보고서 매개 변수의 기본값을 추가 또는 변경하려면  
  
1.  보고서 데이터 창에서 **매개 변수** 노드를 확장합니다. 매개 변수를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다. **보고서 매개 변수 속성** 대화 상자가 열립니다.  
  
    > [!NOTE]  
    >  보고서 데이터 창이 표시되지 않는 경우 **보기** , **보고서 데이터**를 차례로 클릭합니다.  
  
2.  **기본값**을 클릭합니다.  
  
3.  기본 옵션을 선택합니다.  
  
    -   값 또는 값 목록을 직접 제공하려면 **값 지정**을 클릭합니다. **추가** 를 클릭한 다음 **값** 입력란에 값을 입력합니다. 값에 대한 식을 작성할 수 있습니다. 데이터 형식은 매개 변수의 데이터 형식과 일치해야 합니다. 필드 이름은 매개 변수의 식에 사용할 수 없습니다.  
  
         다중값 매개 변수의 경우 제공할 값 개수만큼 이 단계를 반복합니다. 이 목록에 표시되는 항목의 순서에 따라 드롭다운 목록에 표시되는 항목의 순서가 결정됩니다. 목록에서 항목의 순서를 변경하려면 **값** 입력란을 클릭하여 항목을 선택한 다음 위쪽 및 아래쪽 화살표 단추를 사용하여 항목을 목록의 위 또는 아래로 이동합니다.  
  
    -   값을 검색하는 기존 데이터 세트의 이름을 제공하려면 **쿼리에서 값 가져오기**를 클릭합니다. **데이터 세트**에서 데이터 세트의 이름을 선택합니다.  
  
         **값 필드**에서 매개 변수 값을 제공하는 필드의 이름을 선택합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-the-default-values-for-a-report-parameter"></a>보고서 매개 변수의 기본값을 제거하려면  
  
1.  보고서 데이터 창에서 **매개 변수** 노드를 확장합니다. 매개 변수를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다. **보고서 매개 변수 속성** 대화 상자가 열립니다.  
  
2.  **기본값**을 클릭합니다.  
  
3.  **다음 옵션 중 하나 선택**에서 **기본값 없음**을 클릭합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [보고서에 연계 매개 변수 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [자습서: 보고서에 매개 변수 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [데이터 세트 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [매개 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [보고서 매개 변수의 순서 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [보고서 매개 변수 추가, 변경 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
