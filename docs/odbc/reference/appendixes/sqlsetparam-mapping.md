---
description: SQLSetParam 매핑
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2c16f942920b5fefff664cc647f4edfc9ab6d13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339299"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 매핑
**SQLSetParam** 는 ODBC 2와 마찬가지로 **SQLBindParameter** 를 기반으로 계속 매핑됩니다. *x*. **Sqlbindparam 함수와**와 개념적으로 유사 하지만 드라이버 관리자는 **SQLSetParam** 를 **sqlbindparam 함수와**에 매핑하지 않습니다. 이는 기존의 특정 ODBC 2가 있기 때문입니다. *x* 드라이버는 **SQLBindParameter** 를 **SQLSetParam** 매핑할 때 드라이버 관리자가 생성 하는 특수 한 값의 *bufferlength* (SQL_SETPARAM_VALUE_MAX)를 사용 하 여 1에 의해 호출 되는 시기를 결정 합니다. *x* ODBC 응용 프로그램.  
  
 호출입니다.  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 그러면 다음과 같은 결과가 발생 합니다.  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
