---
title: XSD 데이터 형식을 XPath 데이터 형식에 매핑 (SQLXML)
description: SQLXML 4.0에서 XPath 쿼리를 수행할 때 XSD 데이터 형식을 XPath 데이터 형식에 매핑하는 방법에 대해 알아봅니다.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- XPath queries [SQLXML], mapping data types
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XPath data types [SQLXML]
- XSD schemas [SQLXML], mapping data types
ms.assetid: ced1a95e-18d4-4a5a-8da8-dbb6d58bbd45
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 75a7ef44e18566781215bab806caa43860c57cb7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97415851"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>XSD 데이터 형식을 XPath 데이터 형식에 매핑(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Xsd 스키마에 대해 XPath 쿼리를 실행할 때 xsd **: type** 특성에 xsd 형식이 지정 된 경우 xpath는 쿼리를 처리할 때 지정 된 데이터 형식을 사용 합니다.  
  
 다음 표에서 볼 수 있는 것처럼 노드의 XPath 데이터 형식은 스키마의 XSD 데이터 형식에서 파생됩니다. EmployeeID 노드는 설명을 위해 사용되었습니다.  
  
|XSD 데이터 형식|XDR 데이터 형식|해당<br /><br /> XPath 데이터 형식|SQL Server<br /><br /> 변환|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**없음**<br /><br /> **base64bin**|**해당 사항 없음**|없음<br /><br /> EmployeeID|  
|**Boolean**|**boolean**|**boolean**|CONVERT(bit, EmployeeID)|  
|**Decimal, integer, float, byte, short, int, long, float, double, unsignedByte**|**number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8**|**number**|CONVERT(float(53), EmployeeID)|  
|**id, idref, idrefsentity, entities, notation, nmtoken, nmtokens, DateTime, string, AnyURI**|**id, idref, idrefsentity, entities, enumeration, notation, nmtoken, nmtokens, char, dateTime, dateTime.tz, string, uri, uuid**|**string**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**해당 사항 없음(XPath에는 fixed14.4 XDR 데이터 형식에 해당하는 데이터 형식이 없음)**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**string**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**string**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
