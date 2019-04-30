---
title: MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 905fc532057a827f30735efe067464f488f51dc0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242907"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)
첫 번째, 마지막으로 이동의 지정 된 다음 또는 이전 레코드 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체와 현재 레코드로 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>Remarks  
 사용 합니다 **MoveFirst** 레코드 현재 위치에서 첫 번째 레코드를 이동 하는 방법의 **레코드 집합**합니다.  
  
 사용 하 여는 **MoveLast** 마지막 레코드의 현재 위치를 이동 하는 방법에 기록 합니다 **레코드 집합**합니다. 합니다 **레코드 집합** 메서드 호출에서 오류를 생성 하는 고, 그렇지 않으면 개체는 책갈피 또는 이전 버전과 커서 이동을 지원 해야 합니다.  
  
 가 호출 **MoveFirst** 또는 **MoveLast** 때의 **레코드 집합** 비어 (둘 다 **BOF** 하 고 **EOF** True) 오류를 생성 합니다.  
  
 사용 하 여는 **MoveNext** 현재 레코드를 이동 하는 메서드 앞으로 하나의 레코드를 배치 합니다 (아래쪽 합니다 **레코드 집합**). 마지막 레코드를 현재 레코드가 고 호출 하는 경우는 **MoveNext** 메서드를 ADO 설정 된 위치 뒤에 있는 마지막 레코드를 **레코드 집합** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 는 **True**). 경우에 앞으로 이동 하려고 합니다 **EOF** 속성이 이미 **True** 오류를 생성 합니다.  
  
 Ado에서 2.5 이상 경우 합니다 **레코드 집합** 필터링 된 정렬 및 현재 레코드의 데이터가 변경 되 면 호출 합니다 **MoveNext** 현재 레코드에서 전달 커서 두 레코드를 이동 하는 메서드 . 현재 레코드가 변경 되 면 다음 레코드 새 현재 레코드가 때문입니다. 호출 **MoveNext** 후 변경 내용을 새 현재 레코드에서 커서 한 레코드 앞으로 이동 합니다. 이것이 ADO 2.1의에서 동작과 다릅니다 및 이전 버전입니다. 이러한 이전 버전에서는 정렬 또는 필터링에서 현재 레코드의 데이터를 변경 **Recordset** 현재 레코드의 위치를 변경 하지 않습니다 하 고 **MoveNext** 커서를 다음 레코드로 이동 현재 레코드 직후.  
  
 사용 된 **MovePrevious** 현재 레코드를 이동 하는 방법은 이전 버전과 하나의 레코드의 위치 (위쪽으로 **레코드 집합**). 합니다 **레코드 집합** 메서드 호출에서 오류를 생성 하는 고, 그렇지 않으면 개체는 책갈피 또는 이전 버전과 커서 이동을 지원 해야 합니다. 첫 번째 레코드에는 현재 레코드가 고 호출 하는 경우는 **MovePrevious** 메서드를 ADO 현재 레코드에서 첫 번째 레코드 앞의 위치를 설정 합니다 **레코드 집합** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)됩니다 **True**). 이전 버전과 경우 이동 하려고 합니다 **BOF** 속성은 이미 **True** 오류를 생성 합니다. 경우는 **레코드 집합** 책갈피 또는 이전 버전과 커서 이동 개체가 지원 하지 않습니다는 **MovePrevious** 메서드는 오류가 생성 됩니다.  
  
 경우는 **레코드 집합** 정방향 전용 이며 앞으로 및 뒤로 스크롤을 지원 하려면 사용할 수는 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 속성을 이전 버전과 커서 이동에서 지원 되는 레코드 캐시 만들기 통해 합니다 [이동](../../../ado/reference/ado-api/move-method-ado.md) 메서드. 캐시 된 레코드는 메모리에 로드 되므로, 필요한 것 보다 많은 레코드를 캐시 하지 마십시오. 호출할 수 있습니다는 **MoveFirst** 메서드를 정방향 전용 **레코드 집합** 개체; 공급자를 다시 생성 하는 명령을 실행할 않을 이렇게 합니다 **레코드 집합** 개체 .  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 예제 (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 예제 (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 예제 (VC + +)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move 메서드 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
