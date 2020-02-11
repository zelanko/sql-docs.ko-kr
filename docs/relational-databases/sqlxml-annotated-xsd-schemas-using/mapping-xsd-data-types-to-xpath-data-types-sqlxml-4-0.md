---
title: XSD 데이터 형식을 XPath 데이터 형식에 매핑 (SQLXML)
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6b956bf3a52b9ae14e59af770d279e8be8fec028
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75257381"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>XSD 데이터 형식을 XPath 데이터 형식에 매핑(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Xsd 스키마에 대해 XPath 쿼리를 실행할 때 xsd **: type** 특성에 xsd 형식이 지정 된 경우 xpath는 쿼리를 처리할 때 지정 된 데이터 형식을 사용 합니다.  
  
 다음 표에서 볼 수 있는 것처럼 노드의 XPath 데이터 형식은 스키마의 XSD 데이터 형식에서 파생됩니다. EmployeeID 노드는 설명을 위해 사용되었습니다.  
  
|XSD 데이터 형식|XDR 데이터 형식|해당<br /><br /> XPath 데이터 형식|SQL Server<br /><br /> 변환|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**없음을**<br /><br /> **base64bin**|**해당 사항 없음**|None<br /><br /> EmployeeID|  
|**Boolean**|**부울**|**부울**|CONVERT(bit, EmployeeID)|  
|**Decimal, integer, float, byte, short, int, long, float, double, unsignedByte**|**number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8**|**number**|CONVERT(float(53), EmployeeID)|  
|**id, idref, idrefsentity, entities, notation, nmtoken, nmtokens, DateTime, string, AnyURI**|**id, idref, idrefsentity, entities, enumeration, notation, nmtoken, nmtokens, char, dateTime, dateTime.tz, string, uri, uuid**|**문자열**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**진수가**|**fixed14.4**|**해당 사항 없음(XPath에는 fixed14.4 XDR 데이터 형식에 해당하는 데이터 형식이 없음)**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**문자열**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**문자열**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
