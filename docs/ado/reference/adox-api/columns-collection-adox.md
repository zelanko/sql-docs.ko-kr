---
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
ms.openlocfilehash: 46168e694f87c4a8a827420f8b395b843da1d29b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759339"
---
# <a name="columns-collection-adox"></a>Columns 컬렉션(ADOX)
테이블, 인덱스 또는 키의 모든 [열](../../../ado/reference/adox-api/column-object-adox.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 **Columns** 컬렉션에 대 한 [APPEND](../../../ado/reference/adox-api/append-method-adox-columns.md) 메서드는 ADOX에 대해 고유 합니다. 다음을 수행할 수 있습니다.  
  
-   **Append** 메서드를 사용 하 여 컬렉션에 새 열을 추가 합니다.  
  
 나머지 속성 및 메서드는 ADO 컬렉션의 표준입니다. 다음을 수행할 수 있습니다.  
  
-   [Item](../../../ado/reference/ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션의 열에 액세스 합니다.  
  
-   [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션에 포함 된 열 수를 반환 합니다.  
  
-   [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드를 사용 하 여 컬렉션에서 열을 제거 합니다.  
  
-   [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드를 사용 하 여 현재 데이터베이스의 스키마를 반영 하도록 컬렉션의 개체를 업데이트 합니다.  
  
> [!NOTE]
>  [테이블](../../../ado/reference/adox-api/tables-collection-adox.md) 컬렉션에 이미 추가 된 [테이블](../../../ado/reference/adox-api/table-object-adox.md) **에 열이** 없는 경우 [인덱스](../../../ado/reference/adox-api/index-object-adox.md) 의 **Columns** 컬렉션에 **열** 을 추가할 때 오류가 발생 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Columns 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 메서드, Table Type 속성 예제 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 속성 예제 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Column 개체(ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
