---
title: Index 개체 (ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 840484cbfcb1feeb56022835b6c1b3157101edb8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763884"
---
# <a name="index-object-adox"></a>인덱스 개체(ADOX)
데이터베이스 테이블의 인덱스를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 다음 코드는 새 **인덱스**를 만듭니다.  
  
```  
Dim obj As New Index  
```  
  
 **인덱스** 개체의 속성 및 컬렉션을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](../../../ado/reference/adox-api/name-property-adox.md) 속성을 사용 하 여 인덱스를 식별 합니다.  
  
-   [Columns](../../../ado/reference/adox-api/columns-collection-adox.md) 컬렉션을 사용 하 여 인덱스의 데이터베이스 열에 액세스 합니다.  
  
-   [고유](../../../ado/reference/adox-api/unique-property-adox.md) 속성을 사용 하 여 인덱스 키를 고유 하 게 지정 해야 하는지 여부를 지정 합니다.  
  
-   인덱스가 [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) 속성이 있는 테이블의 기본 키인지 여부를 지정 합니다.  
  
-   인덱스 필드에 null 값이 있는 레코드에 [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) 속성이 있는 인덱스 항목이 있는지 여부를 지정 합니다.  
  
-   [클러스터형](../../../ado/reference/adox-api/clustered-property-adox.md) 속성을 사용 하 여 인덱스를 클러스터링 할지 여부를 지정 합니다.  
  
-   [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 공급자별 인덱스 속성에 액세스 합니다.  
  
> [!NOTE]
>  열 **이 테이블** [컬렉션에 이미 추가 된](../../../ado/reference/adox-api/tables-collection-adox.md) [테이블](../../../ado/reference/adox-api/table-object-adox.md) 개체에 없는 경우 **인덱스** 의 **Columns** 컬렉션에 [열](../../../ado/reference/adox-api/column-object-adox.md) 을 추가할 때 오류가 발생 합니다.  
  
> [!NOTE]
>  데이터 공급자가 **인덱스** 개체의 일부 속성을 지원 하지 않을 수 있습니다. 공급자가 지원 하지 않는 속성에 대 한 값을 설정 하면 오류가 발생 합니다. 새 **인덱스** 개체의 경우 개체가 컬렉션에 추가 되 면 오류가 발생 합니다. 기존 개체의 경우 속성을 설정할 때 오류가 발생 합니다.  
  
> [!NOTE]
>  **인덱스** 개체를 만들 때 선택적 속성에 대해 적절 한 기본값이 있으면 공급자가 속성을 지원 하지 않을 수 있습니다. 공급자가 지 원하는 속성에 대 한 자세한 내용은 공급자 설명서를 참조 하십시오.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Index 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Indexes Append 메서드 예제 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [IndexNulls 속성 예제 (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey 및 Unique 속성 예제 (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [SortOrder 속성 예제 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Indexes 컬렉션 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
