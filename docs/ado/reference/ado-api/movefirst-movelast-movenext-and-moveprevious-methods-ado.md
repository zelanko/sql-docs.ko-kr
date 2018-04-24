---
title: MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO) | Microsoft Docs
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
apitype: COM
f1_keywords:
- Recordset15::MoveLast
- Recordset15::MoveNext
- Recordset15::raw_MoveNext
- Recordset15::raw_MovePrevious
- Recordset15::MoveFirst
- Recordset15::raw_MoveLast
- Recordset15::MovePrevious
- Recordset15::raw_MoveFirst
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- MovePrevious method [ADO]
ms.assetid: a61a01a7-5b33-4150-9126-21dfa63654cb
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5803eb0c9c10c0bb4e62cc32b0f341b7ba06c32f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)
첫 번째, 마지막으로 이동의 지정 된 다음 또는 이전 레코드 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체와 현재 레코드로 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **MoveFirst** 의 첫 번째 레코드를 현재 레코드 위치를 이동 하는 메서드는 **레코드 집합**합니다.  
  
 사용 하 여는 **MoveLast** 에 기록 된 마지막 레코드의 현재 위치를 이동 하는 메서드는 **레코드 집합**합니다. **레코드 집합** 메서드 호출에서 오류가 발생 하는 그렇지 않은 경우, 개체가 책갈피 또는 역방향 커서 이동을 지원 해야 합니다.  
  
 에 대 한 호출 **MoveFirst** 또는 **MoveLast** 때는 **레코드 집합** 비어 (둘 다 **BOF** 및 **EOF** True) 오류가 발생 합니다.  
  
 사용 하 여는 **MoveNext** 현재 레코드를 이동 하는 메서드 앞으로 하나의 레코드의 위치 (맨는 **레코드 집합**). 마지막 레코드는 현재 레코드를 호출 하는 **MoveNext** 메서드, ADO 설정 된 위치 뒤의 마지막 레코드의 **레코드 집합** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 은 **True**). 경우에 앞으로 이동 하려고는 **EOF** 속성이 이미 **True** 오류가 발생 합니다.  
  
 ADO의 경우에 2.5 이상는 **레코드 집합** 필터링 된 하거나 정렬 하 고 호출 현재 레코드의 데이터가 변경 되는 **MoveNext** 메서드는 현재 레코드에서 두 커서 레코드 앞으로 이동 . 현재 레코드가 변경 되 면 다음 레코드로 새 현재 레코드가 때문입니다. 호출 **MoveNext** 변경 새 현재 레코드에서 커서 한 레코드 앞으로 이동 되 면입니다. 이 ADO 2.1에서에서와에서 다를 이전 버전. 이러한 초기 버전로 변경 되는 데이터 정렬 또는 필터의 현재 레코드의 **레코드 집합** 현재 레코드의 위치를 변경 하지 않는 및 **MoveNext** 커서를 다음 레코드로 이동 현재 레코드가 직후.  
  
 사용 하 여는 **MovePrevious** 현재 레코드를 이동 하는 메서드 뒤로 한 레코드의 위치 (위쪽으로 **레코드 집합**). **레코드 집합** 메서드 호출에서 오류가 발생 하는 그렇지 않은 경우, 개체가 책갈피 또는 역방향 커서 이동을 지원 해야 합니다. 첫 번째 레코드는 현재 레코드 경우 호출 하면는 **MovePrevious** 메서드, ADO 현재 레코드의 첫 번째 레코드 앞으로 설정 된 **레코드 집합** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)은 **True**). 경우에 뒤로 이동 하려는 시도가 **BOF** 속성이 이미 **True** 오류가 발생 합니다. 경우는 **레코드 집합** 개체가 책갈피나 역방향 커서 이동을 지원 하지 않습니다는 **MovePrevious** 메서드는 오류가 생성 됩니다.  
  
 경우는 **레코드 집합** 만 전달 되며 앞 이나 뒤로 스크롤을 지원 하려면 사용할 수 있습니다는 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 속성을 지 원하는 이전 버전과 커서 움직임 레코드 캐시를 만들려면 통해는 [이동](../../../ado/reference/ado-api/move-method-ado.md) 메서드. 캐시 된 레코드는 메모리에 로드 하기 때문에 필요한 것 보다 많은 레코드를 캐시 하지 않아야 합니다. 호출할 수 있습니다는 **MoveFirst** 정방향 전용의 메서드에서 **레코드 집합** 개체가; 그러면 생성 되는 명령을 다시 실행 하도록 공급자에 발생할 수 있습니다는 **레코드 집합** 개체 .  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 예제 (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 방법 예 (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 예제 (VC + +)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move 메서드 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
