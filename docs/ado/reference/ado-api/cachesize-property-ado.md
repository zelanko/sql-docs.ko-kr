---
title: CacheSize 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f5824141f57838f676b2e1af3e3e9c4f3041648b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718098"
---
# <a name="cachesize-property-ado"></a>CacheSize 속성(ADO)
레코드 수가 표시를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 메모리에 로컬로 캐시 된 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환을 **긴** 0 보다 커야 하는 값입니다. 기본값은 1입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **CacheSize** 공급자에서 로컬 메모리에 한 번에 검색할 레코드 수를 제어 하는 속성입니다. 예를 들어 경우는 **CacheSize** 가 10 이면 처음 연 후 합니다 **레코드 집합** 로컬 메모리로 처음 10 개의 레코드를 검색 하는 공급자 개체입니다. 여기저기로 이동 하면 합니다 **레코드 집합** 개체 공급자는 로컬 메모리 버퍼에서 데이터를 반환 합니다. 캐시에 있는 마지막 레코드를 통과 하는 즉시 캐시로 다음 10 개의 레코드를 데이터 원본에서 검색 공급자입니다.  
  
> [!NOTE]
>  **CacheSize** 기반으로 **최대 열린 행** 공급자별 속성 (에 **속성** 의 컬렉션을 **레코드 집합** 개체). 설정할 수 없습니다 **CacheSize** 보다 큰 값으로 **최대 열린 행**합니다. 설정 공급자가 열 수 있는 행의 수를 수정 하려면 **최대 열린 행**합니다.  
  
 변수의 **CacheSize** 의 수명 동안 조정할 수 있습니다 합니다 **레코드 집합** 있으 나이 값을 변경만 영향을 캐시에 있는 레코드 수가 데이터 원본에서 후속 검색 후 합니다. 단독으로 속성 값을 변경 하는 경우에 캐시의 현재 내용을 변경 되지 않습니다.  
  
 검색할 보다 적은 레코드가 없으면 **CacheSize** 공급자 나머지 레코드를 반환 하며 오류가 발생 하지 않습니다 지정 합니다.  
  
 A **CacheSize** 설정으로 0 허용 되지 않으며 오류를 반환 합니다.  
  
 캐시에서 검색 된 레코드에는 다른 사용자에 게 원본 데이터에 대 한 동시 변경 내용을 반영 하지 않습니다. 캐시 된 모든 데이터의 업데이트를 적용 하려면 사용 합니다 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드.  
  
 하는 경우 **CacheSize** 탐색 방법 1 보다 큰 값으로 설정 됩니다 ([이동](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext 및 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md))에 대 한 탐색 될 수 있습니다는 삭제 된 레코드를 가져온 후 발생 하는 경우 레코드를 삭제 합니다. 초기 fetch를 후 후속 삭제 반영 되지 않습니다 데이터 캐시의 삭제 된 행의 데이터 값에 액세스 하려고 할 때 까지는 합니다. 그러나 설정 **CacheSize** 삭제 된 행을 가져올 수 없으므로 하나로이 문제를 제거 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [CacheSize 속성 예제 (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [CacheSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [CacheSize 속성 예제(JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
