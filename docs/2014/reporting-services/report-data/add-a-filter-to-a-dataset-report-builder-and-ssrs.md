---
title: 데이터 집합에 필터 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eed37e74-6a43-4d7c-9959-2d5fa6a6aba9
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 404bdf0e092e2123af46cf8832dfceedc7dcc0c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090389"
---
# <a name="add-a-filter-to-a-dataset-report-builder-and-ssrs"></a>데이터 집합에 필터 추가(보고서 작성기 및 SSRS)
  데이터 집합에 필터를 추가하여 데이터를 외부 데이터 원본에서 검색한 후에 보고서의 데이터를 제한합니다. 필터를 데이터 집합에 추가하면 모든 보고서 파트 또는 데이터 영역은 필터 조건과 일치하는 데이터만 사용합니다.  
  
 공유 데이터 집합의 경우 모든 종속 항목에 적용되는 필터는 보고서 서버에 있는 공유 데이터 집합 정의의 일부여야 합니다. 공유 데이터 집합 인스턴스를 포함하는 보고서 또는 보고서 파트는 해당 인스턴스에만 적용되는 필터를 추가로 만들 수 있습니다.  
  
 필터를 추가하려면 하나 이상의 조건(필터 수식)을 지정해야 합니다. 필터 수식은 필터링할 데이터를 식별하는 식, 연산자 및 비교할 값으로 구성됩니다. 필터링된 데이터와 값의 데이터 형식은 일치해야 합니다. 데이터 집합에는 집계 값에 대한 필터링이 지원되지 않습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-filter-to-a-shared-dataset"></a>공유 데이터 집합에 필터를 추가하려면  
  
1.  공유 데이터 집합 모드에서 공유 데이터 집합을 엽니다.  
  
2.  **홈** 탭의 **공유 데이터 집합** 그룹에서 데이터 집합을 클릭합니다. **데이터 집합 속성** 대화 상자가 열립니다.  
  
3.  **필터**를 클릭합니다. 그러면 현재 필터 수식 목록이 표시됩니다. 기본적으로 이 목록은 비어 있습니다.  
  
4.  **추가**를 클릭합니다. 새로운 빈 필터 수식이 나타납니다.  
  
5.  **식**에서 필터링할 필드에 대한 식을 입력하거나 선택합니다. 식을 편집하려면 식(*fx*) 단추를 클릭합니다.  
  
6.  5단계에서 만든 식의 데이터 형식과 일치하는 데이터 형식을 목록 상자에서 선택합니다.  
  
7.  **연산자** 상자에서 해당 필터로 **식** 상자와 **값** 상자의 값을 비교하는 데 사용할 연산자를 선택합니다. 선택한 연산자에 따라 다음 단계에서 사용하는 값의 수가 결정됩니다.  
  
8.  **값** 상자에 해당 필터로 **식**의 값을 계산하는 데 기준이 되는 식 또는 값을 입력합니다.  
  
     필터 수식의 예는 [필터 수식 예&#40;보고서 작성기 및 SSRS&#41;](../report-design/filter-equation-examples-report-builder-and-ssrs.md)를 참조하세요.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-filter-to-an-embedded-dataset-or-a-shared-dataset-instance"></a>포함된 데이터 집합 또는 공유 데이터 집합 인스턴스에 필터를 추가하려면  
  
1.  보고서 디자인 모드에서 보고서를 엽니다.  
  
2.  **보고서 데이터** 창에서 데이터 집합을 마우스 오른쪽 단추로 클릭한 다음 **데이터 집합 속성**을 클릭합니다. **데이터 집합 속성** 대화 상자가 열립니다.  
  
3.  **필터**를 클릭합니다. 그러면 현재 필터 수식 목록이 표시됩니다. 기본적으로 이 목록은 비어 있습니다.  
  
4.  **추가**를 클릭합니다. 새로운 빈 필터 수식이 나타납니다.  
  
5.  **식**에서 필터링할 필드에 대한 식을 입력하거나 선택합니다. 식을 편집하려면 식(*fx*) 단추를 클릭합니다.  
  
6.  5단계에서 만든 식의 데이터 형식과 일치하는 데이터 형식을 드롭다운 상자에서 선택합니다.  
  
7.  **연산자** 상자에서 해당 필터로 **식** 상자와 **값** 상자의 값을 비교하는 데 사용할 연산자를 선택합니다. 선택한 연산자에 따라 다음 단계에서 사용하는 값의 수가 결정됩니다.  
  
8.  **값** 상자에 해당 필터로 **식**의 값을 계산하는 데 기준이 되는 식 또는 값을 입력합니다.  
  
     필터 수식의 예는 [필터 수식 예&#40;보고서 작성기 및 SSRS&#41;](../report-design/filter-equation-examples-report-builder-and-ssrs.md)를 참조하세요.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../report-design/expression-examples-report-builder-and-ssrs.md)   
 [필터 추가&#40;보고서 작성기 및 SSRS&#41;](../report-design/add-a-filter-report-builder-and-ssrs.md)  
  
  