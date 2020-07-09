---
title: xml_schema_namespace(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c5749c942f5da62dee1cc1f4bb0345c6165bd649
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85902214"
---
# <a name="xml_schema_namespace"></a>xml_schema_namespace
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  지정한 XML 스키마 컬렉션에서 모든 스키마 또는 특정 스키마를 다시 만듭니다. 이 함수는 **xml** 데이터 형식을 반환합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```  
  
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
## <a name="arguments"></a>인수  
 *Relational_schema*  
 관계형 스키마 이름입니다. *Relational_schema*는 **sysname**입니다.  
  
 *XML_schema_collection_name*  
 다시 만들 XML 스키마 컬렉션의 이름입니다. *XML_schema_collection_name*은 **sysname**입니다.  
  
 *Namespace*  
 다시 만들 XML 스키마의 네임스페이스 URI입니다. 1,000자로 제한됩니다. 네임스페이스 URI를 제공하지 않으면 전체 XML 스키마 컬렉션이 다시 생성됩니다. *Namespace*는 **nvarchar(4000)** 입니다.  
  
## <a name="return-types"></a>반환 형식  
 **xml**  
  
## <a name="remarks"></a>설명  
 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) 또는 [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)을 사용하여 데이터베이스의 XML 스키마 구성 요소를 가져오는 경우에는 유효성 검사에 사용된 스키마의 특성이 유지됩니다. 따라서 다시 만든 스키마가 원래 스키마 문서와 구문적으로 동일하지 않을 수 있습니다. 특히 설명, 공백 및 주석이 손실되고 암시적인 유형 정보가 명시적으로 변경됩니다. 예를 들어 \<xs:element name="e1" />는 \<xs:element name="e1" type="xs:anyType"/>가 됩니다. 또한 네임스페이스 접두사가 유지되지 않습니다.  
  
 네임스페이스 매개 변수를 지정하는 경우 결과 스키마 문서에는 다른 스키마 문서, DDL 단계 또는 둘 모두에 추가된 경우를 비롯하여 해당 네임스페이스의 모든 스키마 구성 요소에 대한 정의가 포함됩니다.  
  
 이 함수는 **sys.sys** XML 스키마 컬렉션에서 XML 스키마 문서를 생성하는 데 사용할 수 없습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `ProductDescriptionSchemaCollection` 데이터베이스의 production 관계형 스키마에서 XML 스키마 컬렉션인 `AdventureWorks`을 검색합니다.  
  
```  
USE AdventureWorks;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [저장된 XML 스키마 컬렉션 보기](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [XML 스키마 컬렉션&#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
