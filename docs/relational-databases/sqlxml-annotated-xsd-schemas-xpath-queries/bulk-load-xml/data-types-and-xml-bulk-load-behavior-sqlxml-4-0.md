---
title: 데이터 형식 및 XML 대량 로드 동작 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8315130a7228d0d5dce2f8baa2f337f16015ae23
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>데이터 형식과 XML 대량 로드 동작(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  매핑 스키마에 지정 된 데이터 형식 (XSD 또는 XDR 형식 및 **sql: datatype**) 일반적으로 무시 되며 다음과 같은 경우를 제외 하 고:  
  
 XSD  
  
-   형식이 **dateTime** 또는 **시간**를 지정 해야 합니다는 **sql: datatype** XML 대량 로드 Microsoft로데이터를보내기전에데이터변환을수행하기때문에[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   열에 대량 로드 하는 경우 **uniqueidentifier** 에 입력 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XSD 값이 중괄호 ({및}), 사용자를 포함 하는 GUID를 지정 해야 하 고 **sql: datatype = "uniqueidentifier"** 를 열에 값을 삽입 하기 전에 중괄호를 제거 합니다. 경우 **sql: datatype** 을 지정 하지 않으면 값이 괄호와 함께 전송 되 고 삽입이 실패 합니다.  
  
 에 대 한 자세한 내용은 **sql: datatype**, 참조 [데이터 형식 강제 변환 및 sql: datatype 주석 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)합니다.  
  
 XDR  
  
-   경우는 **dt: type** 은 **datetime**, **시간**, **dateTime.tz**, 또는 **time.tz**를 모두 지정 해야 **dt: type** 및 **sql: datatype** 데이터 형식에서 XML 대량 로드 데이터를 보내기 전에 데이터 변환을 수행 하기 때문에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
-   XML 데이터 형식인 경우 **uuid**, **sql: datatype** 지정 해야 하며 **dt: type = "uuid"** 표시 되지 않으면도 필요한 경우 데이터는 문자열 데이터. 지정 하지 않으면 **dt:uuid**, 중괄호를 사용 하 여 문자열을 수락 (및 필요에 따라 제거) XML 대량 로드 합니다.  
  
-   XML 데이터는 경우 **bin.base64** 또는 **bin.hex**를 사용 하 여 XML 데이터 형식 지정 해야 **dt: type**합니다. 그러면 XML 대량 로드에서는 데이터의 16진수 표현으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 로드합니다.  
  
  
