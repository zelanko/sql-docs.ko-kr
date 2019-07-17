---
title: SQLSetParam 매핑 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c8d2d567f899c30dfe91cd35445956cd6214da9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125547"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 매핑
**SQLSetParam** 위쪽에 매핑할 계속 **SQLBindParameter** ODBC 2. *x*합니다. 개념적으로 유사한 것 **SQLBindParam**, 드라이버 관리자 매핑되지 **SQLSetParam** 에 **SQLBindParam**합니다. 왜냐하면 특정 기존 ODBC 2. *x* 특수 한 값을 사용 하는 드라이버 *BufferLength* (SQL_SETPARAM_VALUE_MAX) 매핑합니다 때 드라이버 관리자를 생성 하는 **SQLSetParam** 맨 위에  **SQLBindParameter** 를 1로 호출 되는 경우를 결정 합니다. *x* ODBC 응용 프로그램입니다.  
  
 에 대 한 호출  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 다음에 발생 합니다.  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
