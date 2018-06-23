---
title: 데이터 형식 및 XML 대량 로드 동작 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 752dca45eb12e4148ab407b578d0f4161444ece9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088563"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>데이터 형식과 XML 대량 로드 동작(SQLXML 4.0)
  매핑 스키마(XSD 또는 XDR 형식 및 `sql:datatype`)에 지정된 데이터 형식은 일반적으로 다음 경우를 제외하고는 무시됩니다.  
  
 XSD  
  
-   `dateTime` 또는 `time` 형식의 경우 XML 대량 로드는 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 보내기 전에 데이터 변환을 수행하기 때문에 `sql:datatype`을 지정해야 합니다.  
  
-   열에 대량 로드 하는 경우 `uniqueidentifier` 에 입력 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XSD 값이 중괄호 ({및}), 사용자를 포함 하는 GUID를 지정 해야 하 고 **sql: datatype = "uniqueidentifier"** 전에 값이 중괄호를 제거 하려면 열에 삽입 합니다. `sql:datatype`을 지정하지 않으면 값이 중괄호와 함께 전송되어 삽입이 실패합니다.  
  
 에 대 한 자세한 내용은 `sql:datatype`, 참조 [데이터 형식 강제 변환 및 sql: datatype 주석 &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)합니다.  
  
 XDR  
  
-   `dt:type`이 `datetime`, `time`, `dateTime.tz` 또는 `time.tz`인 경우 XML 대량 로드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 보내기 전에 데이터 변환을 수행하기 때문에 `dt:type` 및 `sql:datatype` 데이터 형식을 모두 지정해야 합니다.  
  
-   XML 데이터 형식인 경우 `uuid`, `sql:datatype` 지정 해야 하며 **dt: type = "uuid"** 표시 되지 않으면도 필요한 경우 데이터는 문자열 데이터. `dt:uuid`를 지정하지 않으면 XML 대량 로드에서는 중괄호가 포함된 문자열을 허용하고 필요한 경우 중괄호를 제거합니다.  
  
-   XML 데이터가 `bin.base64` 또는 `bin.hex` 형식이면 `dt:type`을 사용하여 XML 데이터 형식을 지정해야 합니다. 그러면 XML 대량 로드에서는 데이터의 16진수 표현으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 로드합니다.  
  
  