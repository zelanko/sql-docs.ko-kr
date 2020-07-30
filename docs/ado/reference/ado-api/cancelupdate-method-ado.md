---
title: CancelUpdate 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ecc08dde974826846058d4d8927df202367d28d
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242410"
---
# <a name="cancelupdate-method-ado"></a>CancelUpdate 메서드(ADO)
[Update](../../../ado/reference/ado-api/update-method.md) 메서드를 호출 하기 전에 레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 현재 행 또는 새 행 또는 [Record](../../../ado/reference/ado-api/record-object-ado.md) 개체의 [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 대 한 변경 내용을 취소 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>설명  
  
## <a name="recordset"></a>레코드 집합  
 **CancelUpdate** 메서드를 사용 하 여 현재 행에 대 한 변경 내용을 취소 하거나 새로 추가 된 행을 삭제할 수 있습니다. [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드를 사용 하 여 롤백할 수 있는 트랜잭션 또는 일괄 처리 업데이트의 일부를 변경 하지 않는 한 **Update** 메서드를 호출한 후에는 현재 행 또는 새 행에 대 한 변경 내용을 취소할 수 없습니다. 일괄 처리 업데이트의 경우 **CancelUpdate** 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드를 사용 하 여 **업데이트** 를 취소할 수 있습니다.  
  
 **CancelUpdate** 메서드를 호출할 때 새 행을 추가 하는 경우 현재 행은 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 호출 이전의 현재 행이 됩니다.  
  
 편집 모드에 있고 현재 레코드 (예: [move](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)또는 [Close](../../../ado/reference/ado-api/close-method-ado.md) 메서드 사용)로 이동 하려는 경우 **CancelUpdate** 를 사용 하 여 보류 중인 변경 내용을 취소할 수 있습니다. 업데이트를 데이터 원본에 성공적으로 게시할 수 없는 경우이 작업을 수행 해야 할 수 있습니다. 예를 들어 참조 무결성 위반으로 인해 실패 하는 삭제 시도는 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md)를 호출한 후에도 **레코드 집합** 을 편집 모드로 유지 합니다.  
  
## <a name="record"></a>레코드  
 **CancelUpdate** 메서드는 보류 중인 모든 [필드](../../../ado/reference/ado-api/field-object.md) 개체 삽입 또는 삭제를 취소 하 고 기존 필드의 보류 중인 업데이트를 취소 하 여 원래 값으로 복원 합니다. **Fields** 컬렉션에 있는 모든 필드의 [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성은 **adFieldOK**로 설정 됩니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [Update 및 CancelUpdate 메서드 예제 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update 및 CancelUpdate 메서드 예제 (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 메서드 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Cancel 메서드 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 메서드 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 메서드 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [EditMode 속성](../../../ado/reference/ado-api/editmode-property.md)   
 [Update 메서드](../../../ado/reference/ado-api/update-method.md)
