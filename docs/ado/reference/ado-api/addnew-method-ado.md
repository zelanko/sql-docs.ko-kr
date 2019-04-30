---
title: AddNew 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AddNew
- Recordset15::raw_AddNew
helpviewer_keywords:
- AddNew method [ADO]
ms.assetid: a9f54be9-5763-45d0-a6eb-09981b03bc08
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 911509c62c5ae93bc73ca94469ac776195d2a8b1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065273"
---
# <a name="addnew-method-ado"></a>AddNew 메서드(ADO)
업데이트할 수 있는 작업에 대 한 새 레코드를 만듭니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>매개 변수  
 *recordset*  
 A **레코드 집합** 개체입니다.  
  
 *FieldList*  
 (선택 사항) 단일 이름 또는 이름의 배열을 또는 새 레코드에서 필드의 서 수 위치입니다.  
  
 *값*  
 (선택 사항) 단일 값 또는 새 레코드의 필드 값의 배열입니다. 경우 *Fieldlist* 배열이 *값* 배열 해야과 동일한 멤버의 수 고, 그렇지 않으면 오류가 발생 합니다. 필드 이름의 순서는 각 배열에 있는 필드 값의 순서가 일치 해야 합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **AddNew** 메서드를 만들고 새 레코드를 초기화 합니다. 사용 된 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드를 **adAddNew** (을 [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) 값) 현재 레코드를 추가할 수 있는지 여부를 확인 하려면 **레코드집합**개체입니다.  
  
 호출한 후 합니다 **AddNew** 메서드 새 레코드를 현재 레코드가 호출한 후에 현재 상태로 유지 됩니다 합니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드. 때문에 새 레코드가 추가 됩니다는 **레코드 집합**에 대 한 호출 **MoveNext** 끝을 지나서 이동 업데이트를 수행 합니다 **레코드 집합**이면 **EOF**  True입니다. 경우는 **레코드 집합** 개체가 책갈피를 지원 하지 않습니다, 다른 레코드로 이동 되 면 새 레코드에 액세스할 수 있습니다. 커서 유형에 따라 호출 해야 합니다 [Requery](../../../ado/reference/ado-api/requery-method.md) 새 레코드에 액세스할 수 있도록 하는 방법입니다.  
  
 호출 하는 경우 **AddNew** ADO를 호출 하는 현재 레코드를 편집 하는 동안 또는 새 레코드를 추가 하는 동안 합니다 **업데이트** 메서드 하나를 변경 하 고 새 레코드를 만듭니다.  
  
 동작 합니다 **AddNew** 메서드의 업데이트 모드에 따라 달라 집니다 합니다 **레코드 집합** 개체를 전달 하는지 여부를 *Fieldlist* 및 *값*인수.  
  
 *즉시 업데이트 모드* (는 공급자 변경 기록 내부 데이터 소스를 호출 하는 **업데이트** 메서드)를 호출 합니다 **AddNew** 없이 메서드 인수는 [EditMode](../../../ado/reference/ado-api/editmode-property.md) 속성을 **adEditAdd** (프로그램 [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) 값). 공급자 필드 값 변경 내용을 로컬로 캐시합니다. 호출을 **업데이트** 메서드는 데이터베이스에 새 레코드를 게시 하 고 다시 설정 합니다 **EditMode** 속성을 **adEditNone** (을 **EditModeEnum**값). 전달 하는 경우는 *Fieldlist* 하 고 *값* 인수, 게시 데이터베이스에 새 레코드를 즉시 ADO (없습니다 **업데이트** 호출 되기), **EditMode**  속성 값이 변경 되지 않습니다 (**adEditNone**).  
  
 *일괄 업데이트 모드* (공급자는 여러 변경 내용을 캐시 및 호출 된 경우에 기본 데이터 원본에 기록 합니다 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드)를 호출 합니다 **AddNew** 인수 집합이 없는 메서드는 **EditMode** 속성을 **adEditAdd**합니다. 공급자 필드 값 변경 내용을 로컬로 캐시합니다. 호출을 **업데이트** 현재 새 레코드를 추가 하는 메서드 **레코드 집합**, 공급자는 기본 데이터베이스에 변경 내용을 게시 하거나 다시 설정 하지만 합니다 **EditMode** 하 **adEditNone**호출할 때까지, 합니다 **UpdateBatch** 메서드. 전달 하는 경우는 *Fieldlist* 하 고 *값* 인수 ADO 새 레코드 집합 및 캐시 저장소에 대 한 공급자를 보냅니다는 **EditMode** 를 **adEditAdd** ; 호출 해야 합니다 **UpdateBatch** 기본 데이터베이스에 새 레코드를 게시 하는 방법입니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 필드 목록 및 배열 필드 목록 및 값 목록에 포함 하는 방법을 보려면 포함 하는 값 목록을 사용 하 여 AddNew 메서드를 사용 하는 방법을 보여 줍니다.  
  
```  
create table aa1 (intf int, charf char(10))  
insert into aa1 values (2, 'aa')  
  
Dim cn As New adodb.Connection  
Dim rs As New adodb.Recordset  
Dim cmd As New adodb.Command  
  
cn.ConnectionString = "Provider=SQLOLEDB;Data Source=alexverb2;uid=sa;pwd=foo$bar00;"  
  
cn.Open  
rs.Open "select * from xxx..aa1", cn, adOpenKeyset, adLockOptimistic  
  
Dim fieldsArray(1) As Variant  
fieldsArray(0) = "intf"  
fieldsArray(1) = "charf"  
Dim values(1) As Variant  
values(0) = 4  
values(1) = "as"  
rs.AddNew fieldsArray, values  
rs.Update  
```  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [AddNew 메서드 예제 (VB)](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [AddNew 메서드 예제 (VBScript)](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [AddNew 메서드 예제 (VC + +)](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [CancelUpdate 메서드 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 속성](../../../ado/reference/ado-api/editmode-property.md)   
 [Requery 메서드](../../../ado/reference/ado-api/requery-method.md)   
 [메서드를 지원합니다.](../../../ado/reference/ado-api/supports-method.md)   
 [Update 메서드](../../../ado/reference/ado-api/update-method.md)   
 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)
