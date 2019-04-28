---
title: LockType 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05670439a8f14018a999557dd135912e0c2e0159
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864099"
---
# <a name="locktype-property-ado"></a>LockType 속성(ADO)
편집 하는 동안 기록에 배치 하는 잠금 유형을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 값입니다. 기본값은 **adLockReadOnly**합니다.  
  
## <a name="remarks"></a>Remarks  
 설정 된 **LockType** 열기 전에 속성을 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 공급자 잠금 유형을 열 때 사용 하도록 지정 하려면. 개방적이 고 사용 중인 잠금 형식을 반환 하도록 속성을 읽습니다 **레코드 집합** 개체입니다.  
  
 공급자는 모든 잠금 유형을 지원 하지 않습니다. 공급자가 요청한 지원할 수 없습니다 **LockType** 설정을 대체 합니다 다른 잠금 유형입니다. 사용할 수 있는 실제 잠금 기능을 확인 하는 **레코드 집합** 개체를 사용 합니다 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드 **adUpdate** 및 **adUpdateBatch**.  
  
 **adLockPessimistic** 경우에 설정은 지원 되지 않습니다는 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이로 설정 되어 **adUseClient**합니다. 지원 되지 않는 값을 설정 하는 경우 없음 오류가 발생 합니다. 지원 되는 가장 가까운 **LockType** 대신 사용 됩니다.  
  
 **LockType** 속성은 읽기/쓰기 경우 합니다 **레코드 집합** 열려 있는 경우에 닫힌 이며 읽기 전용입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용 되 면 **레코드 집합** 개체를 **LockType** 속성 설정할 수 있습니다 **adLockBatchOptimistic**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [CursorType, LockType, EditMode 속성 예제 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType, EditMode 속성 예제 (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)
