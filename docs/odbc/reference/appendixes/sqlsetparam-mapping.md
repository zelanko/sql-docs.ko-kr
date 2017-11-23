---
title: "SQLSetParam 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 43f15984f487dec8e77fd429f823c083c6c08a5b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 매핑
**SQLSetParam** 위쪽에 매핑할 수는 계속 **SQLBindParameter** 에서처럼 ODBC 2. *x*합니다. 개념적으로 유사한 것 **SQLBindParam**, 드라이버 관리자를 매핑하지 않습니다 **SQLSetParam** 를 **SQLBindParam**합니다. 즉, 특정 기존 ODBC 2. *x* 의 특수 한 값을 사용 하는 드라이버 *BufferLength* (SQL_SETPARAM_VALUE_MAX) 매핑하므로 때 드라이버 관리자에서 생성 하 **SQLSetParam** 맨 위에  **SQLBindParameter** 1로 호출 될 때 확인 하려면. *x* ODBC 응용 프로그램입니다.  
  
 에 대 한 호출  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 에 다음 사항이 적용 됩니다.  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
