---
description: 레코드 집합에서 이동하는 추가 방법
title: 여러 가지 방법으로 레코드 집합에서 이동 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e8c668bc24b388d0367429086416cd67b5355550
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980294"
---
# <a name="more-ways-to-move-in-a-recordset"></a>레코드 집합에서 이동하는 추가 방법
다음 네 가지 방법을 사용 하 여 **레코드 집합**에서 이동 하거나 스크롤할 수 있습니다. [MoveFirst, MoveLast, MoveNext 및 MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md). 이러한 메서드 중 일부는 앞 으로만 이동 가능한 커서에서 사용할 수 없습니다.  
  
 **MoveFirst** 는 **레코드 집합**의 첫 번째 레코드에 현재 레코드 위치를 변경 합니다. **MoveLast** 는 현재 레코드 위치를 **레코드 집합**의 마지막 레코드로 변경 합니다. **MoveFirst** 또는 **MoveLast**를 사용 하려면 **레코드 집합** 개체가 책갈피 또는 역방향 커서 이동을 지원 해야 합니다. 그렇지 않으면 메서드 호출에서 오류를 발생 시킵니다.  
  
 **MoveNext** 는 현재 레코드 위치를 앞으로 이동 합니다. **MoveNext**를 호출할 때 마지막 레코드를 사용할 경우 **EOF** 는 **True**로 설정 됩니다. **MovePrevious** 현재 레코드 위치를 한 위치 뒤로 이동 합니다. **MovePrevious**를 호출할 때 첫 번째 레코드를 사용할 경우에는 **BOF** 가 **True**로 설정 됩니다. 이러한 메서드를 사용할 때 **EOF** 및 **BOF** 속성을 확인 하 고 다음과 같이 **레코드 집합**의 끝에서 이동할 경우 커서를 유효한 현재 레코드 위치로 다시 이동 하는 것이 좋습니다.  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 또는 **MovePrevious** 메서드의 경우 다음을 수행 합니다.  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 **레코드 집합** 을 필터링 하거나 정렬 하 고 현재 레코드의 데이터를 변경한 경우 위치가 변경 될 수도 있습니다. 이러한 경우 **MoveNext** 메서드는 정상적으로 작동 하지만 위치는 이전 위치가 아니라 새 위치에서 앞으로 한 레코드를 이동 한다는 점에 주의 해야 합니다. 예를 들어 레코드를 정렬 된 **레코드 집합**의 끝으로 이동 하는 등의 방법으로 현재 레코드의 데이터를 변경 하면 **MoveNext** 를 호출 하면 ADO에서 현재 레코드를 **레코드 집합** 에서 마지막 레코드의 위치 (**EOF**  =  **True**)로 설정 하는 것을 의미 합니다.  
  
 **레코드** 집합 개체에 대 한 다양 한 Move 메서드의 동작은 **레코드 집합**내의 데이터에 대 한 일부 범위에 따라 다릅니다. **레코드 집합** 에 추가 되는 새 레코드는 처음에 데이터 원본에 의해 정의 되 고 새 레코드의 데이터에 대해 암시적 또는 명시적으로 종속 될 수 있는 특정 순서로 추가 됩니다. 예를 들어 **레코드 집합**을 채우는 쿼리 내에서 정렬 또는 조인이 수행 되 면 새 레코드가 **레코드 집합**내의 적절 한 위치로 삽입 됩니다. **레코드 집합**을 만들 때 정렬이 명시적으로 지정 되지 않은 경우에는 데이터 원본 구현의 변경으로 인해 반환 되는 행의 순서가 실수로 변경 될 수 있습니다. 또한 **레코드 집합** 의 정렬, 필터링 및 편집 함수는 순서에 영향을 줄 수 있으며 레코드 집합의 행이 표시 될 수도 있습니다.  
  
 따라서 **MoveNext**, **MovePrevious**, **MoveFirst**, **MoveLast**및 **Move** 는 모두 동일한 **레코드 집합**에서 수행 되는 다른 작업에 영향을 주는 것입니다. ADO는 항상 명시적으로 이동할 때까지 현재 위치를 유지 하려고 시도 하지만 때로는 변경으로 인해 후속 이동의 효과를 이해 하기 어려워집니다. 예를 들어, **MoveFirst** 를 호출 하 여 정렬 된 **레코드 집합** 의 첫 번째 행에 배치 하 고 정렬을 오름차순에서 내림차순으로 변경 하는 경우 여전히 동일한 행에 있지만 이제는 **레코드 집합**의 마지막 행입니다. **MoveFirst** 를 사용 하면 다른 행 (첫 번째 새 행)으로 이동 합니다.  
  
 또 다른 예로, **레코드 집합** 의 중간에 있는 특정 행에 배치 하 고 **Delete** 를 호출한 다음 **MoveNext**를 호출 하는 경우 이제 삭제 된 레코드 바로 다음에 오는 레코드에 있습니다. 하지만 **MovePrevious** 를 호출 하면 삭제 된 레코드가 레코드 **집합**의 활성 멤버 자격에서 더 이상 계산 되지 않기 때문에 이전 레코드는 현재 레코드를 삭제 합니다.  
  
 현재 레코드에서 데이터를 변경 하는 경우에는 현재 레코드- **MovePrevious**, **MoveNext**및 **move** 로 이동 하는 메서드에 대해 모든 공급자에서 일관 된 이동 의미 체계를 정의 하는 것이 특히 어렵습니다. 예를 들어 정렬 된 필터링 된 **레코드 집합**을 사용 하 여 작업 하는 경우 다른 모든 레코드 앞에 오도록 현재 레코드의 데이터를 변경 하지만 변경 된 데이터는 더 이상 필터와 일치 하지 않을 경우 **MoveNext** 작업에서 수행 해야 하는 위치는 명확 하지 않습니다. 가장 안전한 결론은 레코드를 편집, 추가 또는 삭제 하는 동안 데이터를 변경할 때 **레코드 집합** 내의 상대 이동이 절대 이동 (예: **MoveFirst** 또는 **MoveLast**사용) 보다 riskier는 것입니다. 정렬 및 필터링은 기본 키 또는 ID를 기반으로 해야 합니다 .이 값 유형은 변경 하면 안 됩니다.