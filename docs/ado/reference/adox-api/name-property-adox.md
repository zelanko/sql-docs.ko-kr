---
description: Name 속성(ADOX)
title: Name 속성 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0376017e4ab74822a076379385b4b5ab457afca0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769962"
---
# <a name="name-property-adox"></a>Name 속성(ADOX)
개체의 이름을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **문자열** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 이름은 컬렉션 내에서 고유 하지 않아도 됩니다.  
  
 **Name** 속성은 [Column](./column-object-adox.md), [Group](./group-object-adox.md), [Key](./key-object-adox.md), [Index](./index-object-adox.md), [Table](./table-object-adox.md)및 [User](./user-object-adox.md) 개체에 대 한 읽기/쓰기입니다. **이름** 속성은 [카탈로그](./catalog-object-adox.md), [프로시저](./procedure-object-adox.md)및 [뷰](./view-object-adox.md) 개체에서 읽기 전용입니다.  
  
 읽기/쓰기 개체 (**열**, **그룹**, **키**, **인덱스**, **테이블** 및 **사용자** 개체)의 경우 기본값은 빈 문자열 ("")입니다.  
  
> [!NOTE]
>  키의 경우이 속성은 이미 컬렉션에 추가 된 **키** 개체에 대해 읽기 전용입니다. 테이블의 경우이 속성은 이미 컬렉션에 추가 된 **테이블** 개체에 대해 읽기 전용입니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [열 개체(ADOX)](./column-object-adox.md)  
        [그룹 개체(ADOX)](./group-object-adox.md)  
        [인덱스 개체(ADOX)](./index-object-adox.md)  
    :::column-end:::
    :::column:::
        [키 개체(ADOX)](./key-object-adox.md)  
        [프로시저 개체(ADOX)](./procedure-object-adox.md)  
        [속성 개체(ADO)](../ado-api/property-object-ado.md)  
    :::column-end:::
    :::column:::
        [테이블 개체(ADOX)](./table-object-adox.md)  
        [사용자 개체(ADOX)](./user-object-adox.md)  
        [보기 개체(ADOX)](./view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제(VB)](./parentcatalog-property-example-vb.md)