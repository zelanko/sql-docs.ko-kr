---
title: 레코드 집합에서 이동 하는 방법 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 246e86266622b881402b20d23a8ae12ab6eba0a1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="more-ways-to-move-in-a-recordset"></a>레코드 집합에서 이동 하는 방법
다음 네가지 메서드는, 이동 또는 스크롤할에 하는 데 사용 되는 **레코드 집합**: [MoveFirst, MoveLast, MoveNext 및 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)합니다. (이 중에서 사용할 수 없는 정방향 전용 커서입니다.)  
  
 **MoveFirst** 현재 레코드 위치에 있는 첫 번째 레코드를 변경는 **레코드 집합**합니다. **MoveLast** 변경 내용을 현재 레코드의 마지막 위치에 기록 된 **레코드 집합**합니다. 사용 하도록 **MoveFirst** 또는 **MoveLast**, **레코드 집합** 메서드 호출에서 오류가 발생 하는 그렇지 않은 경우, 개체가 책갈피 또는 역방향 커서 이동을 지원 해야 합니다.  
  
 **MoveNext** 현재 레코드가 위치를 한 곳 앞으로 이동 합니다. 마지막에 있는 경우를 호출 하는 경우 기록 **MoveNext**, **EOF** 로 설정 됩니다 **True**합니다. **MovePrevious** 현재 레코드 위치를 한 곳 뒤로 이동 합니다. 호출 하는 경우 첫 번째 레코드의 않는 **MovePrevious**, **BOF** 로 설정 됩니다 **True**합니다. 확인 하는 것이 좋습니다는 **EOF** 및 **BOF** 이러한 메서드를 사용 하는 경우 속성의 양쪽 끝을 벗어나는 경우 유효한 현재 레코드 위치에 커서를 이동할 수는 **레코드 집합**여기 표시 된 것 처럼:  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 또는의 경우에 **MovePrevious** 메서드:  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 경우에서 위치는 **레코드 집합** 필터링 되거나 정렬 된 현재 레코드의 데이터가 변경 되 고, 위치 변경 될 수 있습니다. 이러한 경우에는 **MoveNext** 메서드가 정상적으로 작동 하지만 하나씩 이동된 위치는 레코드 앞으로 새 위치는 이전 위치가 아니라에서. 예를 들어 현재 레코드의 데이터 변경 레코드는 정렬 된의 끝에 이동 **레코드 집합**, 해당 호출을 의미 하므로 **MoveNext** 현재 레코드 설정 하는 ado에서 결과 마지막 레코드 후 위치는 **레코드 집합** (**EOF** = **True**).  
  
 다양 한 이동 메서드의 동작은 **레코드 집합** 내 데이터에 대해 어느 정도 까지는 개체가 종속 된 **레코드 집합**합니다. 새 레코드에 추가 된 **레코드 집합** 데이터 원본에 의해 정의 되 고 암시적으로 종속 될 수 있습니다는 특정 순서로 또는 명시적으로 새 레코드의 데이터에 추가 됩니다. 조인 정보를 표시 하는 쿼리 내에서 수행 됩니다 정렬 하는 경우에 예를 들어는 **레코드 집합**, 내에서 적절 한 위치에 새 레코드가 삽입 될는 **레코드 집합**합니다. 순서가 지정 되지 않은 경우 명시적으로 만들 때의 **레코드 집합**, 데이터 원본 구현에서 변경 내용을 실수로 변경 하려면 반환 된 행의 순서로 발생할 수 있습니다. 또한, 정렬, 필터링, 및에서는 **레코드 집합** 순서에 영향을 줄 수 있습니다 및 가능한 레코드 집합의 행이 표시 됩니다.  
  
 따라서 **MoveNext**, **MovePrevious**, **MoveFirst**, **MoveLast**, 및 **이동** 는 모두 다른 작업에 민감한 동일한 수행 **레코드 집합**합니다. ADO는 항상 명시적으로 이동, 하지만 경우에 따라 중간 변경은 이후의 이동 작업의 효과 이해 하기 어려울 때까지 현재 위치를 유지 하려고 합니다. 예를 들어, 호출 하는 경우 **MoveFirst** 의 정렬 된 첫 번째 행에 위치를 **레코드 집합** 내림차순 오름차순에서 정렬을 변경 하면, 동일한 행에 여전히 및-이지만 이제 마지막 행 에 **레코드 집합**합니다. **MoveFirst** (새로운 첫 번째 행)의 다른 행으로 이동 합니다.  
  
 또 다른 예로, 가운데 특정 행에 위치 하는 경우는 **레코드 집합** 호출 하면 **삭제** 호출 **MoveNext**, 레코드에 대해 현재 위치는 삭제 된 레코드의 바로 다음 합니다. 하지만 호출 **MovePrevious** 레코드는 삭제 된 레코드를 더 이상의 활성 구성원으로 계산 하므로 현재 레코드를 삭제 하는 한 바로 앞에 **레코드 집합**합니다.  
  
 현재 레코드를 기준으로 이동 하는 방법에 대 한 모든 공급자 일관성 있는 이동 의미 체계를 정의 하기가 특히- **MovePrevious**, **MoveNext**, 및 **이동** -현재 레코드의 데이터를 변경 합니다. 예를 들어, 사용 하는 정렬, 필터링 **레코드 집합**, 및 다른 모든 레코드 앞으로 가도록 있도록 현재 레코드의 데이터를 변경 하지만 변경 된 데이터도 더 이상 일치 필터, where 명확 하지 않습니다는 **MoveNext** 작업 소요 됩니다. 결론적 내에서 해당 상대 이동 되는 **레코드 집합** 은 절대 이동 보다 더 위험 (사용 하는 등 **MoveFirst** 또는 **MoveLast**) 데이터는 경우 변경 레코드를 편집 하는 동안 추가 또는 삭제 합니다. 정렬 및 필터링이 유형의 값을 변경 하지 않아야 하기 때문에 기본 키 또는 ID에 따라 해야 합니다.
