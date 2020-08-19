---
description: 문자열 매개 변수를 수락하는 함수
title: 문자열 매개 변수를 허용 하는 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], string parameters
- ODBC desktop database drivers [ODBC], string parameters
- Jet-based ODBC drivers [ODBC], string parameters
- functions [ODBC], string parameters
- string parameters [ODBC]
ms.assetid: 869b8421-f71e-4dfd-adce-691bd3012b16
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f634e65260332851d02d2fe67302f03529a6ff7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421857"
---
# <a name="functions-accepting-string-parameters"></a>문자열 매개 변수를 수락하는 함수
문자열 매개 변수를 사용 하는 모든 함수는 유니코드로 변환 됩니다. (함수의 "W" 형태를 내보냅니다.) 바이트 수는 해당 하는 ODBC Api에 대 한 문자 수로 변환 됩니다. 이는 다음 함수에 적용 됩니다.  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLColAttributes**  
  
-   **SQLDescribeCol**  
  
-   **SQLError** ( **SQLGetDiagField**로 바뀜)  
  
-   **SQLExecDirect**  
  
-   **SQLGetCursorName**  
  
-   **SQLSetCursorName**  
  
-   **SQLGetStmtAttr**  
  
-   **SQLGetInfo**  
  
-   **SQLGetStmtOption** ( **SQLGetStmtAttr**)  
  
-   **SQLSetStmtOption** ( **SQLSetStmtAttr**)  
  
-   **SQLGetConnectOption**  
  
-   **SQLSetConnectOption**  
  
-   **SQLGetTypeInfo**  
  
-   **SQLStatistics**  
  
-   **SQLTables**  
  
-   **SQLNativeSQL**  
  
-   **SQLSpecialColumns**  
  
-   **ConfigDSNEx**  
  
-   **ConfigDSN**
