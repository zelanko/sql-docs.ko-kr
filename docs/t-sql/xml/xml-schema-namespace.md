---
title: xml_schema_namespace (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 449e545672192baa9d16204afe1fb23497959094
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="xmlschemanamespace"></a>xml_schema_namespace
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 XML 스키마 컬렉션에서 모든 스키마 또는 특정 스키마를 다시 만듭니다. 이 함수는 **xml** 데이터 형식을 반환합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```  
  
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
## <a name="arguments"></a>인수  
 *Relational_schema*  
 관계형 스키마 이름입니다. *Relational_schema* 은 **sysname**합니다.  
  
 *XML_schema_collection_name*  
 다시 만들 XML 스키마 컬렉션의 이름입니다. *XML_schema_collection_name* 은 **sysname**합니다.  
  
 *네임스페이스*  
 다시 만들 XML 스키마의 네임스페이스 URI입니다. 1,000자로 제한됩니다. 네임스페이스 URI를 제공하지 않으면 전체 XML 스키마 컬렉션이 다시 생성됩니다. *Namespace* 은 **nvarchar (4000)**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **xml**  
  
## <a name="remarks"></a>주의  
 사용 하 여 데이터베이스의 XML 스키마 구성 요소를 가져올 때 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) 또는 [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md), 유효성 검사에 사용 되는 스키마의 측면에서 유지 됩니다. 따라서 다시 만든 스키마가 원래 스키마 문서와 구문적으로 동일하지 않을 수 있습니다. 특히 설명, 공백 및 주석이 손실되고 암시적인 유형 정보가 명시적으로 변경됩니다. 예를 들어 \<: element name = "e1" / >가 \<: element name = "e1" type = "xs: anytype" / >입니다. 또한 네임스페이스 접두사가 유지되지 않습니다.  
  
 네임스페이스 매개 변수를 지정하는 경우 결과 스키마 문서에는 다른 스키마 문서, DDL 단계 또는 둘 모두에 추가된 경우를 비롯하여 해당 네임스페이스의 모든 스키마 구성 요소에 대한 정의가 포함됩니다.  
  
 XML 스키마 문서를 생성 하려면이 함수를 사용할 수 없습니다는 **sys.sys** XML 스키마 컬렉션입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `ProductDescriptionSchemaCollection` 데이터베이스의 production 관계형 스키마에서 XML 스키마 컬렉션인 `AdventureWorks2012`을 검색합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [저장된 XML 스키마 컬렉션 보기](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [XML 스키마 컬렉션&#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  

