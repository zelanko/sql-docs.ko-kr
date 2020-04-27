---
title: 보고서 매개 변수의 순서 변경(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7a1d9413332ed19bd4db94fc60beecff85f02ac7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106327"
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>보고서 매개 변수의 순서 변경(보고서 작성기 및 SSRS)
  종속 매개 변수가 종속 대상 매개 변수 앞에 나열된 경우 보고서 매개 변수의 순서를 변경합니다. 매개 변수 순서는 연계 매개 변수가 있거나 사용자가 한 매개 변수의 기본값을 본 다음 다른 매개 변수의 값을 선택하도록 하려는 경우 중요합니다. 종속 보고서 매개 변수에는 보고서 데이터 창의 매개 변수 목록에서 해당 매개 변수 뒤에 오는 보고서 매개 변수를 가리키는 쿼리 매개 변수에 대한 참조가 기본값 쿼리 또는 유효한 값 쿼리에 포함되어 있습니다.  
  
 보고서 뷰어 도구 모음에서 매개 변수가 표시되는 순서는 보고서 데이터 창의 매개 변수 순서에 의해 결정됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-order-of-report-parameters"></a>보고서 매개 변수의 순서를 변경하려면  
  
1.  보고서 데이터 창에서 매개 변수 노드를 확장합니다.  
  
2.  매개 변수를 클릭하고 보고서 데이터 창 도구 모음의 위쪽 및 아래쪽 화살표 단추를 사용하여 매개 변수를 목록의 위 또는 아래로 이동합니다. 다음 이미지에는 보고서 작성기의 보고서 데이터 창이 나와 있습니다.  
  
     ![보고서 데이터 창](../media/reportdatapane.png "보고서 데이터 창")  
  
## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수 &#40;보고서 작성기 및 보고서 디자이너&#41;](report-parameters-report-builder-and-report-designer.md)   
 [대화 상자, 창 및 마법사에 대 한 보고서 작성기 도움말](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [보고서 &#40;보고서 작성기 및 SSRS에 연계 매개 변수를 추가&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [자습서: 보고서에 매개 변수를 추가 &#40;보고서 작성기&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터를 추가 하 여 보고서 작성기 및 SSRS &#40;&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [매개 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)  
  
  
