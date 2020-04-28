---
title: SQL 규칙 수준 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301384"
---
# <a name="sql-conformance-levels"></a>SQL 적합성 수준
드라이버에서 지 원하는 SQL-92 문법 수준은 SQL_SQL_CONFORMANCE 정보 형식을 사용 하는 **SQLGetInfo** 호출에서 반환 된 값으로 표시 됩니다. 드라이버가 SQL-92에 정의 된 항목, FIPS 전환, 중간 또는 전체 수준을 따르는지 여부를 나타냅니다.  
  
 모든 ODBC 드라이버는 부록 C: SQL 문법의 [Sql 최소 문법](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 에 설명 된 최소 sql 문법을 지원 해야 합니다. 이 문법은 SQL-92의 항목 수준 하위 집합입니다. 드라이버는 추가 SQL을 지원 하 고 SQL-92 항목, 중간 또는 전체 수준 또는 FIPS 127-2 전환 수준에 부합 될 수 있습니다. 지정 된 수준의 SQL-92 또는 FIPS 127-2를 준수 하는 드라이버는 더 높은 수준의 추가 기능을 지원할 수 있지만 해당 수준에 완전히 부합 되지 않습니다. 기능이 지원 되는지 여부를 확인 하기 위해 응용 프로그램은 적절 한 정보 형식으로 **SQLGetInfo** 를 호출 해야 합니다. SQL 기능의 규칙 수준은 해당 정보 형식에 설명 되어 있습니다. ( [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명을 참조 하세요.)
