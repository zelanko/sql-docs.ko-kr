---
title: 문자열 매개 변수를 수락하는 함수 | 마이크로 소프트 문서
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
ms.openlocfilehash: 01d0f143c72f57e946f7fe2bf52a50910d4e56aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286303"
---
# <a name="functions-accepting-string-parameters"></a>문자열 매개 변수를 수락하는 함수
문자열 매개 변수를 취하는 모든 함수는 유니코드로 변환됩니다. (함수의 "W" 형식이 내보내집니다.) 바이트 수는 해당 ODBC API에 대한 문자 수로 변환됩니다. 이는 다음 함수에 적용됩니다.  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLCol속성**  
  
-   **SQLDescribeCol**  
  
-   **SQLError** **(SQLGetDiagField로**대체)  
  
-   **SQLExecDirect**  
  
-   **SQLGetCursorName**  
  
-   **SQLSetCursorName**  
  
-   **SQLGetStmtAttr**  
  
-   **SQLGetInfo**  
  
-   **SQLGetStmt옵션(SQLGetStmtAttr이**됨) **SQLGetStmtOption**  
  
-   **SQLSetStmt옵션(SQLSetStmtAttr)** **SQLSetStmtOption**  
  
-   **SQLGet연결 옵션**  
  
-   **SQLSet연결옵션**  
  
-   **SQLGetTypeInfo**  
  
-   **SQLStatistics**  
  
-   **SQLTables**  
  
-   **SQL네이티브SQL**  
  
-   **SQLSpecialColumns**  
  
-   **콘피그드스넥스**  
  
-   **구성DSN**
