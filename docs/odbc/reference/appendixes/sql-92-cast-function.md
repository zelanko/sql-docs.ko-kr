---
title: SQL-92 캐스트 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09d2a2de710dafd4e744166c4219f4c903fd3321
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305064"
---
# <a name="sql-92-cast-function"></a>SQL-92 CAST 함수
SQL-92에 정의된 **CAST** 함수는 ODBC에 정의된 **CONVERT** 함수와 동일합니다. 동등한 함수의 구문은 다음과 같습니다.  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL-92 **CAST** 함수는 다른 데이터 유형으로 변환할 수 있는 데이터 형식을 요구합니다. 자세한 내용은 SQL-92 사양을 참조하십시오. **CAST** 함수는 FIPS 전환 수준에서 지원됩니다.  
  
 응용 프로그램은 다음과 같이 **CAST** 함수에 대한 지원을 결정할 수 있습니다.  
  
1.  SQL_SQL_CONFORMANCE 정보 유형을 통해 **SQLGetInfo를** 호출합니다. 정보 형식의 반환 값이 SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE 또는 SQL_SC_SQL92_FULL 경우 **CAST** 함수가 지원됩니다.  
  
2.  SQL_SQL_CONFORMANCE 정보 형식의 반환 값이 SQL_SC_ENTRY_LEVEL 또는 0인 경우 SQL_SQL92_VALUE_EXPRESSIONS 정보 형식을 통해 **SQLGetInfo를** 호출합니다. SQL_SVE_CAST 비트가 설정된 경우 **CAST** 함수가 지원됩니다.
