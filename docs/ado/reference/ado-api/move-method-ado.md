---
title: "Move 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 098ef46d9d0e336cb142b29b9b899ec0bcaf2eba
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="move-method-ado"></a>Move 메서드 (ADO)
현재 레코드의 위치를 이동 하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>매개 변수  
 *NumRecords*  
 부호 있는 **긴** 현재 레코드 위치가 이동 하는 레코드의 수를 지정 하는 식입니다.  
  
 *시작*  
 (선택 사항) A **문자열** 값 또는 **Variant** 하는 책갈피를 반환 합니다. 사용할 수도 있습니다는 [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) 값입니다.  
  
## <a name="remarks"></a>주의  
 **이동** 모든 메서드는 지원 **레코드 집합** 개체입니다.  
  
 경우는 *NumRecords* 인수가 0 보다 큰 레코드의 현재 위치를 앞으로 이동 (이 끝날 무렵는 **레코드 집합**). 경우 *NumRecords* 가 현재 레코드 위치 이동 합니다. 0 보다 작은 (의 시작 부분 쪽는 **레코드 집합**).  
  
 경우는 **이동** 호출 현재 레코드 위치는 첫 번째 레코드 앞에 포인터를 이동, ADO 레코드 집합에서 첫 번째 레코드 앞의 위치를 현재 레코드를 설정 합니다 ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 은 **True** ). 경우에 뒤로 이동 하려는 시도가 **BOF** 속성이 이미 **True** 오류가 발생 합니다.  
  
 경우는 **이동** 호출 지점에 마지막 레코드 뒤에 현재 레코드 위치를 이동 합니다, ADO 레코드 집합의 마지막 레코드 다음 위치에 현재 레코드를 설정 ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 은 **True** ). 경우에 앞으로 이동 하려고는 **EOF** 속성이 이미 **True** 오류가 발생 합니다.  
  
 호출 된 **이동** 메서드는 빈에서 **레코드 집합** 개체에 오류가 발생 합니다.  
  
 전달 하는 경우는 *시작* 인수에이 책갈피와 레코드를 기준으로 이동 가정은 **레코드 집합** 개체 책갈피를 지원 합니다. 지정 하지 않으면 현재 레코드를 기준으로 이동 합니다.  
  
 사용 하는 경우는 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 속성을 전달 공급자에서 레코드를 로컬로 캐시 한 *NumRecords* 캐시 된 레코드의 현재 그룹 외부 레코드 현재 위치를 이동 하는 인수 하면 ADO 대상 레코드부터 시작 하는 레코드의 새 그룹을 검색 합니다. **CacheSize** 새로 검색된 된 그룹의 크기를 결정 하는 속성 및 대상 레코드는 검색 된 첫 번째 레코드입니다.  
  
 경우는 **레코드 집합** 개체는 앞으로, 사용자 전달할 수 있습니다는 *NumRecords* 인수는 0 보다 작은 대상이 현재 캐시 된 레코드 집합 내에 제공 합니다. 경우는 **이동** 호출 이동 하므로 현재 레코드 위치 레코드는 첫 번째 캐시 된 레코드 바로 앞에 오류가 발생 합니다. 따라서 스크롤 앞 으로만 지 원하는 공급자를 통해 전체 스크롤을 지 원하는 레코드 캐시를 사용할 수 있습니다. 캐시 된 레코드는 메모리에 로드 하기 때문에 필요한 것 보다 많은 레코드를 캐시 하지 않아야 합니다. 정방향 전용 하는 경우에 **레코드 집합** 호출 이러한 방식으로 개체가 지 원하는 뒤로 이동는 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 메서드에서 앞 으로만 이동 가능한 **레코드 집합** 개체를 계속 오류가 발생 합니다.  
  
> [!NOTE]
>  정방향 전용를 뒤로 이동에 대 한 지원 **레코드 집합** 를 공급자에 따라 예측할 수 없습니다. 현재 레코드의 마지막 레코드 후 배치 된 경우는 **레코드 집합**, **이동** 정확한 현재 위치에서 이전 버전과 발생 하지 않을 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Move 메서드 예제 (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Move 메서드 (VBScript) 예제](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Move 메서드 예제 (VC + +)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
