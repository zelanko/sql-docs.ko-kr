---
title: "테이블 컬렉션 (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords: Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c47b8088fa5603de7bd8b17d784100170388509c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="tables-collection-adox"></a>테이블 컬렉션 (ADOX)
모든 포함 [테이블](../../../ado/reference/adox-api/table-object-adox.md) 카탈로그의 개체가 있습니다.  
  
## <a name="remarks"></a>주의  
 [Append](../../../ado/reference/adox-api/append-method-adox-tables.md) 에 대 한 메서드는 **테이블** 컬렉션이 ADOX에 대해 고유 합니다. 다음 작업을 수행할 수 있습니다.  
  
-   새 테이블을 사용 하 여 컬렉션에 추가 **Append** 메서드.  
  
 나머지 속성 및 메서드는 표준 ADO 컬렉션으로. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 컬렉션의 테이블에 액세스는 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에 포함 된 테이블 수를 반환 된 [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   테이블을 사용 하 여 컬렉션에서 제거 된 [삭제](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드.  
  
-   현재 데이터베이스 스키마와 반영 하기 위해 컬렉션의 개체를 업데이트 하는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
 일부 공급자에는 보기와 같은 다른 스키마 개체를 반환할 수 있습니다는 **테이블** 컬렉션입니다. 따라서 일부 ADOX 컬렉션에 동일한 개체에 대 한 여러 참조가 포함 될 수 있습니다. 하나의 컬렉션에서 개체를 삭제 해야 하면, 변경 내용을 볼 수 없게 됩니다 될 때까지 삭제 된 개체를 참조 하는 다른 컬렉션에는 **새로 고침** 메서드는 컬렉션에서 호출 됩니다. 예를 들어 OLE DB Provider for Microsoft Jet와 뷰 반환 됩니다는 **테이블** 컬렉션입니다. 뷰를 삭제 하는 경우 새로 고쳐야는 **테이블** 컬렉션 전에 컬렉션에는 변경 내용이 반영 됩니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Tables 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 ActiveConnection 속성 예제 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [테이블 및 열 이름 속성 예제 (VB) 메서드 추가](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [테이블 형식 속성 예제 (VB) 연결 Close 메서드](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [키 추가 방법, 키 형식, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [카탈로그 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Table 개체(ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
