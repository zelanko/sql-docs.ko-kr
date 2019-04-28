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
manager: craigg
ms.openlocfilehash: c8306a7d8e3247e77579d0bebc9147c3f9a1cc56
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62863490"
---
# <a name="move-method-ado"></a>Move 메서드(ADO)
현재 레코드의 위치를 이동 하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>매개 변수  
 *NumRecords*  
 Signed **긴** 현재 레코드 위치 이동 하는 레코드의 수를 지정 하는 식입니다.  
  
 *시작*  
 (선택 사항) A **문자열** 값 또는 **Variant** 책갈피로 계산 되는 합니다. 사용할 수도 있습니다는 [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) 값입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **이동** 메서드는 모든 지원 **레코드 집합** 개체입니다.  
  
 경우는 *NumRecords* 인수가 0 보다 큰 레코드의 현재 위치를 앞으로 이동 (의 끝에 다가가 합니다 **Recordset**). 하는 경우 *NumRecords* 가 현재 레코드 위치 뒤로 이동 0 보다 작은 (의 시작 부분을 향해 합니다 **레코드 집합**).  
  
 경우는 **이동** 호출에서 현재 레코드 위치 첫 번째 레코드 앞의 위치를 이동, ADO 레코드 집합의 첫 번째 레코드 앞의 위치는 현재 레코드를 설정 합니다 ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 는 **True** ). 이전 버전과 경우 이동 하려고 합니다 **BOF** 속성은 이미 **True** 오류를 생성 합니다.  
  
 경우는 **이동** ADO 레코드 집합의 마지막 레코드 다음 위치에 현재 레코드를 설정, 호출 지점에 마지막 레코드 다음에 현재 레코드 위치를 이동 합니다 ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 는 **True** ). 경우에 앞으로 이동 하려고 합니다 **EOF** 속성이 이미 **True** 오류를 생성 합니다.  
  
 호출을 **이동** 빈 메서드에서 **레코드 집합** 개체에 오류가 발생 합니다.  
  
 전달 하는 경우는 *시작* 인수에이 책갈피를 사용 하 여 레코드를 기준으로 이동 가정 합니다 **레코드 집합** 개체에서 책갈피를 지원 합니다. 지정 하지 않으면 현재 레코드를 기준으로 이동 합니다.  
  
 사용 중인 경우는 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 로컬로 전달 공급자에서 레코드를 캐시 하는 속성을 *NumRecords* 그룹 외부의 현재 캐시 된 레코드의 현재 레코드 위치를 이동 하는 인수 대상 레코드에서 시작 하는 레코드의 새 그룹을 검색 하는 ADO를 강제로 수행 합니다. 합니다 **CacheSize** 새로 검색된 된 그룹의 크기를 결정 하는 속성 및 대상 레코드는 첫 번째 레코드를 검색 합니다.  
  
 경우는 **레코드 집합** 개체는 앞으로, 사용자에 게 전달할 수도 있습니다는 *NumRecords* 인수는 0 보다 작은 대상이 현재 캐시 된 레코드 집합 내에서 제공 합니다. 경우는 **이동** 호출 레코드의 현재 위치를 이동 전에 캐시 된 첫 번째 레코드는 레코드 오류가 발생 합니다. 따라서 앞 으로만 스크롤을 지 원하는 공급자를 통해 전체 스크롤을 지 원하는 레코드 캐시를 사용할 수 있습니다. 캐시 된 레코드는 메모리에 로드 되므로, 필요한 것 보다 많은 레코드를 캐시 하지 마십시오. 정방향 전용 하는 경우에 **레코드 집합** 호출 이전 버전과 개체에서는 이러한 방식으로 이동 합니다 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 에서 메서드 앞 으로만 이동 가능한 **레코드 집합** 개체는 계속 해 서 오류가 발생 합니다.  
  
> [!NOTE]
>  정방향 전용 뒤로 이동 하는 것에 대 한 지원을 **레코드 집합** 는 공급자에 따라 예측할 수 없습니다. 현재 레코드의 마지막 레코드 다음 배치 된 경우는 **Recordset**를 **이동** 이전 버전과 올바른 현재 위치에서 발생 하지 않을 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Move 메서드 예제 (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Move 메서드 예제 (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Move 메서드 예제 (VC + +)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
