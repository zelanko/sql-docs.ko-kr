---
title: "XSD 데이터 형식을 XPath 데이터 형식 (SQLXML 4.0)에 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
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
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 19ce96f9e7c7731b669f5186a1b038bade09646e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>XSD 데이터 형식을 XPath 데이터 형식에 매핑(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]XSD 스키마에 대해 XPath 쿼리 실행은 XSD 형식에 지정 된 시점과 **xsd: type** 특성을 XPath 쿼리를 처리할 때 지정 된 데이터 형식을 사용 합니다.  
  
 다음 표에서 볼 수 있는 것처럼 노드의 XPath 데이터 형식은 스키마의 XSD 데이터 형식에서 파생됩니다. EmployeeID 노드는 설명을 위해 사용되었습니다.  
  
|XSD 데이터 형식|XDR 데이터 형식|해당<br /><br /> XPath 데이터 형식|SQL Server<br /><br /> 변환|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**없음**<br /><br /> **bin.base64bin.hex**|**해당 사항 없음**|없음<br /><br /> EmployeeID|  
|**Boolean**|**boolean**|**boolean**|CONVERT(bit, EmployeeID)|  
|**10 진수, integer, float, 바이트, short, int, long, float, double, unsignedByte, unsignedShort, unsignedInt, unsignedLong**|**숫자, int, float, i1, i2, i4, i8, r4, r8ui1, ui2 ui4, ui8**|**번호**|CONVERT(float(53), EmployeeID)|  
|**id, idref, idrefsentity, 엔터티, 표기법, nmtoken, nmtokens, DateTime, 문자열, AnyURI**|**id, idref, idrefsentity, 엔터티, 열거형, 표기법, nmtoken, nmtokens, char, dateTime, dateTime.tz, string, uri, uuid**|**string**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**해당 사항 없음 (fixed14.4 XDR 데이터 형식에 해당 하는 XPath의 데이터 형식이 없는.)**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**string**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**string**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
