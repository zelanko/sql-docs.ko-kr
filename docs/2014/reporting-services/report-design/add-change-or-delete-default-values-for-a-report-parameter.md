---
title: 추가, 변경 하거나 (보고서 작성기 및 SSRS) 보고서 매개 변수의 기본값을 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10460"
- sql12.rtp.rptdesigner.reportparameters.defaultvalues.f1
- "10072"
ms.assetid: 6a87e069-b3a9-47b6-bcec-afcdd8aff65f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 294940b2ffdeab57d3cde8f7a1fe8a8b61d6532a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48221883"
---
# <a name="add-change-or-delete-default-values-for-a-report-parameter-report-builder-and-ssrs"></a>보고서 매개 변수의 기본값 추가, 변경 또는 삭제(보고서 작성기 및 SSRS)
  보고서 매개 변수를 만든 후에는 기본값 목록을 제공할 수 있습니다. 모든 매개 변수에 유효한 기본값이 있는 경우 보고서를 처음으로 보거나 미리 볼 때 해당 보고서가 자동으로 실행됩니다.  
  
 보고서 매개 변수는 단일 값이나 여러 값을 나타낼 수 있습니다. 단일 값의 경우 리터럴 또는 식을 제공할 수 있습니다. 여러 값의 경우에는 정적 목록 또는 보고서 데이터 집합의 목록을 제공할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 보고서를 게시한 후에는 보고서 서버에서 매개 변수 속성 값을 설정하여 보고서 제작 도구에서 보고서에 정의한 기본값을 재정의할 수 있습니다. 연결된 보고서를 만들어 여러 기본 매개 변수 값 집합을 제공할 수도 있습니다. 자세한 내용은 [보고서 매개 변수 &#40;보고서 작성기 및 보고서 디자이너&#41;](report-parameters-report-builder-and-report-designer.md)  
  
### <a name="to-add-or-change-the-default-values-for-a-report-parameter"></a>보고서 매개 변수의 기본값을 추가 또는 변경하려면  
  
1.  보고서 데이터 창에서 **매개 변수** 노드를 확장합니다. 매개 변수를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다. **보고서 매개 변수 속성** 대화 상자가 열립니다.  
  
    > [!NOTE]  
    >  보고서 데이터 창이 표시되지 않는 경우 **보기** , **보고서 데이터**를 차례로 클릭합니다.  
  
2.  **기본값**을 클릭합니다.  
  
3.  기본 옵션을 선택합니다.  
  
    -   값 또는 값 목록을 직접 제공하려면 **값 지정**을 클릭합니다. **추가** 를 클릭한 다음 **값** 입력란에 값을 입력합니다. 값에 대한 식을 작성할 수 있습니다. 데이터 형식은 매개 변수의 데이터 형식과 일치해야 합니다. 필드 이름은 매개 변수의 식에 사용할 수 없습니다.  
  
         다중값 매개 변수의 경우 제공할 값 개수만큼 이 단계를 반복합니다. 이 목록에 표시되는 항목의 순서에 따라 드롭다운 목록에 표시되는 항목의 순서가 결정됩니다. 목록에서 항목의 순서를 변경하려면 **값** 입력란을 클릭하여 항목을 선택한 다음 위쪽 및 아래쪽 화살표 단추를 사용하여 항목을 목록의 위 또는 아래로 이동합니다.  
  
    -   값을 검색하는 기존 데이터 집합의 이름을 제공하려면 **쿼리에서 값 가져오기**를 클릭합니다. **데이터 집합**에서 데이터 집합의 이름을 선택합니다.  
  
         **값 필드**에서 매개 변수 값을 제공하는 필드의 이름을 선택합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-the-default-values-for-a-report-parameter"></a>보고서 매개 변수의 기본값을 제거하려면  
  
1.  보고서 데이터 창에서 **매개 변수** 노드를 확장합니다. 매개 변수를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다. **보고서 매개 변수 속성** 대화 상자가 열립니다.  
  
2.  **기본값**을 클릭합니다.  
  
3.  **다음 옵션 중 하나 선택**에서 **기본값 없음**을 클릭합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](report-parameters-report-builder-and-report-designer.md)   
 [보고서에 연계 매개 변수를 추가 &#40;보고서 작성기 및 SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [자습서: 보고서에 매개 변수 추가&#40;보고서 작성기&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [매개 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)   
 [보고서 매개 변수의 순서를 변경 &#40;보고서 작성기 및 SSRS&#41;](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [추가, 변경 또는 Delete a Report Parameter &#40;보고서 작성기 및 SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
