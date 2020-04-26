---
title: '작업 11: 조건부 분할 변환을 추가 하 여 중복 항목 필터링 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 71b050e49440764d355d4658607600c135741f50
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65476748"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>태스크 11: 조건부 분할 변환을 추가하여 중복 항목 필터링
  이 작업에서는 조건부 분할 변환을 데이터 흐름에 추가합니다. 이 변환은 들어오는 레코드 집합에서 중복 항목을 필터링하는 데 도움이 됩니다. 유사 항목 그룹 변환은 일치하는 것으로 발견된 레코드를 그룹화하고 레코드 중 하나를 피벗 레코드로 선택합니다. 그룹의 모든 레코드는 동일한 _key_out 값을 갖습니다. 그룹의 피벗 레코드는 _key_in 값이 _key_out 값과 동일합니다. 그룹의 다른 레코드는 _key_in 및 _key_out 값이 서로 다릅니다. 따라서 _key_in==_key_out 조건을 사용해서 필터링하면 그룹의 피벗 행만 표시됩니다.  
  
1.  **SSIS 도구 상자** 의 **공통** 섹션에서 **조건부 분할** 변환을 **데이터 흐름** 탭으로 끌어서 놓습니다.  
  
2.  **데이터 흐름** 탭에서 **조건부 분할 변환** 을 마우스 오른쪽 단추로 클릭 하 고 **이름 바꾸기**를 클릭 합니다. **중복 필터** 를 입력 하 고 **enter**키를 누릅니다.  
  
3.  **Id가 일치 하는 그룹 공급자** 를 연결 하 여 **중복 항목을 필터링**합니다.  
  
4.  **중복 필터** 를 두 번 클릭 하 여 **조건부 분할 변환 편집기** 대화 상자를 시작 합니다.  
  
5.  왼쪽 위 창에서 **열** 을 확장 합니다.  
  
6.  **_Key_in** 를 **조건** 열로 끌어서 놓습니다.  
  
7.  **_Key_in** 옆에 = = (같음)를 입력 하 고 **_key_out**을 끌어서 놓습니다.  
  
8.  **출력 이름** 열에서 **Case 1** 을 클릭 하 고 **Unique Records**를 입력 한 다음 **enter**키를 누릅니다.  
  
     ![조건부 분할 변환 편집기](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "조건부 분할 변환 편집기")  
  
9. **확인** 을 클릭 하 여 **조건부 분할 변환 편집기** 대화 상자를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 12: 파생 열 변환을 추가하여 MDS에 필요한 열 추가](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
