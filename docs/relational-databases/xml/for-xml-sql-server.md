---
title: FOR XML(SQL Server)
description: SQL 쿼리에서 결과를 XML로 검색하는 데 사용되는 FOR XML 절에 대해 알아봅니다.
ms.prod: sql
ms.prod_service: database-engine
ms.technology: xml
ms.topic: conceptual
f1_keywords:
- FOR_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FOR XML clause, about FOR XML clause
- PATH FOR XML mode, construction
- EXPLICIT FOR XML mode
- RAW FOR XML mode
- retrieving XML data
- XML [SQL Server], FOR XML clause
- AUTO FOR XML mode
- XML [SQL Server], construction
ms.assetid: 2b6b5c61-c5bd-49d2-8c0c-b7cf15857906
author: RothJa
ms.author: jroth
ms.reviewer: ''
ms.custom: fresh2019may
ms.date: 04/03/2020
ms.openlocfilehash: 974da804e79a6c571b7543caec230984296f6a8e
ms.sourcegitcommit: 2bf83972036bdbe6a039fb2d1fc7b5f9ca9589d3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94674157"
---
# <a name="for-xml-sql-server"></a>FOR XML(SQL Server)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

SELECT 쿼리는 결과를 행 집합으로 반환합니다. 선택적으로 쿼리에서 FOR XML 절을 지정하면 SQL 쿼리의 서식 결과를 XML로 검색할 수 있습니다. FOR XML 절은 최상위 쿼리 및 하위 쿼리에서 사용할 수 있습니다. 최상위 FOR XML 절은 SELECT 문에서만 사용할 수 있습니다. 하위 쿼리에서는 INSERT, UPDATE 및 DELETE 문에서 FOR XML을 사용할 수 있습니다. FOR XML은 대입문에서도 사용할 수 있습니다.

FOR XML 절에서 다음 모드 중 하나를 지정합니다.

- RAW
- AUTO
- EXPLICIT
- PATH

RAW 모드는 행 집합의 각 행마다 SELECT 문으로 반환되는 단일 \<row> 요소를 생성합니다. 중첩된 FOR XML 쿼리를 작성하여 XML 계층을 생성할 수 있습니다.

AUTO 모드는 SELECT 문이 지정된 방식에 따른 추론 방식을 사용하여 결과 XML에서 중첩 구조를 생성합니다. 생성된 XML의 셰이프는 최소한으로만 제어할 수 있습니다. AUTO 모드 추론 방식으로 생성된 XML 셰이프와는 달리 XML 계층을 생성하도록 중첩된 FOR XML 쿼리를 작성할 수 있습니다.

EXPLICIT 모드는 XML 셰이프에 대해 더 많은 제어 기능을 제공합니다. 사용자는 XML 셰이프를 결정할 때 자신의 의지대로 특성과 요소를 혼합할 수 있습니다. 이를 위해서는 쿼리 실행에 따라 생성되는 결과 행 집합에 대한 특정 서식이 필요합니다. 그런 다음 이 행 집합 서식이 XML 셰이프로 매핑됩니다. EXPLICIT 모드의 장점은 특성 및 요소를 자신의 의지대로 혼합하고, 래퍼 및 중첩된 복합 속성을 만들고, 공백으로 구분된 값(예: 주문 ID 값 목록이 포함된 OrderID 특성)과 혼합된 내용을 만들 수 있습니다.

하지만 EXPLICIT 모드 쿼리 작성은 복잡할 수 있습니다. 중첩된 FOR XML RAW/AUTO/PATH 모드 쿼리 및 TYPE 지시어를 작성하여 EXPLICIT 모드를 사용하는 대신 새로운 FOR XML 기능 중 일부를 사용하여 계층을 생성할 수 있습니다. 중첩된 FOR XML 쿼리는 EXPLICIT 모드를 사용하여 생성할 수 있는 모든 XML을 만들 수 있습니다. 자세한 내용은 [중첩 FOR XML 쿼리 사용](../../relational-databases/xml/use-nested-for-xml-queries.md) 및 [FOR XML 쿼리의 TYPE 지시어](../../relational-databases/xml/type-directive-in-for-xml-queries.md)를 참조하세요.

중첩된 FOR XML 쿼리 기능이 함께 포함된 PATH 경로는 EXPLICIT 모드를 보다 간단한 방식으로 사용할 수 있는 유연성을 제공합니다.

이러한 모드는 실제로 모드가 설정된 해당 쿼리 실행만을 위한 것입니다. 다른 후속 쿼리의 결과에는 영향을 주지 않습니다.

FOR XML은 FOR BROWSE 절과 함께 사용하는 모든 선택에 대해서는 유효하지 않습니다.

## <a name="example"></a>예제

다음 `SELECT` 문은 `Sales.Customer` 데이터베이스의 `Sales.SalesOrderHeader` 및 `AdventureWorks2012` 테이블에서 정보를 검색합니다. 다음 쿼리는 `AUTO` 절에 `FOR XML` 모드를 지정합니다.

```sql
USE AdventureWorks2012
GO
SELECT Cust.CustomerID,
       OrderHeader.CustomerID,
       OrderHeader.SalesOrderID,
       OrderHeader.Status
FROM Sales.Customer Cust 
INNER JOIN Sales.SalesOrderHeader OrderHeader
ON Cust.CustomerID = OrderHeader.CustomerID
FOR XML AUTO;
```

## <a name="the-for-xml-clause-and-server-names"></a>FOR XML 절 및 서버 이름

FOR XML 절이 있는 SELECT 명령문이 쿼리에서 네 부분으로 된 이름을 지정할 경우, 로컬 컴퓨터에서 쿼리를 실행하면 서버 이름이 결과 XML 문서에 반환되지 않습니다. 그러나 쿼리를 네트워크 서버에서 실행하면 서버 이름은 네 부분으로 된 이름으로 반환됩니다.

예를 들어 다음과 같은 쿼리를 고려할 수 있습니다.

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person
  FOR XML AUTO;
```

&nbsp;

**로컬 서버**: &nbsp;`ServerName`이 로컬 서버인 경우 쿼리는 다음 텍스트를 반환합니다.

```xml
<AdventureWorks2012.Person.Person LastName="Achong" />  
```

&nbsp;

**네트워크 서버**: &nbsp;`ServerName`이 네트워크 서버인 경우 쿼리는 다음 텍스트를 반환합니다.

```xml
<ServerName.AdventureWorks2012.Person.Person LastName="Achong" />
```

&nbsp;

**모호성 방지**: &nbsp; 다음과 같이 별칭을 지정하여 이러한 잠재적 모호성을 방지할 수 있습니다.

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person x
  FOR XML AUTO;
```

이제 명확한 쿼리가 다음 텍스트를 반환합니다.

```xml
<x LastName="Achong"/>
```

## <a name="see-also"></a>참고 항목

[FOR XML 절의 기본 구문](../../relational-databases/xml/basic-syntax-of-the-for-xml-clause.md)  
[FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
[FOR XML에서 AUTO 모드 사용](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
[FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
[FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
[OPENXML&#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
[WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)
