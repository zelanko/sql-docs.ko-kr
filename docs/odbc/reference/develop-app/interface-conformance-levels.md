---
title: 인터페이스 적합성 수준 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304603"
---
# <a name="interface-conformance-levels"></a>인터페이스 적합성 수준
평준화의 목적은 드라이버에서 사용할 수 있는 기능을 응용 프로그램에 알리는 것입니다. 함수를 기반으로 하는 평준화 체계는 이 목표를 충분히 달성하지 못합니다. ODBC 3. *x*, 드라이버는 그들이 가지고있는 기능에 따라 분류됩니다. 이 기능을 지원하는 것은 기능을 지원하는 것을 포함할 수 있습니다. 또한 설명자 필드, 문 특성, **SQLGetInfo에서**반환되는 정보 유형에 대한 "Y" 값 등을 지원할 수도 있습니다.  
  
 ODBC는 인터페이스 적합성 사양을 단순화하기 위해 세 가지 적합성 수준을 정의합니다. 특정 적합성 수준을 충족하려면 드라이버는 해당 준수 수준의 모든 요구 사항을 충족해야 합니다. 주어진 레벨을 준수한다는 것은 모든 하위 레벨에 대한 완전한 적합성을 의미합니다.  
  
 적합성 수준이 항상 특정 ODBC 함수 목록에 대한 지원으로 깔끔하게 분할되는 것은 아니지만 다음 섹션에 나열된 대로 지원되는 피쳐를 지정합니다. 기능에 대한 지원을 제공하려면 드라이버는 특정 ODBC 함수에 대한 일부 또는 모든 형태의 호출(자세한 내용은 [함수 준수](../../../odbc/reference/develop-app/function-conformance.md)참조), 특정 특성 설정(특성 [준수](../../../odbc/reference/develop-app/attribute-conformance.md)참조) 및 특정 설명자 [필드(설명자 필드 적합성](../../../odbc/reference/develop-app/descriptor-field-conformance.md)참조)를 지원해야 합니다.  
  
 응용 프로그램은 데이터 원본에 연결하고 SQL_ODBC_INTERFACE_CONFORMANCE 옵션으로 **SQLGetInfo를** 호출하여 드라이버의 인터페이스 적합성 수준을 검색합니다.  
  
 드라이버는 완전한 적합성을 주장하는 수준 이상으로 기능을 자유롭게 구현할 수 있습니다. 응용 프로그램은 **SQLGetFunctions(존재하는** ODBC 함수를 결정하기 위해) 및 **SQLGetInfo(다른** 다양한 ODBC 기능을 쿼리하기 위해)를 호출하여 이러한 추가 기능을 검색합니다.  
  
 코어, 레벨 1 및 레벨 2의 세 가지 ODBC 인터페이스 준수 수준이 있습니다.  
  
> [!NOTE]
>  이러한 적합성 수준은 ODBC 2 *.x.* 특히 ODBC 2 *.x* API 준수 수준 수준 1에서 내포하는 모든 기능은 이제 코어 인터페이스 준수 레벨의 일부가 되었습니다. 따라서 많은 ODBC 드라이버가 코어 레벨 인터페이스 적합성을 보고할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [핵심 인터페이스 적합성](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [수준 1 인터페이스 적합성](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [수준 2 인터페이스 적합성](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [함수 적합성](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [특성 적합성](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [설명자 필드 적합성](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
