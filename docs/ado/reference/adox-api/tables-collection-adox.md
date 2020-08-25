---
description: Tables 컬렉션(ADOX)
title: Tables 컬렉션 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
author: rothja
ms.author: jroth
ms.openlocfilehash: 001472bd748d0821beae62801b889024cb699022
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769262"
---
# <a name="tables-collection-adox"></a>Tables 컬렉션(ADOX)
카탈로그의 모든 [테이블](./table-object-adox.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 **Tables** 컬렉션에 대 한 [APPEND](./append-method-adox-tables.md) 메서드는 ADOX에 대해 고유 합니다. 다음을 수행할 수 있습니다.  
  
-   **Append** 메서드를 사용 하 여 컬렉션에 새 테이블을 추가 합니다.  
  
 나머지 속성 및 메서드는 ADO 컬렉션의 표준입니다. 다음을 수행할 수 있습니다.  
  
-   [Item](../ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션의 테이블에 액세스 합니다.  
  
-   [Count](../ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션에 포함 된 테이블 수를 반환 합니다.  
  
-   [Delete](./delete-method-adox-collections.md) 메서드를 사용 하 여 컬렉션에서 테이블을 제거 합니다.  
  
-   [Refresh](../ado-api/refresh-method-ado.md) 메서드를 사용 하 여 현재 데이터베이스 스키마를 반영 하도록 컬렉션의 개체를 업데이트 합니다.  
  
 일부 공급자는 **Tables** 컬렉션에서 뷰와 같은 다른 스키마 개체를 반환할 수 있습니다. 따라서 일부 ADOX 컬렉션에는 동일한 개체에 대 한 여러 참조가 포함 될 수 있습니다. 한 컬렉션에서 개체를 삭제 하는 경우 컬렉션에 대해 **Refresh** 메서드가 호출 될 때까지 삭제 된 개체를 참조 하는 다른 컬렉션에는 변경 내용이 표시 되지 않습니다. 예를 들어 Microsoft Jet 용 OLE DB 공급자를 사용 하는 경우 뷰는 **Tables** 컬렉션과 함께 반환 됩니다. 뷰를 삭제 하는 경우 컬렉션에 변경 내용이 반영 되기 전에 **Tables** 컬렉션을 새로 고쳐야 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Tables 컬렉션 속성, 메서드 및 이벤트](./tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Catalog ActiveConnection 속성 예제 (VB)](./catalog-activeconnection-property-example-vb.md)   
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 메서드, Table Type 속성 예제 (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [테이블 개체(ADOX)](./table-object-adox.md)