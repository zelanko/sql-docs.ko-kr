---
title: "모두 속성 (ADO) | Microsoft Docs"
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
f1_keywords: Recordset15::CursorType
helpviewer_keywords: CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f1f16755e5030cec19d7b513f725f3fd5defb3f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="cursortype-property-ado"></a>모두 속성 (ADO)
사용 되는 커서 유형을 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) 값입니다. 기본값은 **adOpenForwardOnly**합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **모두** 속성을 열 때 사용 해야 하는 커서의 유형을 지정 하는 **레코드 집합** 개체입니다.  
  
 설정만 **adOpenStatic** 경우 지원 되는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이로 설정 되어 **adUseClient**합니다. 지원 되지 않는 값을 설정 하는 경우 다음 오류가 발생 하지 될 수 있습니다. 가장 가까운 지원 **모두** 대신 사용 됩니다.  
  
 공급자가 요청한 커서 유형을 지원 하지 않습니다, 하는 경우 또 다른 커서 유형을 반환할 수 있습니다. **모두** 속성 실제 커서 유형과 일치 하도록 변경 됩니다 때 사용 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체가 열려 합니다. 반환된 된 커서의 특정 기능을 확인 하려면는 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드. 닫은 후의 **레코드 집합**, **모두** 속성이 원래 설정으로 돌아갑니다.  
  
 다음 차트에는 공급자 기능을 보여 줍니다 (으로 식별 **지원** 메서드 상수) 각 커서 유형에 필요 합니다.  
  
|이 모두의 레코드 집합에 대 한|이러한 상수 중 모든 Supports 메서드가 True 반환 해야 합니다.|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
  
> [!NOTE]
>  하지만 **지원**(**adUpdateBatch**) 일괄 처리 업데이트에 대 한 동적이 고 정방향 전용 커서에 대 한 해당할 수 있습니다는 keyset 또는 static 커서를 사용 해야 합니다. 설정의 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) 속성을 **adLockBatchOptimistic** 및 **앞** 속성을 **adUseClient** 커서를 사용 하도록 설정 하려면 OLE db의 경우 일괄 처리 업데이트에 필요한 서비스입니다.  
  
 **모두** 속성은 읽기/쓰기 때는 **레코드 집합** 열려 있는 경우에 닫힌 이며 읽기 전용입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **레코드 집합** 개체는 **모두** 속성에만 설정할 수 있습니다 **adOpenStatic**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [모두, LockType, 및 EditMode 속성 예제 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [모두, LockType, 및 EditMode 속성 예제 (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports 메서드](../../../ado/reference/ado-api/supports-method.md)
