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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5cd13809703c14022b6e2a1e7dbb87716c4778c9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600041"
---
# <a name="columns-collection-adox"></a>Columns 컬렉션(ADOX)
모든 포함 [열](../../../ado/reference/adox-api/column-object-adox.md) 테이블, 인덱스 또는 키의 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 [추가](../../../ado/reference/adox-api/append-method-adox-columns.md) 에 대 한 메서드는 **열** 컬렉션이 ADOX에 대 한 고유 합니다. 다음 작업을 수행할 수 있습니다.  
  
-   컬렉션에 새 열을 추가 합니다 **Append** 메서드.  
  
 나머지 속성 및 메서드는 ADO 컬렉션에 표준입니다. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 컬렉션의 열에 액세스 합니다 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에 포함 된 열 개수를 반환 합니다 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에서 열을 제거 합니다 [삭제](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드.  
  
-   현재 데이터베이스의 스키마를 반영 하기 위해 컬렉션의 개체를 업데이트 합니다 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
> [!NOTE]
>  추가할 때 오류가 발생 합니다는 **열** 에 **열** 의 컬렉션은 [인덱스](../../../ado/reference/adox-api/index-object-adox.md) 경우를 **열** 를 에존재하지않는[표](../../../ado/reference/adox-api/table-object-adox.md) 에 이미 추가 된는 [테이블](../../../ado/reference/adox-api/tables-collection-adox.md) 컬렉션입니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Columns 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 메서드, Table Type 속성 예제 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 메서드, 키 유형, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 속성 예제 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Column 개체(ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
