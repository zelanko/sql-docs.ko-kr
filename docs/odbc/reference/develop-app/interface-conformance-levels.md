---
title: 인터페이스 적합성 수준 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 185e68ed8d083e3ccfbab99369f6a778766a4c09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138908"
---
# <a name="interface-conformance-levels"></a>인터페이스 적합성 수준
사용할 수 있는 기능을 드라이버에서 응용 프로그램에 알리기 위해 평준화의 목적은입니다. 함수를 기반으로 평준화 체계를 충분히이 목표를 얻지 않습니다. Odbc 3. *x*, 드라이버는 소유 하는 기능을 기반으로 분류 됩니다. 기능을 지 원하는 함수를 지 원하는 포함 될 수 있습니다. 반환 된 정보 유형에 대 한 설명자 필드, 문 특성, "Y" 값을 지 원하는 포함할 수도 있습니다 **SQLGetInfo**등입니다.  
  
 ODBC를 간소화 하기 위해 인터페이스 적합성 사양의 세 적합성 수준을 정의 합니다. 특정 규칙 수준을 달성 하기 위해 드라이버를 모든 해당 규칙 수준의 요구 사항을 충족 해야 합니다. 지정된 된 수준에 따라 모든 하위 수준으로 전체 준수를 의미합니다.  
  
 적합성 수준 항상 나누지 마세요 깔끔하게 ODBC 함수의 특정 목록에 대 한 지원 하지만 다음 섹션에 나열 된 지원 되는 기능을 지정 합니다. 기능을 지원 하기 위해 드라이버를 일부 또는 모든 형태의 특정 ODBC 함수 호출을 지원 해야 합니다 (자세한 내용은 [함수 적합성](../../../odbc/reference/develop-app/function-conformance.md)), 특정 특성을 설정 (참조 [특성 적합성 ](../../../odbc/reference/develop-app/attribute-conformance.md)), 및 특정 설명자 필드 (참조 [설명자 필드 적합성](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 응용 프로그램은 데이터 원본에 연결 하 고 호출 하 여 운전 인터페이스 적합성 수준 검색 **SQLGetInfo** SQL_ODBC_INTERFACE_CONFORMANCE 옵션을 사용 합니다.  
  
 드라이버는 전체 규칙 클레임을 수준 이상의 기능을 구현 하는 무료입니다. 호출 하 여 이러한 모든 추가 기능을 검색 하는 응용 프로그램 **SQLGetFunctions** (결정할 ODBC 함수를 사용할 수 있는) 및 **SQLGetInfo** (다른 다양 한 ODBC 기능 쿼리)를 합니다.  
  
 ODBC 인터페이스 적합성 수준 세 가지 Core, 수준 1 및 수준 2입니다.  
  
> [!NOTE]
>  이러한 적합성 수준 ODBC 2에 있는 동일한 이름의 ODBC API 적합성 수준 보다 다양 한 요구 사항이 *.x*합니다. ODBC 2에 의해 모든 기능을 포함 하는 특히 *.x* API 규칙 Level 1 Core 인터페이스 적합성 수준 포함 됩니다. 결과적으로, 대부분의 ODBC 드라이버는 핵심 수준 인터페이스 적합성을 보고할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [핵심 인터페이스 적합성](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [수준 1 인터페이스 적합성](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [함수 적합성](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [특성 적합성](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [설명자 필드 적합성](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
