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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa9e680e1626311f2cc10aa7c79fb583841fbc38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920112"
---
# <a name="cancelupdate-method-ado"></a>CancelUpdate 메서드(ADO)
현재 또는 새 행에 대 한 모든 변경 내용을 취소를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 또는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체를 호출 하기 전에 [업데이트 ](../../../ado/reference/ado-api/update-method.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>설명  
  
## <a name="recordset"></a>레코드 집합  
 사용 된 **CancelUpdate** 메서드를 현재 행에 대 한 변경 내용을 취소 하거나 새로 추가 된 행을 삭제 합니다. 호출한 후 새 행을 현재 행에 변경 내용을 취소할 수 없습니다는 **업데이트** 메서드를 변경 내용을 사용 하 여 롤백할 수 있는 트랜잭션의 일부인 경우가 아니면 합니다 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드 또는 파트 일괄 업데이트 합니다. 일괄 업데이트의 경우 취소할 수 있습니다 합니다 **업데이트** 사용 하 여 합니다 **CancelUpdate** 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드.  
  
 호출 하는 경우 새 행을 추가 하는 경우는 **CancelUpdate** 메서드를 현재 행이 행 하기 전에 현재 합니다 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 호출 합니다.  
  
 편집 모드에 있으며 현재 레코드를 이동 하려는 경우 (사용 하 여 예를 들어 합니다 [이동](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md), 또는 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드)를 사용할 수 있습니다  **CancelUpdate** 보류 중인 변경 내용을 취소 합니다. 데이터 원본에 업데이트를 게시할 수 없는 경우이 작업을 수행 해야 합니다. 예를 들어 삭제 참조 무결성 위반으로 인해 실패 하면 종료 됩니다는 **Recordset** 를 호출한 후 편집 모드로 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md).  
  
## <a name="record"></a>녹음  
 **CancelUpdate** 메서드를 삽입 또는 삭제 보류 중인 취소 [필드](../../../ado/reference/ado-api/field-object.md) 개체 및 기존 필드의 보류 중인 업데이트 취소 하 고, 원래 값으로 복원 합니다. 합니다 [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 의 모든 필드의 속성을 **필드** 컬렉션으로 설정 됩니다 **adFieldOK**합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [Update 및 CancelUpdate 메서드 예제 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update 및 CancelUpdate 메서드 예제 (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 메서드 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Cancel 메서드 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 메서드 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 메서드 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [EditMode 속성](../../../ado/reference/ado-api/editmode-property.md)   
 [Update 메서드](../../../ado/reference/ado-api/update-method.md)
