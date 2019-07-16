---
title: 레코드 집합에서 이동 하는 방법은 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ea83f40c6d6e595277a173c181c24f33e382393
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924885"
---
# <a name="more-ways-to-move-in-a-recordset"></a>레코드 집합에서 이동하는 추가 방법
다음 네 가지 방법, 이동 하거나에서 스크롤 되는 **레코드 집합**: [MoveFirst, MoveLast, MoveNext 및 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)합니다. (이러한 메서드 중 일부를 사용할 수 없는 정방향 전용 커서의 경우)  
  
 **MoveFirst** 의 첫 번째 레코드에는 현재 레코드 위치를 변경 합니다 **레코드 집합**합니다. **MoveLast** 변경 내용을 현재 레코드의 마지막 위치에 기록 합니다 **레코드 집합**합니다. 사용 하도록 **MoveFirst** 또는 **MoveLast**의 **레코드 집합** 메서드 호출에서 오류를 생성 하는 고, 그렇지 않으면 개체는 책갈피 또는 이전 버전과 커서 이동을 지원 해야 합니다.  
  
 **MoveNext** 현재 레코드 위치 한곳 앞으로 이동 합니다. 마지막으로 하는 경우 호출 하는 경우 기록 **MoveNext**를 **EOF** 로 설정 됩니다 **True**합니다. **MovePrevious** 현재 레코드를 한 곳의 이전 버전과 위치를 이동 합니다. 호출할 때 첫 번째 레코드의 않는 **MovePrevious**를 **BOF** 로 설정 됩니다 **True**합니다. 확인 하는 것이 좋습니다 합니다 **EOF** 및 **BOF** 이러한 메서드를 사용 하는 경우 속성의 양쪽 끝을 벗어나는 경우 유효한 현재 레코드 위치로 커서를 이동할 수는 **레코드 집합**다음과 같이 합니다.  
  
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
  
 경우에 위치 합니다 **레코드 집합** 정렬 되거나 필터링 된 현재 레코드의 데이터가 변경 되 고 위치 변경 될 수 있습니다. 이러한 경우는 **MoveNext** 메서드가 제대로 작동 하지만 하나씩 이동된 위치 인지 알고 있어야 새 위치를 이전 위치에서 앞으로 기록 합니다. 예를 들어, 현재 레코드의 데이터 변경 레코드를 정렬 된의 끝에 이동 됩니다 **레코드 집합**를 호출 하는 것은 의미 **MoveNext** 현재 레코드 설정 하는 ado에서 결과 마지막 레코드 다음 위치를 **Recordset** (**EOF** = **True**).  
  
 다양 한 이동 방법의 동작을 **레코드 집합** 내 데이터에 대해 어느 정도 까지는 개체가 종속 합니다 **레코드 집합**합니다. 새 레코드를 추가 합니다 **레코드 집합** 또는 명시적으로 새 레코드의 데이터를 데이터 소스에 의해 정의 되 고 암시적으로 종속 될 수 있습니다 특정 순서로 처음에 추가 됩니다. 조인 채우는 쿼리 내에서 수행 됩니다을 정렬 하는 경우에 예를 들어를 **레코드 집합**, 내에서 적절 한 위치에 삽입 될 새 레코드를 **레코드 집합**. 순서 지정 하지 않으면 명시적으로 만들면 합니다 **레코드 집합**, 데이터 원본 구현에 대 한 변경 내용을 실수로 변경 하려면 반환된 된 행의 순서 지정이 발생할 수 있습니다. 추가, 정렬, 필터링 및 함수를 편집 합니다 **레코드 집합** 순서에 영향을 줄 수 있으며 가능한 경우 레코드 집합의 행 표시 되지 것입니다.  
  
 따라서 **MoveNext**, **MovePrevious**합니다 **MoveFirst**를 **MoveLast**, 및 **이동** 는 모두 동일한 다른 작업에 중요 한 수행 **레코드 집합**합니다. ADO는 항상 명시적으로 이동, 경우에 따라 중간 변경 하기가 어려울 이후의 이동 작업의 효과 이해 될 때까지 현재 위치를 유지 하려고 합니다. 예를 들어, 호출 하는 경우 **MoveFirst** 첫 번째 행의 정렬 된 위치로 **Recordset** 및 정렬 순서를 내림차순으로 오름차순에서 변경, 여전히 동일한 행에 있는 이지만 이제 마지막 행 에 **레코드 집합**합니다. **MoveFirst** 다른 행 (새로운 첫 번째 행)로 이동 됩니다.  
  
 또 다른 예로, 특정 행의 가운데에 배치 하는 경우는 **레코드 집합** 호출 하면 **삭제** 호출 **MoveNext**, 레코드에서 이제는 즉시 삭제 된 레코드를 수행 합니다. 하지만 호출 **MovePrevious** 레코드 삭제 된 레코드를 더 이상의 활성 구성원으로 계산 하므로 현재 레코드를 삭제 하는 것을 바로 앞에 **Recordset**합니다.  
  
 -현재 레코드를 기준으로 이동 하는 방법에 대 한 모든 공급자에서 일관성 있는 이동 의미 체계를 정의 하는 것이 어려운 것 **MovePrevious**하십시오 **MoveNext**, 및 **이동** -현재 레코드의 데이터를 변경 합니다. 정렬 된를 사용 하 여 작업 하는 경우 필터링 하는 예를 들어 **레코드 집합**, 및 다른 모든 레코드는 앞으로는 현재 레코드의 데이터를 변경 하면 변경 된 데이터도 더 이상 필터와 일치 하지만 where 확실 하지 않은 한 **MoveNext** 작업을 완료 해야 합니다. 결론적 내에서 해당 상대 이동 되는 **레코드 집합** 는 절대 이동 보다 더 위험 (사용 하는 등 **MoveFirst** 또는 **MoveLast**) 데이터의 경우 변경 레코드를 편집 하는 동안 추가 또는 삭제 합니다. 정렬 및 필터링이 형식의 값을 변경 하지 않아야 하기 때문에 기본 키 또는 ID에 따라 합니다.
