---
description: SQL-92 CAST 함수
title: SQL-92 CAST 함수 | Microsoft Docs
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
ms.openlocfilehash: 7818cd653ac770de8f3d78d8599da5b66c4cf768
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424935"
---
# <a name="sql-92-cast-function"></a>SQL-92 CAST 함수
SQL-92에 정의 된 **CAST** 함수는 ODBC에 정의 된 **CONVERT** 함수와 동일 합니다. 동등한 함수의 구문은 다음과 같습니다.  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL-92 **CAST** 함수는 다른 데이터 형식으로 변환할 수 있는 데이터 형식을 규정 합니다. 자세한 내용은 SQL-92 사양을 참조 하십시오. **CAST** 함수는 FIPS 전환 수준에서 지원 됩니다.  
  
 응용 프로그램은 다음과 같이 **CAST** 함수에 대 한 지원을 확인할 수 있습니다.  
  
1.  SQL_SQL_CONFORMANCE 정보 형식으로 **SQLGetInfo** 를 호출 합니다. 정보 형식의 반환 값이 SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE 또는 SQL_SC_SQL92_FULL 인 경우 **CAST** 함수가 지원 됩니다.  
  
2.  SQL_SQL_CONFORMANCE 된 정보 형식의 반환 값이 SQL_SC_ENTRY_LEVEL 또는 0 인 경우 SQL_SQL92_VALUE_EXPRESSIONS 정보 형식으로 **SQLGetInfo** 를 호출 합니다. SQL_SVE_CAST 비트가 설정 되어 있으면 **CAST** 함수가 지원 됩니다.
