---
title: "저장된 XML 스키마 컬렉션 보기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema collections [SQL Server], viewing
- XML schemas [SQL Server], viewing
- CREATE XML SCHEMA COLLECTION statement
- xml_schema_namespace function
- XML schema collections [SQL Server], viewing
- displaying XML schema collections
- viewing XML schema collections
ms.assetid: e38031af-22df-4cd9-a14e-e316b822f91b
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2bacfd298e992c64739442605f986afffefdb443
ms.lasthandoff: 04/11/2017

---
# <a name="view-a-stored-xml-schema-collection"></a>저장된 XML 스키마 컬렉션 보기
  [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)을 사용하여 XML 스키마 컬렉션을 가져오면 스키마 구성 요소가 메타데이터에 저장됩니다. [xml_schema_namespace](../../t-sql/xml/xml-schema-namespace.md)내장 함수를 사용하여 XML 스키마 컬렉션을 다시 만들 수 있습니다. 이 함수는 **xml** 데이터 형식을 반환합니다.  
  
 예를 들어 다음 쿼리는`ProductDescriptionSchemaCollection`데이터베이스의 프로덕션 관계형 스키마에서 XML 스키마 컬렉션( [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] )을 검색합니다.  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection')  
GO  
```  
  
 XML 스키마 컬렉션에서 한 개의 스키마만 표시하려면 **가 반환하는** xml `xml_schema_namespace`유형 결과에 대해 XQuery를 지정할 수 있습니다.  
  
```  
SELECT xml_schema_namespace(N'RelationalSchemaName',N'XmlSchemaCollectionName').query('  
/xs:schema[@targetNamespace="TargetNameSpace"]  
')  
GO  
```  
  
 예를 들어 다음 쿼리는 `ProductDescriptionSchemaCollection` XML 스키마 컬렉션에서 제품 보증 및 유지 관리 XML 스키마 정보를 검색합니다.  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection').query('  
/xs:schema[@targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"]  
')  
GO  
```  
  
 또한 선택적인 대상 네임스페이스를 세 번째 매개 변수로 `xml_schema_namespace` 함수에 전달하여 다음 쿼리처럼 컬렉션에서 특정 스키마를 검색할 수 있습니다.  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection', N'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain')  
GO  
```  
  
 데이터베이스에 CREATE XML SCHEMA COLLECTION을 사용하여 XML 스키마 컬렉션을 만들면 스키마 구성 요소가 메타데이터에 저장됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 인식하는 스키마 구성 요소만 저장됩니다. 설명, 주석 또는 비-XSD 특성은 저장되지 않습니다. 따라서 **xml_schema_namespace** 가 다시 만든 스키마는 원래 스키마와 동일한 기능을 하지만 모양이 반드시 같을 필요는 없습니다. 예를 들어 원래 스키마에 있던 동일한 접두사가 표시되지 않습니다. **xml_schema_namespace** 에서 반환된 스키마는 **t** 를 대상 네임스페이스에 대한 접두사로 사용하고 **ns1**, **ns2**등을 다른 네임스페이스에 대한 접두사로 사용합니다.  
  
 XML 스키마의 동일한 복사본을 보존하려면 XML 스키마를 파일에 저장하거나 **xml** 유형 열에 있는 데이터베이스 테이블에 저장해야 합니다.  
  
 또한 [sys.xml_schema_collections](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md) 카탈로그 뷰는 XML 스키마 컬렉션에 대한 정보를 반환합니다. 이 정보에는 컬렉션의 이름, 만든 날짜, 컬렉션의 소유자 등이 포함됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 스키마 컬렉션&#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
