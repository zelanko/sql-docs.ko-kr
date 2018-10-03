---
title: CursorType 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fb037216c851a869cb19013a37fccd48145f284
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789681"
---
# <a name="cursortype-property-ado"></a>CursorType 속성(ADO)
사용 되는 커서의 유형을 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) 값입니다. 기본값은 **adOpenForwardOnly**합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 합니다 **CursorType** 속성을 열 때 사용 해야 하는 커서의 유형을 지정 하는 **레코드 집합** 개체입니다.  
  
 설정만 **adOpenStatic** 경우 지원 되는 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이로 설정 되어 **adUseClient**합니다. 지원 되지 않는 값을 설정 하는 경우 없음 오류가 발생 합니다. 지원 되는 가장 가까운 **CursorType** 대신 사용 됩니다.  
  
 공급자를 요청한 커서 유형을 지원 하지 않는, 경우 또 다른 커서 유형을 반환할 수 있습니다. 합니다 **CursorType** 속성이 실제 커서 유형과 일치 하도록 변경 됩니다 때 사용 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체가 열려 합니다. 반환된 된 커서의 특정 기능을 확인 하려면 사용 합니다 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드. 닫은 후 합니다 **레코드 집합**의 **CursorType** 속성이 원래 설정으로 되돌립니다.  
  
 다음 차트에는 공급자 기능을 보여 줍니다 (구분 **지원** 메서드 상수) 각 커서 유형에 대해 필요 합니다.  
  
|이 CursorType의 레코드 집합|Supports 메서드는 모두 이러한 상수에 대 한 True 반환 해야 합니다.|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
  
> [!NOTE]
>  하지만 **지원**(**adUpdateBatch**) 일괄 처리 업데이트에 대 한 동적이 고 정방향 전용 커서에 대 한 일 수는 keyset 또는 static 커서를 사용 해야 합니다. 설정 된 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) 속성을 **adLockBatchOptimistic** 하며 **CursorLocation** 속성을 **adUseClient** 커서를 사용 하도록 설정 하려면 OLE DB에 대 한 일괄 처리 업데이트에 필요한 서비스입니다.  
  
 **CursorType** 속성은 읽기/쓰기 경우 합니다 **레코드 집합** 열려 있는 경우에 닫힌 이며 읽기 전용입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용 되 면 **레코드 집합** 개체를 **CursorType** 속성에만 설정할 수 있습니다 **adOpenStatic**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [CursorType, LockType, EditMode 속성 예제 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType, EditMode 속성 예제 (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports 메서드](../../../ado/reference/ado-api/supports-method.md)
