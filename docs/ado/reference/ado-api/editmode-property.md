---
description: EditMode 속성
title: EditMode 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
author: rothja
ms.author: jroth
ms.openlocfilehash: b6dd04a089d5a28a7eec3b67ebe1c48fe563ff69
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973834"
---
# <a name="editmode-property"></a>EditMode 속성
현재 레코드의 편집 상태를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 [Editmodeenum](../../../ado/reference/ado-api/editmodeenum.md) 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 ADO는 현재 레코드와 연결 된 편집 버퍼를 유지 관리 합니다. 이 속성은이 버퍼가 변경 되었는지 아니면 새 레코드가 생성 되었는지 여부를 나타냅니다. **EditMode** 속성을 사용 하 여 현재 레코드의 편집 상태를 확인 합니다. 편집 프로세스가 중단 된 경우 보류 중인 변경 내용을 테스트 하 고 [Update](../../../ado/reference/ado-api/update-method.md) 또는 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드를 사용 해야 하는지 여부를 결정할 수 있습니다.  
  
 *즉시 업데이트 모드* 에서 **EditMode** 속성은 **업데이트** 메서드 호출이 성공적으로 호출 된 후 **adEditNone** 로 다시 설정 됩니다. 참조 무결성 위반으로 인해 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md) 에 대 한 호출에서 데이터 원본의 레코드를 성공적으로 삭제 하지 못하는 경우에는 [레코드 집합이](../../../ado/reference/ado-api/recordset-object-ado.md) 편집 모드 (**EditMode**  =  **adEditInProgress**)로 유지 됩니다. 따라서 현재 레코드를 밖으로 이동 하기 전에 **CancelUpdate** 를 호출 해야 합니다 (예: [Move](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)또는 [Close](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 *일괄 업데이트 모드* 에서 ( [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드를 호출 하는 경우에만 공급자가 여러 변경 내용을 캐시 하 고 기본 데이터 소스에이를 기록 함) **EditMode** 속성의 값은 첫 번째 작업이 수행 될 때 변경 되 고 **update** 메서드를 호출 하 여 다시 설정 되지 않습니다. 후속 작업은 다른 작업을 수행 하는 경우에도 **EditMode** 속성의 값을 변경 하지 않습니다. 예를 들어 첫 번째 작업이 새 레코드를 추가 하 고 두 번째 작업이 기존 레코드를 변경 하는 경우 **EditMode** 의 속성은 여전히 **adEditAdd**됩니다. **EditMode** 속성은 **UpdateBatch**를 호출할 때까지 **adEditNone** 로 다시 설정 되지 않습니다. 수행 된 작업을 확인 하려면 [필터](../../../ado/reference/ado-api/filter-property.md) 속성을 [adfilterpending](../../../ado/reference/ado-api/filtergroupenum.md) 으로 설정 하 여 보류 중인 변경 내용이 있는 레코드만 표시 하 고 각 레코드의 [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성을 검사 하 여 데이터가 변경 되었는지 확인 합니다.  
  
> [!NOTE]
>  **EditMode** 는 현재 레코드가 있는 경우에만 유효한 값을 반환할 수 있습니다. [BOF 또는 EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 가 True 이면 **EditMode** 는 오류를 반환 하 고, 현재 레코드가 삭제 된 경우에는 오류를 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [CursorType, LockType 및 EditMode 속성 예제 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType 및 EditMode 속성 예제 (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew 메서드 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [CancelUpdate 메서드 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update 메서드](../../../ado/reference/ado-api/update-method.md)
