---
title: 개체 (ADOX) 인덱스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b6fca30201a93b84f59e9356c5201e1070053d5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63311784"
---
# <a name="index-object-adox"></a>인덱스 개체(ADOX)
데이터베이스 테이블에서 인덱스를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 다음 코드를 만듭니다 **인덱스**:  
  
```  
Dim obj As New Index  
```  
  
 속성 및 컬렉션을 **인덱스** 개체를 할 수 있습니다.  
  
-   사용 하 여 인덱스를 식별 합니다 [이름을](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   사용 하 여 인덱스의 데이터베이스 열에 액세스 합니다 [열](../../../ado/reference/adox-api/columns-collection-adox.md) 컬렉션입니다.  
  
-   인덱스 키 내에서 고유 해야 하는지 여부를 지정 합니다 [Unique](../../../ado/reference/adox-api/unique-property-adox.md) 속성입니다.  
  
-   인덱스 테이블의 기본 키인지 여부를 지정 합니다 [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) 속성입니다.  
  
-   인덱스 필드에 null 값이 있는 레코드와 인덱스 항목이 있는지 여부를 지정 합니다 [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) 속성입니다.  
  
-   인덱스와 클러스터형 인지 여부를 지정 합니다 [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) 속성입니다.  
  
-   공급자별 인덱스 속성에 액세스 합니다 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
> [!NOTE]
>  추가할 때 오류가 발생 합니다는 [열](../../../ado/reference/adox-api/column-object-adox.md) 에 **열** 의 컬렉션은 **인덱스** 경우를 **열** 를 에존재하지않는[테이블](../../../ado/reference/adox-api/table-object-adox.md) 개체에 이미 추가 된 [테이블](../../../ado/reference/adox-api/tables-collection-adox.md) 컬렉션입니다.  
  
> [!NOTE]
>  데이터 공급자의 모든 속성을 지원 하지 않을 수 있습니다 **인덱스** 개체입니다. 공급자가 지원 되지 않는 속성의 값을 사용 하도록 설정한 경우 오류가 발생 합니다. 새로운 **인덱스** 개체는 개체 컬렉션에 추가할 때 오류가 발생 합니다. 기존 개체에 대 한 속성을 설정할 때 오류가 발생 합니다.  
  
> [!NOTE]
>  만들면 **인덱스** 개체 선택적 속성에 대 한 적절 한 기본값이 있는지 공급자 속성을 지원 하도록 보장 하지 않습니다. 공급자에서 지원 되는 속성에 대 한 자세한 내용은 공급자 설명서를 참조 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Index 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Indexes Append 메서드 예제 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [IndexNulls 속성 예제 (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey 및 Unique 속성 예제 (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [SortOrder 속성 예제 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Indexes 컬렉션 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
