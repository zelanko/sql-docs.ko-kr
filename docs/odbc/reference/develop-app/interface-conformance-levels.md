---
title: 인터페이스 규칙 수준 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fff555324746fcb92641126ddf11ea91ce5e3f89
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304603"
---
# <a name="interface-conformance-levels"></a>인터페이스 적합성 수준
평준화의 목적은 드라이버에서 사용할 수 있는 기능을 응용 프로그램에 알리는 것입니다. 함수를 기반으로 하는 평준화 체계는이 목표를 달성 하는 데 충분 하지 않습니다. ODBC 3. *x*, 드라이버는 소유 하 고 있는 기능을 기준으로 분류 됩니다. 기능 지원에는 함수 지원이 포함 될 수 있습니다. 설명자 필드, 문 특성, **SQLGetInfo**에서 반환 하는 정보 형식에 대 한 "Y" 값 등을 지원 하기도 합니다.  
  
 인터페이스 규칙의 지정을 단순화 하기 위해 ODBC는 세 가지 규칙 수준을 정의 합니다. 특정 규칙 수준을 충족 하려면 드라이버가 해당 규칙 수준의 요구 사항을 모두 충족 해야 합니다. 지정 된 수준에 대 한 규칙은 모든 하위 수준에 대 한 완전 한 준수를 의미 합니다.  
  
 규칙 수준은 항상 특정 ODBC 함수 목록에 대 한 지원으로 깔끔하게 분할 되지는 않지만 다음 섹션에 나열 된 지원 되는 기능을 지정 합니다. 기능에 대 한 지원을 제공 하려면 드라이버는 특정 ODBC 함수에 대 한 일부 또는 모든 형태의 호출을 지원 해야 합니다 (자세한 내용은 [함수 규칙](../../../odbc/reference/develop-app/function-conformance.md)을 참조). 특정 특성 설정 ( [특성 규칙](../../../odbc/reference/develop-app/attribute-conformance.md)참조) 및 특정 설명자 필드 ( [설명자 필드 규칙](../../../odbc/reference/develop-app/descriptor-field-conformance.md)참조).  
  
 응용 프로그램은 데이터 원본에 연결 하 고 SQL_ODBC_INTERFACE_CONFORMANCE 옵션으로 **SQLGetInfo** 를 호출 하 여 드라이버의 인터페이스 규칙 수준을 검색 합니다.  
  
 드라이버는 완전 한 규칙을 준수 하는 수준 이상의 기능을 구현 하는 데 사용할 수 있습니다. 응용 프로그램은 **SQLGetFunctions** (odbc 함수를 결정 하기 위해)와 **SQLGetInfo** (다른 여러 odbc 기능을 쿼리 하기 위해)를 호출 하 여 이러한 추가 기능을 검색 합니다.  
  
 핵심, 수준 1 및 수준 2의 세 가지 ODBC 인터페이스 규칙 수준이 있습니다.  
  
> [!NOTE]
>  이러한 규칙 수준의 요구 사항은 ODBC 2.x에서 동일한 이름의 ODBC API 규칙 수준과*다릅니다.* 특히 ODBC*2.X API 규칙* 수준 1에서 암시 하는 모든 기능은 이제 핵심 인터페이스 규칙 수준의 일부입니다. 결과적으로 많은 ODBC 드라이버에서 핵심 수준 인터페이스 규칙을 보고할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [핵심 인터페이스 적합성](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [수준 1 인터페이스 적합성](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [함수 적합성](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [특성 적합성](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [설명자 필드 적합성](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
