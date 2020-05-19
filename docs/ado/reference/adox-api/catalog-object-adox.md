---
title: Catalog 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADOX]
ms.assetid: bb651639-a488-4e38-b6de-0ed99fa4dd92
author: rothja
ms.author: jroth
ms.openlocfilehash: f13533ce9d14a650e409507e646eb536bad14e4d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763944"
---
# <a name="catalog-object-adox"></a>카탈로그 개체(ADOX)
데이터 원본의 스키마 카탈로그를 설명 하는 컬렉션 ([테이블](../../../ado/reference/adox-api/tables-collection-adox.md), [뷰](../../../ado/reference/adox-api/views-collection-adox.md), [사용자](../../../ado/reference/adox-api/users-collection-adox.md), [그룹](../../../ado/reference/adox-api/groups-collection-adox.md)및 [프로시저](../../../ado/reference/adox-api/procedures-collection-adox.md))을 포함 합니다.  
  
## <a name="remarks"></a>설명  
 개체를 추가 또는 제거 하거나 기존 개체를 수정 하 여 **카탈로그** 개체를 수정할 수 있습니다. 일부 공급자는 일부 **카탈로그** 개체를 지원 하지 않거나 스키마 정보만 볼 수 있습니다.  
  
 **Catalog** 개체의 속성 및 메서드를 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 속성을 ADO [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 또는 유효한 연결 문자열로 설정 하 여 카탈로그를 엽니다.  
  
-   [Create](../../../ado/reference/adox-api/create-method-adox.md) 메서드를 사용 하 여 새 카탈로그를 만듭니다.  
  
-   [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) 및 [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) 메서드를 사용 하 여 **카탈로그** 의 개체 소유자를 확인 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Catalog 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Catalog ActiveConnection 속성 예제 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Command 및 CommandText 속성 예제 (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Connection Close 메서드, Table Type 속성 예제 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Create 메서드 예제 (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Parameters 컬렉션, Command 속성 예제 (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [프로시저 Append 메서드 예제 (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [프로시저 Delete 메서드 예제 (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [프로시저 Refresh 메서드 예제 (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [Views 및 Fields 컬렉션 예제 (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Views Append 메서드 예제 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Views 컬렉션, CommandText 속성 예제 (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Views Delete 메서드 예제 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Views Refresh 메서드 예제 (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Groups 컬렉션 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [프로시저 컬렉션 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Tables 컬렉션 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [사용자 컬렉션 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [Views 컬렉션(ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
