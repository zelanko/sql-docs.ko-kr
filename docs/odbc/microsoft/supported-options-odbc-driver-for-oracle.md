---
title: 지원되는 옵션(오라클용 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], supported options
ms.assetid: feefe0fd-5679-4c42-aa9e-e52b83f02544
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5dabb7130bb8eb1936d8cbaa946b31eb98210a3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307074"
---
# <a name="supported-options-odbc-driver-for-oracle"></a>지원되는 옵션(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 오라클의 ODBC 드라이버는 SQLGetConnectOption() 및 SQLSetConnectOption() 수준 1 함수에 대해 다음과 같은 옵션을 지원합니다.  
  
-   SQL_ACCESS_MODE[(SQLGetConnect옵션](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)() 만)  
  
-   [SQL_AUTOCOMMIT](../../odbc/microsoft/connect-options.md)  
  
-   [SQL_ODBC_CURSORS](../../odbc/microsoft/connect-options.md)  
  
-   [SQL_OPT_TRACEFILE](../../odbc/microsoft/connect-options.md)  
  
-   [SQL_OPT_TRACE](../../odbc/microsoft/connect-options.md)  
  
-   [SQL_TRANSLATE_DLL](../../odbc/microsoft/connect-options.md)  
  
-   [SQL_TRANSLATE_OPTION](../../odbc/microsoft/connect-options.md)  
  
-   [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)  
  
 오라클의 ODBC 드라이버는 SQLGetStmtOption() 및 SQLSetStmt옵션() 수준 1 함수에 대해 다음과 같은 옵션을 지원합니다.  
  
-   [SQL_BIND_TYPE](../../odbc/microsoft/statement-options.md)  
  
-   [SQL_CONCURRENCY](../../odbc/microsoft/statement-options.md)  
  
-   [SQL_CURSOR_TYPE](../../odbc/microsoft/statement-options.md)  
  
-   [SQL_KEYSET_SIZE](../../odbc/microsoft/statement-options.md)  
  
-   [SQL_MAX_ROWS](../../odbc/microsoft/statement-options.md)  
  
-   [SQL_ROWSET_SIZE](../../odbc/microsoft/statement-options.md)
