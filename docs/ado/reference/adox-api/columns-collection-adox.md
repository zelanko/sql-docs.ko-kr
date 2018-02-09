---
title: "Columns 컬렉션 (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: afacdd2d86d25382c6026dba8d3deda55d05c99a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="columns-collection-adox"></a>Columns 컬렉션 (ADOX)
모든 포함 [열](../../../ado/reference/adox-api/column-object-adox.md) 테이블, 인덱스 또는 키의 개체입니다.  
  
## <a name="remarks"></a>주의  
 [Append](../../../ado/reference/adox-api/append-method-adox-columns.md) 에 대 한 메서드는 **열** 컬렉션이 ADOX에 대해 고유 합니다. 다음 작업을 수행할 수 있습니다.  
  
-   새 열을 사용 하 여 컬렉션에 추가 **Append** 메서드.  
  
 나머지 속성 및 메서드는 표준 ADO 컬렉션으로. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 컬렉션의 열에 액세스는 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에 포함 된 열 수를 반환 된 [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에서 열 제거는 [삭제](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드.  
  
-   현재 데이터베이스의 스키마를 반영 하기 위해 컬렉션의 개체를 업데이트 하는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
> [!NOTE]
>  추가할 때 오류가 발생 합니다는 **열** 에 **열** 컬렉션은 [인덱스](../../../ado/reference/adox-api/index-object-adox.md) 경우는 **열** 는 에존재하지않는[테이블](../../../ado/reference/adox-api/table-object-adox.md) 이미에 추가 된는 [테이블](../../../ado/reference/adox-api/tables-collection-adox.md) 컬렉션입니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Columns 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 열 이름 속성 예제 (VB) 메서드 추가](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [테이블 형식 속성 예제 (VB) 연결 Close 메서드](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [키 추가 방법, 키 형식, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 속성 예제 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Column 개체(ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
