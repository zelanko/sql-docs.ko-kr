---
title: LockType 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35d413ea9bfaded1494270d837f433fc9546e0b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="locktype-property-ado"></a>LockType 속성 (ADO)
편집 중 레코드에 적용 되는 잠금 유형을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 값입니다. 기본값은 **adLockReadOnly**합니다.  
  
## <a name="remarks"></a>주의  
 설정의 **LockType** 속성 열기 전에 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 를 열 때 사용 해야 하는 공급자 잠금 유형을 지정 합니다. 열린에서 사용 중인 잠금 유형을 반환 하려면 속성을 읽을 **레코드 집합** 개체입니다.  
  
 공급자는 일부 잠금 유형을 지원 하지 않습니다. 공급자가 요청 된 지원할 수 없는 **LockType** 설정, 다른 잠금 유형으로 대체 될 것입니다. 사용할 수 있는 실제 잠금 기능을 확인 하는 **레코드 집합** 개체를 가져오려면는 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드 **adUpdate** 및 **adUpdateBatch**.  
  
 **adLockPessimistic** 경우 설정을 지원 하지 않습니다는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이 **adUseClient**합니다. 지원 되지 않는 값을 설정 하는 경우 다음 오류가 발생 하지 될 수 있습니다. 가장 가까운 지원 **LockType** 대신 사용 됩니다.  
  
 **LockType** 속성은 읽기/쓰기 때는 **레코드 집합** 열려 있는 경우에 닫힌 이며 읽기 전용입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **레코드 집합** 개체는 **LockType** 속성 설정할 수 있습니다 **adLockBatchOptimistic**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [모두, LockType, 및 EditMode 속성 예제 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [모두, LockType, 및 EditMode 속성 예제 (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)
