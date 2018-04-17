---
title: 받는 규칙 수준 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be780023002dba4422a6523f57866661fde593b7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="interface-conformance-levels"></a>인터페이스 받는 규칙 수준
평준화의 목적은 어떤 기능을 사용할 수에 드라이버에서 응용 프로그램에 알리기 위해 하는 것입니다. 함수 기반 평준화 체계 충분히이 목표를 달성 하지 않습니다. Odbc 3. *x*, 드라이버는 기능을 기반으로 분류 됩니다. 기능을 지 원하는 기능; 포함 될 수 있습니다. 반환 된 정보 유형에 대해 지원 되는 설명자 필드, 문 특성, "Y" 값을 포함할 수 **SQLGetInfo**등입니다.  
  
 ODBC를 간소화 하기 위해 인터페이스 규격의 사양을 세 받는 규칙 수준을 정의 합니다. 특정 규칙 수준을 충족 하기 위해 드라이버를 모든 해당 규칙에 따라 수준의 요구 사항을 충족 해야 합니다. 지정된 된 수준에 따라 모든 하위 수준으로 전체 준수를 의미합니다.  
  
 받는 규칙 수준 항상 나누지 마세요 깔끔하게 ODBC 함수의 특정 목록에 대 한 지원에 있지만 다음 섹션에 나열 된 지원 되는 기능을 지정 합니다. 기능에 대 한 지원을 제공 하는 드라이버 특정 ODBC 함수 호출을 일부 또는 모든 형태의 지원 해야 합니다 (자세한 내용은 참조 [함수 규칙](../../../odbc/reference/develop-app/function-conformance.md)), 특정 특성을 설정 (참조 [특성 규칙 ](../../../odbc/reference/develop-app/attribute-conformance.md)), 및 특정 설명자 필드 (참조 [설명자 필드 규칙](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 응용 프로그램은 데이터 원본에 연결 하 고 호출 하 여 드라이버의 인터페이스 규칙 수준 검색 **SQLGetInfo** SQL_ODBC_INTERFACE_CONFORMANCE 옵션을 사용 합니다.  
  
 드라이버는 자유롭게 완료 규칙을 요구 하는 수준 보다 더 뛰어난 기능을 구현할 수 있습니다. 응용 프로그램을 호출 하 여 이러한 추가 기능 검색 **SQLGetFunctions** (ODBC 함수를 사용할 수 있는지 결정)를 및 **SQLGetInfo** (ODBC의 다른 다양 한 기능을 쿼리)를 합니다.  
  
 세 가지 ODBC 인터페이스 규칙에 따라 수준이 있습니다: 코어, 수준 1 및 수준 2입니다.  
  
> [!NOTE]  
>  이러한 받는 규칙 수준 ODBC 2에 동일한 이름의 ODBC API 받는 규칙 수준 보다 각기 요구 사항이*.x*합니다. 특히, 모든 기능 사용 권한에 포함 된 ODBC 2*.x* API 규칙에 따라 수준 1 코어 인터페이스 규칙 수준에 포함 되었는지 합니다. 결과적으로, 대부분의 ODBC 드라이버는 핵심 수준 인터페이스 규칙을 보고할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [핵심 인터페이스 적합성](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [수준 1 인터페이스 적합성](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [함수 적합성](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [특성 적합성](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [설명자 필드 적합성](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
