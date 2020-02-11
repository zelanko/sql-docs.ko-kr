---
title: 대화형 정렬(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 00cafed5-1a3c-4ce0-a1fb-ff1e2613f495
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 02735bafde927ba110de6465c5380987ddb6b5f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105617"
---
# <a name="interactive-sort-report-builder-and-ssrs"></a>대화형 정렬(보고서 작성기 및 SSRS)
  대화형 정렬 단추를 추가하여 사용자가 테이블의 행 또는 행렬의 행 및 열에 대해 오름차순 및 내림차순 사이를 전환하도록 할 수 있습니다. 대화형 정렬의 일반적인 용도는 열 머리글마다 정렬 단추를 추가하는 것입니다. 그러면 사용자는 정렬할 기준이 되는 열을 선택할 수 있습니다.  
  
 대화형 정렬 단추는 열 머리글뿐만 아니라 모든 입력란에도 추가할 수 있습니다. 예를 들어 행 그룹 외부에 있는 행에 대한 입력란의 경우 부모 그룹 행/열, 자식 그룹 행/열 또는 정보 행/열에 대한 정렬을 지정할 수 있습니다. 또한 필드를 단일 그룹 식으로 결합한 다음 여러 필드를 기준으로 정렬할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 대화형 정렬을 추가하려면 다음 항목을 정의해야 합니다.  
  
-   **정렬 대상:** 행 또는 열  
  
-   **정렬 기준:** 테이블 열에 표시되는 필드 또는 표시되지 않는 필드  
  
-   **정렬할 컨텍스트:** 예를 들어 행 그룹에 연결된 행, 열 그룹에 연결된 열, 정보 행, 부모 그룹 내 자식 그룹 또는 부모 및 자식 그룹 모두를 기준으로 정렬할 수 있습니다.  
  
-   **정렬 단추를 추가할 입력란:** 열 머리글 또는 그룹 행 머리글  
  
-   **여러 데이터 영역에 대해 정렬을 동기화할지 여부:** 보고서를 디자인하여 사용자가 정렬 순서를 전환할 때 다른 데이터 영역도 같은 순서로 정렬되도록 할 수 있습니다.  
  
 단계별 지침은 [테이블 또는 행렬에 대화형 정렬 추가&#40;보고서 작성기 및 SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)를 참조하세요.  
  
 다음 표에서는 대화형 정렬 단추를 사용하여 얻을 수 있는 효과에 대해 간략히 설명합니다.  
  
|작업|정렬 대상|정렬 단추 추가 위치|정렬 기준|정렬 범위|  
|------------|------------------|----------------------------------|---------------------|----------------|  
|그룹이 없는 테이블의 정보 행 정렬|세부 정보|열 머리글|이 열에 바인딩되는 데이터 세트 필드|데이터 영역|  
|행렬의 최상위 그룹 인스턴스 정렬|그룹|열 머리글|부모 그룹의 그룹 식|데이터 영역|  
|테이블의 자식 그룹에 대해 정보 행 정렬|세부 정보|자식 그룹 머리글 행|정렬 기준이 되는 데이터 세트 필드|자식 그룹|  
|여러 행 그룹의 행 및 테이블의 정보 행 정렬|그룹(단, 그룹 식을 구체화해야 함)|열 머리글|정렬 기준이 되는 데이터 세트의 집계|데이터 영역|  
|여러 데이터 영역에 대한 정렬 순서 동기화|그룹|일반적으로 열 머리글|그룹 식|데이터 세트|  
  
 보고서 처리기는 모든 데이터 영역 및 그룹 정렬 식이 적용된 후 대화형 정렬을 적용합니다. 자세한 내용은 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="adding-interactive-sort-for-multiple-groups"></a>여러 그룹에 대한 대화형 정렬 추가  
 단일 데이터 세트 필드 기반의 중첩 행 그룹이 있는 테이블에서 대화형 정렬 단추를 추가하여 부모 그룹 값, 자식 그룹 값 또는 정보 행을 정렬할 수 있습니다. 여러 번 클릭하지 않고도 부모 및 자식 그룹 값 모두를 기준으로 테이블을 정렬할 수 있는 능력을 사용자에게 제공할 수 있습니다.  
  
 이렇게 하려면 여러 필드를 결합하는 식을 그룹화하여 테이블을 다시 디자인해야 합니다. 예를 들어 재고 수가 들어 있는 데이터 세트의 경우 원래 테이블을 크기 및 색 순서로 그룹화하는 경우 크기 및 색을 결합한 그룹 식으로 단일 그룹을 지정할 수 있습니다. 자세한 내용은 [테이블 또는 행렬에 대화형 정렬 추가&#40;보고서 작성기 및 SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 영역의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [테이블 또는 행렬에 대화형 정렬 추가&#40;보고서 작성기 및 SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  
