---
title: "SQL 받는 규칙 수준 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d397eef2bec5e803cca97f05d009708273a05473
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-conformance-levels"></a>SQL 받는 규칙 수준
드라이버에서 지 원하는 SQL 92 문법의 수준에 대 한 호출에서 반환 된 값으로 표시 됩니다 **SQLGetInfo** SQL_SQL_CONFORMANCE 정보 유형을 사용 합니다. 이 드라이버는 SQL 92에 정의 된 항목, FIPS 전환, 중간, 또는 전체 수준이에 맞는지 여부를 나타냅니다.  
  
 모든 ODBC 드라이버에 설명 된 최소 SQL 문법을 지원 해야 [최소 SQL 문법을](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 부록 c: SQL 문법에 있습니다. 이 문법에는 SQL 92 항목 수준의 일부입니다. 드라이버는 추가 SQL을 지원 하 고와 호환 되는 SQL 92 항목, 중간, 또는 전체 수준 또는 FIPS 127-2 전환 수준 될 수 있습니다. S Q l 92 또는 FIPS 127-2의 지정 된 수준에 따라 드라이버의 더 높은 수준에서 추가 기능을 지원 하면서 완벽 하 게 해당 수준에 부합 되지 수 있습니다. 기능이 지원 되는지 여부를 확인 하려면 응용 프로그램 호출 해야 **SQLGetInfo** 적절 한 정보 형식을 사용 합니다. SQL 기능의 규칙 수준과 해당 정보 유형을 설명 합니다. (참조는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.)
