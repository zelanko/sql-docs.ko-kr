---
title: SQL 적합성 수준 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 875330ac78588566b4b1c212f7a65d2841127a61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301384"
---
# <a name="sql-conformance-levels"></a>SQL 적합성 수준
드라이버에서 지원하는 SQL-92 문법 수준은 SQL_SQL_CONFORMANCE 정보 형식을 사용하여 **SQLGetInfo** 호출에서 반환되는 값으로 표시됩니다. 이는 드라이버가 SQL-92에 정의된 항목, FIPS 전환, 중급 또는 전체 수준을 준수하는지 여부를 나타냅니다.  
  
 모든 ODBC 드라이버는 부록 C: SQL 문법의 [SQL 최소 문법에](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 설명된 최소 SQL 문법을 지원해야 합니다. 이 문법은 SQL-92의 엔트리 레벨의 하위 집합입니다. 드라이버는 추가 SQL을 지원하고 SQL-92 엔트리, 중급 또는 전체 수준 또는 FIPS 127-2 과도기 수준을 준수할 수 있습니다. 지정된 수준의 SQL-92 또는 FIPS 127-2를 준수하는 드라이버는 상위 수준의 추가 기능을 지원할 수 있지만 해당 수준에 완전히 부합하지는 않습니다. 기능이 지원되는지 여부를 확인하려면 응용 프로그램이 적절한 정보 형식을 사용하여 **SQLGetInfo를** 호출해야 합니다. SQL 기능의 적합성 수준은 해당 정보 유형에 설명되어 있습니다. [(SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명을 참조하십시오.)
