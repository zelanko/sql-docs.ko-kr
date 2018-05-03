---
title: 인덱스를 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a79307fb344ae5b3a7a65b12b960008688ca7304
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="index-object-adox"></a>Index 개체 (ADOX)
데이터베이스 테이블에서 인덱스를 나타냅니다.  
  
## <a name="remarks"></a>주의  
 다음 코드에서는 새 **인덱스**:  
  
```  
Dim obj As New Index  
```  
  
 속성과 컬렉션을 사용 하 여 프로그램 **인덱스** 개체를 할 수 있습니다.  
  
-   사용 하 여 인덱스를 식별 된 [이름](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   데이터베이스 열에 사용 하 여 인덱스의 액세스는 [열](../../../ado/reference/adox-api/columns-collection-adox.md) 컬렉션입니다.  
  
-   인덱스 키에서 고유 해야 하는지 여부를 지정 된 [Unique](../../../ado/reference/adox-api/unique-property-adox.md) 속성입니다.  
  
-   인덱스 있는 테이블에 대 한 기본 키를 지정 된 [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) 속성입니다.  
  
-   인덱스 필드에 null 값이 포함 된 레코드와 인덱스 항목이 있는지 여부를 지정할는 [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) 속성입니다.  
  
-   인덱스와 클러스터형 인지 여부를 지정 된 [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) 속성입니다.  
  
-   공급자 관련 인덱스 속성을 액세스는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
> [!NOTE]
>  추가할 때 오류가 발생 합니다는 [열](../../../ado/reference/adox-api/column-object-adox.md) 에 **열** 컬렉션은 **인덱스** 경우는 **열** 는 에존재하지않는[테이블](../../../ado/reference/adox-api/table-object-adox.md) 에 이미 연결 된 개체는 [테이블](../../../ado/reference/adox-api/tables-collection-adox.md) 컬렉션입니다.  
  
> [!NOTE]
>  데이터 공급자의 모든 속성을 지원 하지 않을 수 있습니다 **인덱스** 개체입니다. 공급자가 지원 되지 않는 속성에 대 한 값을 사용 하도록 설정한 경우 오류가 발생 합니다. 새 **인덱스** 개체는 개체 컬렉션에 추가할 때 오류가 발생 합니다. 기존 개체에 대 한 속성을 설정할 때 오류가 발생 합니다.  
  
> [!NOTE]
>  만들 때 **인덱스** 개체의 경우에 선택적 속성에 대 한 적절 한 기본값이 있는지 공급자 속성을 지원 하도록 보장 하지 않습니다. 공급자에서 지원 되는 속성에 대 한 자세한 내용은 공급자 설명서를 참조 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Index 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [인덱스 추가 (VB) 메서드 예제](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [IndexNulls 속성 예제 (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey 및 고유한 속성 예제 (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [SortOrder 속성 예제 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [인덱스 컬렉션 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
