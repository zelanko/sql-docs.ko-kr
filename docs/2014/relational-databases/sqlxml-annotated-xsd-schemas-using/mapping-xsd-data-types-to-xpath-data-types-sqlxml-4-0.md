---
title: XSD 데이터 형식을 XPath 데이터 형식에 매핑 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: f8e0e1f4e2914439c380b3bbf7b6339ee28c6879
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013762"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>XSD 데이터 형식을 XPath 데이터 형식에 매핑(SQLXML 4.0)
  XSD 스키마에 대해 XPath 쿼리를 실행할 경우 XSD 형식이 `xsd:type` 특성에 지정되어 있으면 XPath는 쿼리를 처리할 때 지정된 데이터 형식을 사용합니다.  
  
 다음 표에서 볼 수 있는 것처럼 노드의 XPath 데이터 형식은 스키마의 XSD 데이터 형식에서 파생됩니다. EmployeeID 노드는 설명을 위해 사용되었습니다.  
  
|XSD 데이터 형식|XDR 데이터 형식|해당<br /><br /> XPath 데이터 형식|SQL Server<br /><br /> 변환|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|`Base64Binary`<br /><br /> `HexBinary`|`None`<br /><br /> `bin.base64bin.hex`|`Not applicable`|None<br /><br /> EmployeeID|  
|`Boolean`|`boolean`|`boolean`|CONVERT(bit, EmployeeID)|  
|`Decimal, integer, float, byte, short, int, long, float, double, unsignedByte, unsignedShort, unsignedInt, unsignedLong`|`number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8`|`number`|CONVERT(float(53), EmployeeID)|  
|`id, idref, idrefsentity, entities, notation, nmtoken, nmtokens, DateTime, string, AnyURI`|`id, idref, idrefsentity, entities, enumeration, notation, nmtoken, nmtokens, char, dateTime, dateTime.tz, string, uri, uuid`|`string`|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|`decimal`|`fixed14.4`|`Not applicable (There is no data type in XPath that is equivalent to the fixed14.4 XDR data type.)`|CONVERT(money, EmployeeID)|  
|`date`|`date`|`string`|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|`time`|`time`<br /><br /> `time.tz`|`string`|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
