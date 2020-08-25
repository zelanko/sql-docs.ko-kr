---
description: LockType 속성(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b9211ec3b9c6213ffab8cfc07c8bcf89559240ae
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774582"
---
# <a name="locktype-property-ado"></a>LockType 속성(ADO)
편집 하는 동안 레코드에 적용 되는 잠금 유형을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [LockTypeEnum](./locktypeenum.md) 값을 설정 하거나 반환 합니다. 기본값은 **Adlockreadonly**입니다.  
  
## <a name="remarks"></a>설명  
 [레코드 집합](./recordset-object-ado.md) 을 열기 전에 **LockType** 속성을 설정 하 여 공급자가 열을 열 때 사용 해야 하는 잠금 유형을 지정 합니다. 열려 있는 **레코드 집합** 개체에서 사용 중인 잠금 유형을 반환 하려면 속성을 읽습니다.  
  
 공급자는 일부 잠금 유형을 지원 하지 않을 수 있습니다. 공급자는 요청한 **LockType** 설정을 지원할 수 없는 경우 다른 잠금 유형으로 대체 합니다. **레코드 집합** 개체에서 사용할 수 있는 실제 잠금 기능을 확인 하려면 **Adupdate** 및 **adupdate**에서 [지원](./supports-method.md) 메서드를 사용 합니다.  
  
 [CursorLocation](./cursorlocation-property-ado.md) 속성이 **adUseClient**로 설정 된 경우에는 **adlockpessimistic** 설정이 지원 되지 않습니다. 지원 되지 않는 값이 설정 되 면 오류가 발생 하지 않습니다. 가장 가까운 지원 되는 **LockType** 가 대신 사용 됩니다.  
  
 **LockType** 속성은 **레코드 집합이** 닫혀 있을 때 읽기/쓰기이 고, 열려 있으면 읽기 전용입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **레코드 집합** 개체에서 사용 하는 경우 **LockType** 속성은 **adlockbatchoptimistic**으로만 설정할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [CursorType, LockType 및 EditMode 속성 예제 (VB)](./cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType 및 EditMode 속성 예제 (VC + +)](./cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch 메서드 (ADO)](./cancelbatch-method-ado.md)   
 [UpdateBatch 메서드](./updatebatch-method.md)