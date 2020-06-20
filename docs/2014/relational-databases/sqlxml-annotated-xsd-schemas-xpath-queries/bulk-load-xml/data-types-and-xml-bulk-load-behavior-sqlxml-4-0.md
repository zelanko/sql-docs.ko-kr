---
title: 데이터 형식 및 XML 대량 로드 동작 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 34b03423f3bb88166d0d9ce5b0df450d4455e7ef
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068166"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>데이터 형식과 XML 대량 로드 동작(SQLXML 4.0)
  매핑 스키마(XSD 또는 XDR 형식 및 `sql:datatype`)에 지정된 데이터 형식은 일반적으로 다음 경우를 제외하고는 무시됩니다.  
  
 XSD  
  
-   `dateTime` 또는 `time` 형식의 경우 XML 대량 로드는 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 보내기 전에 데이터 변환을 수행하기 때문에 `sql:datatype`을 지정해야 합니다.  
  
-   에서 형식의 열로 대량 로드 하 `uniqueidentifier` [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 고 XSD 값이 중괄호 ({및})를 포함 하는 GUID 인 경우 열에 값을 삽입 하기 전에 중괄호를 제거 하려면 **sql: datatype = "uniqueidentifier"** 를 지정 해야 합니다. `sql:datatype`을 지정하지 않으면 값이 중괄호와 함께 전송되어 삽입이 실패합니다.  
  
 에 대 한 자세한 내용은 `sql:datatype` [데이터 형식 강제 변환 및 sql: datatype 주석 &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)를 참조 하세요.  
  
 XDR  
  
-   `dt:type`이 `datetime`, `time`, `dateTime.tz` 또는 `time.tz`인 경우 XML 대량 로드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 보내기 전에 데이터 변환을 수행하기 때문에 `dt:type` 및 `sql:datatype` 데이터 형식을 모두 지정해야 합니다.  
  
-   XML 데이터가 형식인 경우 `uuid` 를 `sql:datatype` 지정 해야 합니다. **dt: type = "uuid"** 는 데이터가 문자열 데이터가 아닌 경우에도 필요 합니다. `dt:uuid`를 지정하지 않으면 XML 대량 로드에서는 중괄호가 포함된 문자열을 허용하고 필요한 경우 중괄호를 제거합니다.  
  
-   XML 데이터가 `bin.base64` 또는 `bin.hex` 형식이면 `dt:type`을 사용하여 XML 데이터 형식을 지정해야 합니다. 그러면 XML 대량 로드에서는 데이터의 16진수 표현으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 로드합니다.  
  
  
