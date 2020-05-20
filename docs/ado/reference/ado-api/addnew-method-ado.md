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
author: rothja
ms.author: jroth
ms.openlocfilehash: a6359d1b9f69963120e9446c47aa5473beedd127
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760729"
---
# <a name="addnew-method-ado"></a>AddNew 메서드(ADO)
업데이트할 수 있는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에 대 한 새 레코드를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>매개 변수  
 *집합인*  
 **레코드 집합** 개체입니다.  
  
 *FieldList*  
 (선택 사항) 단일 이름 이거나 새 레코드에 있는 필드의 이름 또는 서 수 위치 배열입니다.  
  
 *값*  
 (선택 사항) 단일 값 또는 새 레코드의 필드에 대 한 값의 배열입니다. *Fieldlist)* 가 배열인 경우 *값* 도 멤버 수가 같은 배열 이어야 합니다. 그렇지 않으면 오류가 발생 합니다. 필드 이름의 순서는 각 배열에서 필드 값의 순서와 일치 해야 합니다.  
  
## <a name="remarks"></a>설명  
 **AddNew** 메서드를 사용 하 여 새 레코드를 만들고 초기화 합니다. **Adaddnew** ( [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) 값)와 함께 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드를 사용 하 여 현재 **레코드 집합** 개체에 레코드를 추가할 수 있는지 여부를 확인 합니다.  
  
 **AddNew** 메서드를 호출 하면 새 레코드가 현재 레코드가 되며 [Update](../../../ado/reference/ado-api/update-method.md) 메서드를 호출한 후에는 현재 레코드가 됩니다. 새 레코드가 **레코드 집합**에 추가 되기 때문에 업데이트 다음에 오는 **MoveNext** 호출은 **레코드 집합**의 끝을 지나서 이동 하 여 **EOF** True로 설정 됩니다. **레코드 집합** 개체가 책갈피를 지원 하지 않는 경우에는 다른 레코드로 이동 하는 동안 새 레코드에 액세스 하지 못할 수 있습니다. 커서 유형에 따라 [Requery](../../../ado/reference/ado-api/requery-method.md) 메서드를 호출 하 여 새 레코드를 액세스할 수 있도록 해야 할 수도 있습니다.  
  
 현재 레코드를 편집 하는 동안 **AddNew** 를 호출 하거나 새 레코드를 추가 하는 동안 ADO에서 **Update** 메서드를 호출 하 여 변경 내용을 저장 한 다음 새 레코드를 만듭니다.  
  
 **AddNew** 메서드의 동작은 **레코드 집합** 개체의 업데이트 모드와 *fieldlist)* 및 *Values* 인수를 전달 하는지 여부에 따라 달라 집니다.  
  
 **업데이트** 메서드를 호출 하면 공급자가 기본 데이터 소스에 변경 내용을 쓰는 *즉시 업데이트 모드* 에서 인수 없이 **AddNew** 메서드를 호출 하면 [EditMode](../../../ado/reference/ado-api/editmode-property.md) 속성이 **adEditAdd** ( [editmodeenum](../../../ado/reference/ado-api/editmodeenum.md) 값)로 설정 됩니다. 공급자는 필드 값 변경 내용을 로컬로 캐시 합니다. **Update** 메서드를 호출 하면 새 레코드가 데이터베이스에 게시 되 고 **EditMode** 속성이 **adEditNone** ( **editmodeenum** 값)로 다시 설정 됩니다. *Fieldlist)* 및 *Values* 인수를 전달 하는 경우 ADO는 새 레코드를 데이터베이스에 즉시 게시 합니다 ( **업데이트** 호출이 필요 하지 않음). **EditMode** 속성 값은 변경 되지 않습니다 (**adEditNone**).  
  
 *일괄 업데이트 모드* 에서 ( [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드를 호출 하는 경우에만 공급자가 여러 변경 내용을 캐시 하 고 기본 데이터 소스에 쓰도록 함), 인수 없이 **AddNew** 메서드를 호출 하면 **EditMode** 속성이 **adEditAdd**로 설정 됩니다. 공급자는 필드 값 변경 내용을 로컬로 캐시 합니다. **Update** 메서드를 호출 하면 새 레코드가 현재 **레코드 집합**에 추가 되지만, 공급자는 **UpdateBatch** 메서드를 호출할 때까지 기본 데이터베이스에 변경 내용을 게시 하거나 **EditMode** 를 **adEditNone**로 다시 설정 하지 않습니다. *Fieldlist)* 및 *Values* 인수를 전달 하는 경우 ADO는 캐시에 저장 하기 위해 새 레코드를 공급자에 게 보내고 **EditMode** 를 **adEditAdd**로 설정 합니다. 새 레코드를 기본 데이터베이스에 게시 하려면 **UpdateBatch** 메서드를 호출 해야 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 필드 목록 및 값 목록을 포함 하는 AddNew 메서드를 사용 하 여 필드 목록 및 값 목록을 배열로 포함 하는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [AddNew 메서드 예제 (VB)](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [AddNew 메서드 예제 (VBScript)](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [AddNew 메서드 예제 (VC + +)](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [CancelUpdate 메서드 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 속성](../../../ado/reference/ado-api/editmode-property.md)   
 [Requery 메서드](../../../ado/reference/ado-api/requery-method.md)   
 [지원 메서드](../../../ado/reference/ado-api/supports-method.md)   
 [Update 메서드](../../../ado/reference/ado-api/update-method.md)   
 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)
