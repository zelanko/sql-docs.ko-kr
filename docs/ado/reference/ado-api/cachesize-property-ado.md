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
ms.openlocfilehash: c6b33ef7eb4bae796fa2b2da59a7b1dc805d739e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920339"
---
# <a name="cachesize-property-ado"></a>CacheSize 속성(ADO)
메모리에 로컬로 캐시 된 레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 레코드 수를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 0 보다 커야 하는 **Long** 값을 설정 하거나 반환 합니다. 기본값은 1입니다.  
  
## <a name="remarks"></a>설명  
 **CacheSize** 속성을 사용 하 여 한 번에 공급자의 로컬 메모리로 검색할 레코드 수를 제어 합니다. 예를 들어 **CacheSize** 가 10 이면 먼저 **레코드 집합** 개체를 연 후 공급자는 처음 10 개의 레코드를 로컬 메모리에 검색 합니다. **레코드 집합** 개체를 이동할 때 공급자는 로컬 메모리 버퍼에서 데이터를 반환 합니다. 캐시의 마지막 레코드를 지나서 이동 하는 즉시 공급자는 데이터 원본에서 캐시로 다음 10 개의 레코드를 검색 합니다.  
  
> [!NOTE]
>  **CacheSize** 는 **레코드 집합** 개체의 **Properties** 컬렉션에 있는 **최대 Open Rows** 공급자별 속성을 기반으로 합니다. **CacheSize** 를 **열려 있는 최대 행**보다 큰 값으로 설정할 수 없습니다. 공급자가 열 수 있는 행 수를 수정 하려면 **열려 있는 최대 행**수를 설정 합니다.  
  
 **CacheSize** 의 값은 **레코드 집합** 개체의 수명 동안 조정 될 수 있지만이 값을 변경 하면 이후 데이터 원본에서 데이터를 검색할 때 캐시에 있는 레코드 수에만 영향을 줍니다. 속성 값만 변경 해도 캐시의 현재 콘텐츠는 변경 되지 않습니다.  
  
 검색할 레코드의 개수가 **CacheSize** 에서 지정 하는 것 보다 적으면 공급자는 나머지 레코드를 반환 하 고 오류는 발생 하지 않습니다.  
  
 **CacheSize** 설정 0은 허용 되지 않으며 오류를 반환 합니다.  
  
 캐시에서 검색 된 레코드는 다른 사용자가 원본 데이터에 대해 수행한 동시 변경 내용을 반영 하지 않습니다. 모든 캐시 된 데이터를 강제로 업데이트 하려면 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드를 사용 합니다.  
  
 **CacheSize** 가 1 보다 큰 값으로 설정 된 경우 탐색 메서드 ([Move](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext 및 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md))는 레코드가 검색 된 후 삭제가 발생 하면 삭제 된 레코드를 탐색할 수 있습니다. 초기 인출 후에는 삭제 된 행에서 데이터 값에 액세스 하려고 할 때까지 후속 삭제가 데이터 캐시에 반영 되지 않습니다. 그러나 **CacheSize** 를 one으로 설정 하면 삭제 된 행을 인출할 수 없기 때문에이 문제가 제거 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [CacheSize 속성 예제 (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [CacheSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [CacheSize 속성 예제(JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
