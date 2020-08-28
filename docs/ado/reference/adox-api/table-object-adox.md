---
description: 테이블 개체(ADOX)
title: Table 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f6803b4afc7f50a08f305a619e9c0ca328e5e988
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983254"
---
# <a name="table-object-adox"></a>테이블 개체(ADOX)
열, 인덱스 및 키를 포함 하는 데이터베이스 테이블을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 다음 코드는 새 **테이블**을 만듭니다.  
  
```  
Dim obj As New Table  
```  
  
 **Table** 개체의 속성 및 컬렉션을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name 속성 (ADOX)](./name-property-adox.md) 속성을 사용 하 여 테이블을 식별 합니다.  
  
-   [유형 속성 (테이블) (ADOX)](./type-property-table-adox.md) 속성을 사용 하 여 테이블 유형을 결정 합니다.  
  
-   [ADOX (Columns collection)](./columns-collection-adox.md) 컬렉션을 사용 하 여 테이블의 데이터베이스 열에 액세스 합니다.  
  
-   [인덱스 컬렉션 (ADOX)](./indexes-collection-adox.md)을 사용 하 여 테이블의 인덱스에 액세스 합니다.  
  
-   [키 컬렉션 (ADOX)](./keys-collection-adox.md)을 사용 하 여 테이블의 키에 액세스 합니다.  
  
-   [ParentCatalog 속성 (ADOX)](./parentcatalog-property-adox.md) 속성을 사용 하 여 테이블을 소유 하는 카탈로그를 지정 합니다.  
  
-   [DateCreated 속성 (adox)](./datecreated-property-adox.md) 및 [DATEMODIFIED Property (adox)](./datemodified-property-adox.md) 속성을 사용 하 여 날짜 정보를 반환 합니다.  
  
-   [Properties collection (ADO)](../ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 공급자별 테이블 속성에 액세스 합니다.  
  
> [!NOTE]
>  데이터 공급자가 **테이블** 개체의 일부 속성을 지원 하지 않을 수 있습니다. 공급자가 지원 하지 않는 속성에 대 한 값을 설정 하면 오류가 발생 합니다. 새 **테이블** 개체의 경우 개체가 컬렉션에 추가 되 면 오류가 발생 합니다. 기존 개체의 경우 속성을 설정할 때 오류가 발생 합니다.  
>   
>  **테이블** 개체를 만들 때 선택적 속성에 대해 적절 한 기본값이 있으면 공급자가 속성을 지원 하지 않을 수 있습니다. 공급자가 지 원하는 속성에 대 한 자세한 내용은 공급자 설명서를 참조 하십시오.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [테이블 개체 속성, 메서드 및 이벤트](./table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Catalog ActiveConnection 속성 예제 (VB)](./catalog-activeconnection-property-example-vb.md)   
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 메서드, Table Type 속성 예제 (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](./parentcatalog-property-example-vb.md)   
 [Columns 컬렉션 (ADOX)](./columns-collection-adox.md)   
 [Indexes 컬렉션 (ADOX)](./indexes-collection-adox.md)   
 [Keys 컬렉션 (ADOX)](./keys-collection-adox.md)   
 [Properties 컬렉션 (ADO)](../ado-api/properties-collection-ado.md)   
 [Tables 컬렉션(ADOX)](./tables-collection-adox.md)