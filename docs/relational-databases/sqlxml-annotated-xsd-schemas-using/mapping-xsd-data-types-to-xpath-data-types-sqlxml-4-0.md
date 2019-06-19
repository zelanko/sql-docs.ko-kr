---
title: XSD 데이터 형식을 XPath 데이터 형식 (SQLXML 4.0)에 매핑 | Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f10134d4aa4d71c4471e5e3120b3f8fbd8ee1748
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65980788"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>XSD 데이터 형식을 XPath 데이터 형식에 매핑(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSD 스키마에 대해 XPath 쿼리가 실행 되 고 XSD 형식에 지정 된 경우는 **xsd: type** 특성을 XPath 쿼리를 처리할 때 지정 된 데이터 형식을 사용 합니다.  
  
 다음 표에서 볼 수 있는 것처럼 노드의 XPath 데이터 형식은 스키마의 XSD 데이터 형식에서 파생됩니다. EmployeeID 노드는 설명을 위해 사용되었습니다.  
  
|XSD 데이터 형식|XDR 데이터 형식|해당<br /><br /> XPath 데이터 형식|SQL Server<br /><br /> 변환|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**없음**<br /><br /> **bin.base64bin.hex**|**해당 사항 없음**|없음<br /><br /> EmployeeID|  
|**Boolean**|**boolean**|**boolean**|CONVERT(bit, EmployeeID)|  
|**10 진수, 정수, 실수, byte, short, int, long, float, double, unsignedShort, unsignedByte, unsignedInt, unsignedLong**|**숫자, int, float, i1, i2, i4, i8, r4, r8ui1, ui2 ui4, ui8**|**number**|CONVERT(float(53), EmployeeID)|  
|**id, idref, idrefsentity, entities, notation, nmtoken, nmtokens, DateTime, string, AnyURI**|**id, idref, idrefsentity, entities, enumeration, notation, nmtoken, nmtokens, char, dateTime, dateTime.tz, string, uri, uuid**|**string**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**해당 없음 (XPath에는 fixed14.4 XDR 데이터 형식에 해당 하는 없는 데이터 형식입니다.)**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**string**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**string**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
