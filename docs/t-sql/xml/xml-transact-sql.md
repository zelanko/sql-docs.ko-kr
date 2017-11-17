---
title: xml (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xml_TSQL
- xml
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], about xml data type
ms.assetid: 9198f671-8e61-4ca4-9c3a-859f84020e62
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e85eb245cf9d53f7d38579928a5145828797002
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="xml-transact-sql"></a>xml(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  XML 데이터를 저장하는 데이터 형식입니다. 저장할 수 있습니다 **xml** 열 또는 변수에서 인스턴스 **xml** 유형입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xml ( [ CONTENT | DOCUMENT ] xml_schema_collection )  
```  
  
## <a name="arguments"></a>인수  
 CONTENT  
 제한 된 **xml** 인스턴스 올바른 형식의 XML 조각이 되도록 합니다. XML 데이터는 최상위 수준에 0개 이상의 요소를 포함할 수 있습니다. 텍스트 노드도 최상위 수준에서 허용됩니다.  
  
 이것이 기본 동작입니다.  
  
 DOCUMENT  
 제한 된 **xml** 인스턴스를 올바른 형식의 XML 문서입니다. XML 데이터에는 한 개의 루트 요소만 있어야 합니다. 텍스트 노드는 최상위 수준에서 허용되지 않습니다.  
  
 *xml_schema_collection*  
 XML 스키마 컬렉션의 이름입니다. 형식화 된 만들려면 **xml** 열 또는 변수, XML 스키마 컬렉션 이름을 선택적으로 지정할 수 있습니다. 자세한 정보에 대 한 정보 입력을 형식화 되지 않은 XML에 대 한 참조 [형식화 된 XML과 형식화 되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)합니다.  
  
## <a name="remarks"></a>주의  
 저장 된 표현은 **xml** 데이터 형식 인스턴스의 2gb (기가바이트)의 크기를 초과할 수 없습니다.  
  
 CONTENT 및 DOCUMENT 패싯은 형식화된 XML에만 적용됩니다. 자세한 내용은 참조 [형식화 된 XML과 형식화 되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)합니다.  
  
## <a name="examples"></a>예  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @y xml (Sales.IndividualSurveySchemaCollection);  
SET @y =  (SELECT TOP 1 Demographics FROM Sales.Individual);  
SELECT @y;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식 변환 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  

