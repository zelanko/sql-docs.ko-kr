---
title: xml(Transact-SQL)
description: xml(Transact-SQL)
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- XML_TSQL
- xml_TSQL
- xml
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], about xml data type
ms.assetid: 9198f671-8e61-4ca4-9c3a-859f84020e62
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: ''
ms.date: 07/26/2017
ms.openlocfilehash: 885499cdd42d429c1fd86f098ad03be7b4b54ed2
ms.sourcegitcommit: 2bf83972036bdbe6a039fb2d1fc7b5f9ca9589d3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94674205"
---
# <a name="xml-transact-sql"></a>xml(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  XML 데이터를 저장하는 데이터 형식입니다. **xml** 형식의 변수 또는 열에 **xml** 인스턴스를 저장할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```
xml ( [ CONTENT | DOCUMENT ] xml_schema_collection )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 CONTENT  
 올바른 형식의 XML 조각이 되도록 **xml** 인스턴스를 제한합니다. XML 데이터는 최상위 수준에 0개 이상의 요소를 포함할 수 있습니다. 텍스트 노드도 최상위 수준에서 허용됩니다.  
  
 기본 동작입니다.  
  
 DOCUMENT  
 올바른 형식의 XML 문서가 되도록 **xml** 인스턴스를 제한합니다. XML 데이터에는 한 개의 루트 요소만 있어야 합니다. 텍스트 노드는 최상위 수준에서 허용되지 않습니다.  
  
 *xml_schema_collection*  
 XML 스키마 컬렉션의 이름입니다. 형식화된 **xml** 열이나 변수를 만들려면 선택적으로 XML 스키마 컬렉션 이름을 지정할 수 있습니다. 형식화된 XML 및 형식화되지 않은 XML에 대한 자세한 내용은 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)를 참조하세요.  
  
## <a name="remarks"></a>설명  
 **xml** 데이터 형식 인스턴스의 저장된 표현 크기는 2GB를 넘을 수 없습니다.  
  
 CONTENT 및 DOCUMENT 패싯은 형식화된 XML에만 적용됩니다. 자세한 내용은 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)를 참조하세요.  
  
## <a name="examples"></a>예제  
  
```sql
USE AdventureWorks;  
GO  
DECLARE @DemographicData XML (Person.IndividualSurveySchemaCollection);  
SET @DemographicData = (SELECT TOP 1 Demographics FROM Person.Person);  
SELECT @DemographicData;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식 변환&#40;Database Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
