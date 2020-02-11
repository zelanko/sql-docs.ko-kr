---
title: Append 메서드 (ADOX Columns) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6493157c00e5a71c7c2f085191231bb33bb5279a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967329"
---
# <a name="append-method-adox-columns"></a>Append 메서드(ADOX 열)
[열](../../../ado/reference/adox-api/columns-collection-adox.md) 컬렉션에 새 [열](../../../ado/reference/adox-api/column-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *열*  
 추가할 **열** 개체 또는 만들고 추가할 열 이름입니다.  
  
 *형식*  
 (선택 사항) 열의 데이터 형식을 지정 하는 **Long** 값입니다. *Type* 매개 변수는 **Column** 개체의 [type](../../../ado/reference/adox-api/type-property-column-adox.md) 속성에 해당 합니다.  
  
 *DefinedSize*  
 (선택 사항) 열의 크기를 지정 하는 **Long** 값입니다. *DefinedSize* 매개 변수는 **Column** 개체의 [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) 속성에 해당 합니다.  
  
> [!NOTE]
>  [테이블](../../../ado/reference/adox-api/tables-collection-adox.md) 컬렉션에 이미 추가 된 [테이블](../../../ado/reference/adox-api/table-object-adox.md) **에 열이** 없는 경우 [인덱스](../../../ado/reference/adox-api/index-object-adox.md) 의 **Columns** 컬렉션에 **열** 을 추가할 때 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Columns 컬렉션(ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append 메서드 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX 보기)](../../../ado/reference/adox-api/append-method-adox-views.md)
