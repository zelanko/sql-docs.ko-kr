---
title: 그룹 또는 테이블릭스 데이터 영역에 합계 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cf1b96c3-7f0f-4c94-ad08-5239c77ccfe4
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 800c8ce788f4152f1f429b54032efa193972c10f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159974"
---
# <a name="add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs"></a>그룹 또는 테이블릭스 데이터 영역에 합계 추가(보고서 작성기 및 SSRS)
  그룹 또는 전체 데이터 영역에 대한 테이블릭스 데이터 영역에 합계를 추가할 수 있습니다. 기본적으로 합계는 필터가 적용된 후 그룹 또는 데이터 영역의 Null이 아닌 숫자 데이터의 합계입니다. 그룹에 대한 합계를 추가하려면 그룹화 창의 그룹에 대한 바로 가기 메뉴에서 **합계 추가** 를 클릭합니다. 테이블릭스 본문 영역에서 개별 셀에 대한 합계를 추가하려면 셀에 대한 바로 가기 메뉴에서 **합계 추가** 를 클릭합니다. **합계 추가** 명령은 상황에 맞게 작동하며 숫자 필드에 대해서만 사용할 수 있습니다. 선택한 테이블릭스 셀에 따라 테이블릭스 본문 영역에서 셀을 선택하여 단일 셀에 대한 합계를 추가하거나 테이블릭스 행 그룹 영역 또는 열 그룹 영역에서 셀을 선택하여 전체 그룹에 대한 합계를 추가할 수 있습니다. 테이블 릭 스 영역에 대 한 자세한 내용은 참조 하세요. [테이블 릭 스 데이터 영역 &#40;보고서 작성기 및 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)합니다.  
  
 합계를 추가한 후에는 기본 함수 Sum을 기본 제공 보고서 함수 목록의 다른 집계 함수로 변경할 수 있습니다. 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)를 참조하세요.[!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-total-for-an-individual-value-in-the-tablix-body-area"></a>테이블릭스 본문 영역의 개별 값에 대한 합계를 추가하려면  
  
-   테이블릭스 데이터 영역 본문 영역에서 합계를 추가할 셀을 마우스 오른쪽 단추로 클릭합니다. 셀은 숫자 필드를 포함해야 합니다. **합계 추가**를 가리킨 다음 **행** 또는 **열**을 클릭합니다.  
  
     새 행 또는 열이 클릭한 셀의 필드에 대한 기본 합계와 함께 현재 그룹 외부 데이터 영역에 추가됩니다.  
  
     테이블릭스 데이터 영역이 테이블이면 행이 자동으로 추가됩니다.  
  
### <a name="to-add-totals-for-a-row-group"></a>행 그룹에 대한 합계를 추가하려면  
  
-   테이블릭스 데이터 영역 행 그룹 영역에서 합계를 구할 행 그룹 영역의 셀을 마우스 오른쪽 단추로 클릭한 다음 **합계 추가**를 가리키고 **이전** 또는 **이후**를 클릭합니다.  
  
     새 행이 현재 그룹 외부 데이터 영역에 추가되고 해당 행의 각 숫자 필드에 대한 기본 합계가 추가됩니다.  
  
### <a name="to-add-totals-for-a-column-group"></a>열 그룹에 대한 합계를 추가하려면  
  
-   테이블릭스 데이터 영역 행 그룹 영역에서 합계를 구할 열 그룹 영역의 셀을 마우스 오른쪽 단추로 클릭한 다음 **합계 추가**를 가리키고 **이전** 또는 **이후**를 클릭합니다.  
  
     새 열이 현재 그룹 외부 데이터 영역에 추가되고 해당 열의 각 숫자 필드에 대한 기본 합계가 추가됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [합계, 집계 및 기본 제공 컬렉션의 식 범위 &#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)   
 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [테이블&#40;보고서 작성기 및 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [행렬&#40;보고서 작성기 및 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
