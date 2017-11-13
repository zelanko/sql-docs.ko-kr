---
title: "Name 속성 (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Table::PutName
- _Table::GetName
- _Key::Name
- _Key::get_Name
- _Column::GetName
- _Index::Name
- _Index::put_Name
- _Column::PutName
- _Key::put_Name
- _Table::put_Name
- _User25::PutName
- _Index::get_Name
- _Column::get_Name
- _Group25::Name
- _Group25::get_Name
- _Column::Name
- _User25::get_Name
- _Table::Name
- _Group25::GetName
- _Index::PutName
- _Column::put_Name
- _Key::GetName
- _Table::get_Name
- _User25::Name
- _User25::put_Name
- _Index::GetName
- _User25::GetName
helpviewer_keywords:
- Name property [ADOX]
ms.assetid: 81b92baf-b6b9-4f4e-9f33-4503795518cd
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 96a4d83770ee986c781efb9859eb071d197b112c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="name-property-adox"></a>Name 속성 (ADOX)
개체의 이름을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **문자열** 값입니다.  
  
## <a name="remarks"></a>주의  
 이름은은 컬렉션 내에서 고유할 필요가 없습니다.  
  
 **이름** 속성은 읽기/쓰기 [열](../../../ado/reference/adox-api/column-object-adox.md), [그룹](../../../ado/reference/adox-api/group-object-adox.md), [키](../../../ado/reference/adox-api/key-object-adox.md), [인덱스](../../../ado/reference/adox-api/index-object-adox.md), [ 테이블](../../../ado/reference/adox-api/table-object-adox.md), 및 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 개체입니다. **이름** 속성은 읽기 전용 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md), [프로시저](../../../ado/reference/adox-api/procedure-object-adox.md), 및 [보기](../../../ado/reference/adox-api/view-object-adox.md) 개체입니다.  
  
 읽기/쓰기 개체에 대 한 (**열**, **그룹**, **키**, **인덱스**, **테이블** 및  **사용자** 개체), 기본값은 빈 문자열 ("").  
  
> [!NOTE]
>  키의 경우이 속성은 읽기 전용 **키** 컬렉션에 이미 추가 된 개체입니다. 테이블의 경우이 속성은 읽기 전용입니다 **테이블** 컬렉션에 이미 추가 된 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Column 개체(ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Group 개체(ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Index 개체(ADOX)](../../../ado/reference/adox-api/index-object-adox.md)|  
|[Key 개체(ADOX)](../../../ado/reference/adox-api/key-object-adox.md)|[Procedure 개체(ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[속성 개체(ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
|[Table 개체(ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|[View 개체(ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 열 이름 속성 예제 (VB) 메서드 추가](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [키 추가 방법, 키 형식, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제(VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)

