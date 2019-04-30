---
title: 테이블 컬렉션 (ADOX) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b9ae2422e9d0d3a776bf786f77be5c8c5025d21
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281496"
---
# <a name="tables-collection-adox"></a>Tables 컬렉션(ADOX)
모든 포함 [테이블](../../../ado/reference/adox-api/table-object-adox.md) 카탈로그의 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 [추가](../../../ado/reference/adox-api/append-method-adox-tables.md) 에 대 한 메서드는 **테이블** 컬렉션이 ADOX에 대 한 고유 합니다. 다음 작업을 수행할 수 있습니다.  
  
-   새 테이블을 사용 하 여 컬렉션에 추가 합니다 **Append** 메서드.  
  
 나머지 속성 및 메서드는 ADO 컬렉션에 표준입니다. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 컬렉션의 테이블에 액세스 합니다 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에 포함 된 테이블 수를 반환 합니다 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에서 테이블을 제거 합니다 [삭제](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드.  
  
-   사용 하 여 현재 데이터베이스 스키마를 반영 하 여 컬렉션의 개체를 업데이트 합니다 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
 일부 공급자에는 보기 등의 다른 스키마 개체를 반환할 수 있습니다 합니다 **테이블** 컬렉션입니다. 따라서 일부 ADOX 컬렉션의 동일한 개체에 대 한 여러 참조를 포함할 수 있습니다. 하나의 컬렉션에서 개체를 삭제 해야 합니다는 변경 되지 것입니다 될 때까지 삭제 된 개체를 참조 하는 다른 컬렉션에 표시 합니다 **새로 고침** 메서드는 컬렉션에서 호출 됩니다. 예를 들어 OLE DB Provider for Microsoft Jet을 사용 하 여 뷰는와 함께 반환 된 **테이블** 컬렉션입니다. 뷰를 삭제 하는 경우 새로 고쳐야 합니다 **테이블** 컬렉션 전에 컬렉션에는 변경 내용이 반영 됩니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Tables 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Catalog ActiveConnection 속성 예제 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 메서드, Table Type 속성 예제 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 메서드, 키 유형, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Table 개체(ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
