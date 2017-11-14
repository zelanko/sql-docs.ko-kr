---
title: "테이블 개체 (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 198b59d624b2daa2e2451b8dbb61ae5868f7eb7d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="table-object-adox"></a>Table 개체 (ADOX)
열, 인덱스 및 키를 포함 하 여 데이터베이스 테이블을 나타냅니다.  
  
## <a name="remarks"></a>주의  
 다음 코드에서는 새 **테이블**:  
  
```  
Dim obj As New Table  
```  
  
 속성과 컬렉션을 사용 하 여 한 **테이블** 개체를 할 수 있습니다.  
  
-   포함 된 테이블을 식별 된 [Name 속성 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   포함 된 테이블의 형식을 결정는 [Type 속성 (테이블) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md) 속성입니다.  
  
-   데이터베이스 열에 있는 테이블의 액세스는 [열 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md) 컬렉션입니다.  
  
-   포함 된 테이블의 인덱스에 액세스할는 [인덱스 컬렉션 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)합니다.  
  
-   포함 된 테이블의 키에 액세스할는 [키 컬렉션 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)합니다.  
  
-   포함 된 테이블을 소유 하는 카탈로그를 지정 된 [ParentCatalog 속성 (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) 속성입니다.  
  
-   반환 된 날짜 정보는 [DateCreated 속성 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md) 및 [DateModified 속성 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md) 속성.  
  
-   사용 하 여 공급자별 테이블 속성에 액세스는 [속성 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
> [!NOTE]
>  데이터 공급자의 모든 속성을 지원 하지 않을 수 있습니다 **테이블** 개체입니다. 공급자를 지원 하지 않는 속성에 대 한 값을 사용 하도록 설정한 경우 오류가 발생 합니다. 새 **테이블** 개체는 개체 컬렉션에 추가할 때 오류가 발생 합니다. 기존 개체에 대 한 속성을 설정할 때 오류가 발생 합니다.  
>   
>  만들 때 **테이블** 개체의 경우에 선택적 속성에 대 한 적절 한 기본값이 있는지 공급자 속성을 지원 하도록 보장 하지 않습니다. 공급자에서 지원 되는 속성에 대 한 자세한 내용은 공급자 설명서를 참조 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Table 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 ActiveConnection 속성 예제 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [테이블 및 열 이름 속성 예제 (VB) 메서드 추가](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [테이블 형식 속성 예제 (VB) 연결 Close 메서드](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [키 추가 방법, 키 형식, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [인덱스 컬렉션 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [키 컬렉션 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Tables 컬렉션(ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)

