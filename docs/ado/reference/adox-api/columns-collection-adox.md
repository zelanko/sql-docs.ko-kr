---
description: Columns 컬렉션(ADOX)
title: Columns 컬렉션 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c0e37715077af500e0c5cc023021765a9e4978d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770982"
---
# <a name="columns-collection-adox"></a>Columns 컬렉션(ADOX)
테이블, 인덱스 또는 키의 모든 [열](./column-object-adox.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 **Columns** 컬렉션에 대 한 [APPEND](./append-method-adox-columns.md) 메서드는 ADOX에 대해 고유 합니다. 다음을 수행할 수 있습니다.  
  
-   **Append** 메서드를 사용 하 여 컬렉션에 새 열을 추가 합니다.  
  
 나머지 속성 및 메서드는 ADO 컬렉션의 표준입니다. 다음을 수행할 수 있습니다.  
  
-   [Item](../ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션의 열에 액세스 합니다.  
  
-   [Count](../ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션에 포함 된 열 수를 반환 합니다.  
  
-   [Delete](./delete-method-adox-collections.md) 메서드를 사용 하 여 컬렉션에서 열을 제거 합니다.  
  
-   [Refresh](../ado-api/refresh-method-ado.md) 메서드를 사용 하 여 현재 데이터베이스의 스키마를 반영 하도록 컬렉션의 개체를 업데이트 합니다.  
  
> [!NOTE]
>  [테이블](./tables-collection-adox.md) 컬렉션에 이미 추가 된 [테이블](./table-object-adox.md) **에 열이** 없는 경우 [인덱스](./index-object-adox.md) 의 **Columns** 컬렉션에 **열** 을 추가할 때 오류가 발생 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Columns 컬렉션 속성, 메서드 및 이벤트](./columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 메서드, Table Type 속성 예제 (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](./parentcatalog-property-example-vb.md)   
 [SortOrder 속성 예제 (VB)](./sortorder-property-example-vb.md)   
 [열 개체(ADOX)](./column-object-adox.md)