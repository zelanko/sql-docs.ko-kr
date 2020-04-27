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
ms.openlocfilehash: e5f0cdacc6e0d7e5512dbc259815e5b9562c9b68
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918117"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)
지정 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에서 첫 번째, 마지막, 다음 또는 이전 레코드로 이동 하 고이 레코드를 현재 레코드로 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>설명  
 **MoveFirst** 메서드를 사용 하 여 현재 레코드 위치를 **레코드 집합**의 첫 번째 레코드로 이동 합니다.  
  
 **MoveLast** 메서드를 사용 하 여 현재 레코드 위치를 **레코드 집합**의 마지막 레코드로 이동 합니다. **레코드 집합** 개체는 책갈피 또는 역방향 커서 이동을 지원 해야 합니다. 그렇지 않으면 메서드 호출에서 오류를 발생 시킵니다.  
  
 **레코드 집합이** 비어 있을 때 **MoveFirst** 또는 **MoveLast** 를 호출 하는 경우 ( **BOF** 와 **EOF** 모두 True) 오류를 생성 합니다.  
  
 **MoveNext** 메서드를 사용 하 여 현재 레코드 위치를 레코드 **집합**의 아래쪽으로 앞으로 이동 합니다. 마지막 레코드가 현재 레코드이 고 **MoveNext** 메서드를 호출 하는 경우 ADO는 현재 레코드를 **레코드 집합** 에서 마지막 레코드의 위치 ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 가 **True**임)로 설정 합니다. **EOF** 속성이 이미 **True** 인 경우 앞으로 이동 하려고 하면 오류가 생성 됩니다.  
  
 ADO 2.5 이상에서 **레코드 집합** 을 필터링 하거나 정렬 하 고 현재 레코드의 데이터를 변경 하면 **MoveNext** 메서드를 호출 하 여 현재 레코드에서 앞으로 커서 두 개의 레코드를 이동 합니다. 현재 레코드가 변경 되 면 다음 레코드가 새 현재 레코드가 됩니다. 변경 후 **MoveNext** 를 호출 하면 새 현재 레코드에서 커서가 한 레코드에서 앞으로 이동 합니다. 이는 ADO 2.1 이전 버전의 동작과 다릅니다. 이러한 이전 버전에서 정렬 되거나 필터링 된 **레코드 집합** 의 현재 레코드에 대 한 데이터를 변경 해도 현재 레코드의 위치는 변경 되지 않으며 **MoveNext** 는 커서를 현재 레코드 바로 뒤의 다음 레코드로 이동 합니다.  
  
 **MovePrevious** 메서드를 사용 하 여 현재 레코드 위치를 레코드 **집합**의 위쪽으로 뒤로 이동 합니다. **레코드 집합** 개체는 책갈피 또는 역방향 커서 이동을 지원 해야 합니다. 그렇지 않으면 메서드 호출에서 오류를 발생 시킵니다. 첫 번째 레코드가 현재 레코드이 고 **MovePrevious** 메서드를 호출 하는 경우 ADO는 현재 레코드를 **레코드 집합** 의 첫 번째 레코드 앞의 위치로 설정 합니다 ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 가 **True**임). **BOF** 속성이 이미 **True 이면** 뒤로 이동 하려고 하면 오류가 생성 됩니다. **레코드 집합** 개체가 책갈피 또는 역방향 커서 이동을 지원 하지 않는 경우 **MovePrevious** 메서드는 오류를 생성 합니다.  
  
 **레코드 집합이** 앞 으로만 표시 되 고 앞으로 스크롤 및 뒤로 스크롤을 모두 지원 하려는 경우 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 속성을 사용 하 여 [Move](../../../ado/reference/ado-api/move-method-ado.md) 메서드를 통한 역방향 커서 이동을 지 원하는 레코드 캐시를 만들 수 있습니다. 캐시 된 레코드는 메모리에 로드 되기 때문에 필요한 것 보다 많은 레코드를 캐시 하지 않는 것이 좋습니다. 앞 으로만 이동 가능한 **레코드 집합** 개체에서 **MoveFirst** 메서드를 호출할 수 있습니다. 이렇게 하면 공급자가 **레코드 집합** 개체를 생성 한 명령을 다시 실행할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 예제 (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 예제 (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 예제 (VC + +)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move 메서드 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
