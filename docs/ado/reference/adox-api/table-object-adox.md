---
title: 테이블 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5af59dbc50f6e1a2cd95cbdf99874d860eceeb1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622341"
---
# <a name="table-object-adox"></a>테이블 개체(ADOX)
열, 인덱스 및 키를 포함 하 여 데이터베이스 테이블을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 다음 코드를 만듭니다 **테이블**:  
  
```  
Dim obj As New Table  
```  
  
 속성 및 컬렉션을 **테이블** 개체를 할 수 있습니다.  
  
-   사용 하 여 테이블을 식별 하는 [이름 속성 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   테이블의 형식을 확인 합니다 [Type 속성 (테이블) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md) 속성입니다.  
  
-   테이블의 데이터베이스 열에 액세스 합니다 [열 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md) 컬렉션입니다.  
  
-   포함 된 테이블의 인덱스에 액세스 합니다 [인덱스 컬렉션 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)합니다.  
  
-   포함 된 테이블의 키에 액세스 합니다 [키 컬렉션 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)합니다.  
  
-   포함 된 테이블을 소유 하는 카탈로그를 지정 합니다 [ParentCatalog 속성 (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) 속성입니다.  
  
-   사용 하 여 날짜 정보를 반환 합니다 [DateCreated 속성 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md) 하 고 [DateModified 속성 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md) 속성입니다.  
  
-   공급자별 테이블 속성에 액세스 합니다 [속성 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
> [!NOTE]
>  데이터 공급자의 모든 속성을 지원 하지 않을 수 있습니다 **테이블** 개체입니다. 공급자를 지원 하지 않는 속성의 값을 사용 하도록 설정한 경우 오류가 발생 합니다. 새로운 **테이블** 개체는 개체 컬렉션에 추가할 때 오류가 발생 합니다. 기존 개체에 대 한 속성을 설정할 때 오류가 발생 합니다.  
>   
>  만들면 **테이블** 개체 선택적 속성에 대 한 적절 한 기본값이 있는지 공급자 속성을 지원 하도록 보장 하지 않습니다. 공급자에서 지원 되는 속성에 대 한 자세한 내용은 공급자 설명서를 참조 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Table 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Catalog ActiveConnection 속성 예제 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 메서드, Table Type 속성 예제 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 메서드, 키 유형, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Indexes 컬렉션 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Keys 컬렉션 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Tables 컬렉션(ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
