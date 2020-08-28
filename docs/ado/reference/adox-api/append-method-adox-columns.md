---
description: Append 메서드(ADOX 열)
title: Append 메서드 (ADOX Columns) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c959f6d822724ee6e7480cf00941aaa1fc8012a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985504"
---
# <a name="append-method-adox-columns"></a>Append 메서드(ADOX 열)
[열](./columns-collection-adox.md) 컬렉션에 새 [열](./column-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *열*  
 추가할 **열** 개체 또는 만들고 추가할 열 이름입니다.  
  
 *유형*  
 선택 사항입니다. 열의 데이터 형식을 지정 하는 **Long** 값입니다. *Type* 매개 변수는 **Column** 개체의 [type](./type-property-column-adox.md) 속성에 해당 합니다.  
  
 *DefinedSize*  
 선택 사항입니다. 열의 크기를 지정 하는 **Long** 값입니다. *DefinedSize* 매개 변수는 **Column** 개체의 [DefinedSize](./definedsize-property-adox.md) 속성에 해당 합니다.  
  
> [!NOTE]
>  [테이블](./tables-collection-adox.md) 컬렉션에 이미 추가 된 [테이블](./table-object-adox.md) **에 열이** 없는 경우 [인덱스](./index-object-adox.md) 의 **Columns** 컬렉션에 **열** 을 추가할 때 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Columns 컬렉션(ADOX)](./columns-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](./parentcatalog-property-example-vb.md)   
 [Append 메서드 (ADOX Groups)](./append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](./append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](./append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](./append-method-adox-procedures.md)   
 [Append 메서드 (ADOX Tables)](./append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](./append-method-adox-users.md)   
 [Append 메서드(ADOX 보기)](./append-method-adox-views.md)