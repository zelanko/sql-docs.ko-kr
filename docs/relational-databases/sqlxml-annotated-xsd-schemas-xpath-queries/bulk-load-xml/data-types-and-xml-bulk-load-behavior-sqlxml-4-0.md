---
title: 데이터 형식과 XML 대량 로드 동작 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 820d2b083544542d1c1414f978105fe992b0ce36
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915155"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>데이터 형식과 XML 대량 로드 동작(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  매핑 스키마에 지정 된 데이터 형식 (XSD 또는 XDR 형식 및 **sql: datatype**) 일반적으로 무시 되며 다음과 같은 경우를 제외 하 고:  
  
 XSD  
  
-   형식이 **날짜/시간** 또는 **시간**를 지정 해야 합니다 **sql: datatype** XML 대량 로드 Microsoft로데이터를보내기전에데이터변환을수행하기때문에[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   열으로 대량 로드 하는 경우 **uniqueidentifier** 입력 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XSD 값이 중괄호 ({및}) 수를 포함 하는 GUID를 지정 해야 합니다 **sql: datatype = "uniqueidentifier"** 를 열에 값을 삽입 하기 전에 중괄호를 제거 합니다. 하는 경우 **sql: datatype** 지정 하지 않으면 값이 괄호와 함께 전송 되 고 삽입이 실패 합니다.  
  
 에 대 한 자세한 내용은 **sql: datatype**를 참조 하십시오 [데이터 형식 강제 변환 및 sql: datatype 주석 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 XDR  
  
-   경우는 **dt: type** 됩니다 **datetime**, **시간**, **dateTime.tz**, 또는 **time.tz**를 둘 다 지정 해야 합니다 합니다 **dt: type** 하 고 **sql: datatype** XML 대량 로드 데이터를 보내기 전에 데이터 변환을 수행 하기 때문에 데이터 형식을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
-   XML 데이터 형식의 경우 **uuid**하십시오 **sql: datatype** 지정 해야 합니다. **dt: type = "uuid"** 데이터가 문자열 데이터 경우가 아니면 필요 이기도 합니다. 지정 하지 않는 경우 **dt:uuid**, 중괄호를 사용 하 여 문자열을 허용 (및 필요한 경우 제거) XML 대량 로드 합니다.  
  
-   XML 데이터가 **bin.base64** 또는 **bin.hex**를 사용 하 여 XML 데이터 형식을 지정 해야 **dt: type**합니다. 그러면 XML 대량 로드에서는 데이터의 16진수 표현으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 로드합니다.  
  
  
