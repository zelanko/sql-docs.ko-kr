---
title: Move 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d76f239094185af7a3e940201b3f99132c0194a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918192"
---
# <a name="move-method-ado"></a>Move 메서드(ADO)
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에서 현재 레코드의 위치를 이동 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>매개 변수  
 *NumRecords*  
 현재 레코드 위치가 이동 하는 레코드 수를 지정 하는 부호 있는 **Long** 식입니다.  
  
 *시작*  
 (선택 사항) 책갈피를 반환 하는 **문자열** 값 또는 **변형** 입니다. [책갈피 열거형](../../../ado/reference/ado-api/bookmarkenum.md) 값을 사용할 수도 있습니다.  
  
## <a name="remarks"></a>설명  
 **Move** 메서드는 모든 **레코드 집합** 개체에서 지원 됩니다.  
  
 *NumRecords* 인수가 0 보다 크면 현재 레코드 위치가 앞으로 이동 합니다 ( **레코드 집합**의 끝까지). *NumRecords* 가 0 보다 작은 경우에는 현재 레코드 위치가 뒤로 이동 하 여 **레코드 집합**의 시작 부분을 향해 이동 합니다.  
  
 **이동** 호출로 인해 현재 레코드 위치가 첫 번째 레코드 앞의 지점으로 이동 하는 경우 ADO는 현재 레코드를 레코드 집합의 첫 번째 레코드 앞의 위치로 설정 합니다 ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 가 **True**임). **BOF** 속성이 이미 **True 이면** 뒤로 이동 하려고 하면 오류가 생성 됩니다.  
  
 **이동** 호출로 인해 현재 레코드 위치가 마지막 레코드 다음의 지점으로 이동 하는 경우 ADO는 현재 레코드를 레코드 집합에서 마지막 레코드의 위치 ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 가 **True**임)로 설정 합니다. **EOF** 속성이 이미 **True** 인 경우 앞으로 이동 하려고 하면 오류가 생성 됩니다.  
  
 빈 **레코드 집합** 개체에서 **Move** 메서드를 호출 하면 오류가 발생 합니다.  
  
 *Start* 인수를 전달 하는 경우 레코드 **집합** 개체가 책갈피를 지원 한다고 가정 하 고이 책갈피를 사용 하는 레코드를 기준으로 이동 합니다. 지정 하지 않으면 현재 레코드를 기준으로 이동 합니다.  
  
 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 속성을 사용 하 여 공급자의 레코드를 로컬로 캐시 하는 경우 현재 레코드 위치를 캐시 된 레코드의 현재 그룹 외부로 이동 하는 *NumRecords* 인수를 전달 하면 ADO에서 대상 레코드부터 시작 하 여 새 레코드 그룹을 검색 합니다. **CacheSize** 속성은 새로 검색 된 그룹의 크기를 결정 하 고, 대상 레코드는 검색 된 첫 번째 레코드입니다.  
  
 **레코드 집합** 개체가 앞 으로만 사용 되는 경우 사용자는 현재 캐시 된 레코드 집합 내에 있는 경우에도 0 보다 작은 *NumRecords* 인수를 전달할 수 있습니다. **이동** 호출로 인해 현재 레코드 위치가 첫 번째 캐시 된 레코드 이전의 레코드로 이동 하는 경우 오류가 발생 합니다. 따라서 전방 스크롤만 지 원하는 공급자를 통해 전체 스크롤을 지 원하는 레코드 캐시를 사용할 수 있습니다. 캐시 된 레코드는 메모리에 로드 되기 때문에 필요한 것 보다 많은 레코드를 캐시 하지 않는 것이 좋습니다. 앞 으로만 이동 가능한 **레코드 집합** 개체가 이러한 방식으로 뒤로 이동 하는 것을 지원 하더라도 앞 으로만 이동 가능한 **레코드 집합** 개체에 대해 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 메서드를 호출 해도 오류가 발생 합니다.  
  
> [!NOTE]
>  전달 전용 **레코드 집합** 에서 뒤로 이동 하는 기능은 공급자에 따라 예측할 수 없습니다. 현재 레코드를 **레코드 집합**의 마지막 레코드 뒤에 배치 하는 경우 뒤로 **이동** 하 여 올바른 현재 위치를 얻지 못할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Move 메서드 예제 (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Move 메서드 예제 (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Move 메서드 예제 (VC + +)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
