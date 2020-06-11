---
title: 데이터 형식 및 XML 대량 로드 동작 (SQLXML)
description: SQLXML 4.0의 데이터 형식 및 XML 대량 로드 동작에 대해 알아봅니다.
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e77e4ca789a2abf5bb664221adb8911dd5a1bae5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529750"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>데이터 형식과 XML 대량 로드 동작(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  매핑 스키마 (XSD 또는 XDR 형식 및 **sql: datatype**)에 지정 된 데이터 형식은 일반적으로 다음과 같은 경우를 제외 하 고 무시 됩니다.  
  
 XSD  
  
-   형식이 **dateTime** 또는 **TIME**인 경우 XML 대량 로드에서 데이터를 Microsoft로 보내기 전에 데이터 변환을 수행 하기 때문에 **sql: datatype** 을 지정 해야 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   에서 **uniqueidentifier** 형식의 열로 대량 로드 하 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 고 XSD 값이 중괄호 ({및})를 포함 하는 GUID 인 경우 열에 값을 삽입 하기 전에 중괄호를 제거 하려면 **sql: datatype = "uniqueidentifier"** 를 지정 해야 합니다. **Sql: datatype** 을 지정 하지 않으면 값이 중괄호와 함께 전송 되 고 삽입이 실패 합니다.  
  
 **Sql: datatype**에 대 한 자세한 내용은 [데이터 형식 강제 변환 및 Sql: DATATYPE 주석 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)을 참조 하세요.  
  
 XDR  
  
-   **Dt: type** 이 **datetime**, **time**, **DateTime.tz**또는 **time.tz**인 경우 XML 대량 로드는 데이터를로 보내기 전에 데이터 변환을 수행 하기 때문에 **dt: type** 및 **sql: datatype** 데이터 형식을 모두 지정 해야 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   XML 데이터가 **uuid**형식인 경우 **sql: datatype** 을 지정 해야 합니다. **dt: type = "uuid"** 는 데이터가 문자열 데이터가 아닌 경우에도 필요 합니다. **Dt: uuid**를 지정 하지 않으면 XML 대량 로드는 중괄호를 사용 하 여 문자열을 수락 하 고 필요한 경우 제거 합니다.  
  
-   XML 데이터가 **bin. base64** 또는 **bin. hex**인 경우 **dt: TYPE**을 사용 하 여 xml 데이터 형식을 지정 해야 합니다. 그러면 XML 대량 로드에서는 데이터의 16진수 표현으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 로드합니다.  
  
  
