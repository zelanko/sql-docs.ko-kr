---
title: "CacheSize 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::CacheSize
helpviewer_keywords: CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 57ac5e367e3dd9181dcdbde260b04917d30453ee
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="cachesize-property-ado"></a>CacheSize 속성 (ADO)
레코드 수를 나타내는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 메모리에 로컬로 캐시 된 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **긴** 0 보다 커야 하는 값입니다. 기본값은 1입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **CacheSize** 레코드를 공급자에서 로컬 메모리에 한 번에 가져올 수를 제어 하는 속성입니다. 예를 들어 경우는 **CacheSize** 은 10, 첫 번째 여는 **레코드 집합** 개체 공급자는 로컬 메모리에 처음 10 개의 레코드를 검색 합니다. 이동할 때는 **레코드 집합** 개체 공급자는 로컬 메모리 버퍼에서 데이터를 반환 합니다. 캐시에 있는 마지막 레코드를 지 나 이동 공급자 다음 10 개의 레코드를 캐시에에 데이터 원본에서 검색 합니다.  
  
> [!NOTE]
>  **CacheSize** 기반으로 **최대 열린 행** 공급자별 속성 (에 **속성** 의 컬렉션은 **레코드 집합** 개체). 설정할 수 없습니다. **CacheSize** 보다 큰 값으로 **최대 열린 행**합니다. 공급자에서 열 수 있는 행의 수를 수정 하려면 설정 **최대 열린 행**합니다.  
  
 값 **CacheSize** 의 수명 동안 조정 될 수 있습니다는 **레코드 집합** 개체가 아니라이 값을 변경만 영향을 미칩니다 캐시에 있는 레코드 수가 데이터 원본에서 발생 한 후속 검색 후 합니다. 단독 속성 값을 변경 하는 경우에 캐시의 현재 내용을 변경 되지 않습니다.  
  
 검색할 보다 더 적은 레코드 없으면 **CacheSize** 지정 공급자 나머지 레코드를 반환 하 고 오류가 발생 하지 않습니다.  
  
 A **CacheSize** 설정 0는 허용 되지 않으며 오류를 반환 합니다.  
  
 캐시에서 검색 된 레코드는 다른 사용자가 원본 데이터에 동시 변경 내용을 반영 하지 않습니다. 모든 캐시 된 데이터의 업데이트를 적용 하려면 사용 된 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드.  
  
 경우 **CacheSize** 탐색 방법 1 보다 큰 값으로 설정 됩니다 ([이동](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext 및 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) 탐색을 발생할 수 있습니다는 삭제 된 레코드를 가져온 후 발생 하는 경우 레코드를 삭제 합니다. 초기 인출 후 후속 삭제 반영 되지 않습니다 데이터 캐시에서 삭제 된 행의 데이터 값에 액세스 하려고 합니다. 그러나 설정 **CacheSize** 삭제 된 행을 가져올 수 없으므로 하나에이 문제를 제거 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [CacheSize 속성 예제 (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [CacheSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [CacheSize 속성 예제(JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
