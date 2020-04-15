---
title: SQLSetParam 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8e632412965664e5cdd9c87dc1e26787dcdab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300533"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 매핑
**SQLSetParam은** ODBC 2에서와 같이 **SQLBindParameter** 위에 계속 매핑됩니다. *x*. **SQLBindParam과**개념적으로 유사하지만 드라이버 관리자는 **SQLSetParam을** **SQLBindParam에**매핑하지 않습니다. 이는 특정 기존 ODBC 2이기 때문입니다. *x* 드라이버는 드라이버 관리자가 **SQLBindParameter** 위에 **SQLSetParam을** 매핑할 때 생성되는 *BufferLength(SQL_SETPARAM_VALUE_MAX)의* 특수 값을 사용하여 1에 의해 호출되는 시기를 결정합니다. *x* ODBC 응용 프로그램.  
  
 에 대한 호출  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 다음과 같은 결과가 발생합니다.  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
