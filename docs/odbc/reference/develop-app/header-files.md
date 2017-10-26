---
title: "헤더 파일 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8cec0dc5105addb28606a12c99dd2d77b0a48a64
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="header-files"></a>헤더 파일
헤더 파일 Sql.h 함수 및 기능 ODBC 핵심 인터페이스 규칙 수준에 대 한 프로토타입이 포함 되어 있습니다. Sqlext.h 헤더 파일에는 함수 및 기능 수준 1 및 수준 2 API 받는 규칙 수준에 대 한 프로토타입이 포함 됩니다. 형식 정 및 SQL 데이터 형식에 대 한 표시기 Sqltypes.h 헤더 파일에 포함 되어 있습니다.  
  
 모두 포함 하는 헤더 파일을 **#define**, 응용 프로그램 또는 드라이버는 ODBC의 버전 마다 컴파일할 설정할 수 있는 ODBCVER 합니다.  
  
 ISO CLI 및 Open 그룹 CLI 맞춰 헤더 파일에 대 한 호출에 사용 되는 정보 종류에 대 한 별칭을 포함 **SQLGetInfo**합니다. 다음 표에서 "ODBC name" 열에는 정보 유형은 ODBC 이름을 나타냅니다. [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)합니다. "헤더 파일에서 별칭" 열에는 ISO CLI 및 Open 그룹 CLI에 사용 되는 이름을 나타냅니다. 이러한 매니페스트 이름의 실제 숫자 값은 ODBC와 표준 Cli에 같습니다. 이러한 별칭을 통해 표준 호환 응용 프로그램 또는 드라이버는 ODBC 3로 컴파일하려면*.x* 헤더 파일입니다.  
  
 이러한 별칭 이름을 더 이해할 수 있도록 ODBC 이름에 약어의 확장을 포함 합니다. "MAX" 확장 되어 "최대", "LEN"를 "LENGTH", "MULT"를 "OUTER_JOIN"를 "여러", "OJ" 및 "트랜잭션"을 "TXN"  
  
|ODBC 이름|헤더 파일에 대 한 별칭|  
|---------------|--------------------------|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAXIMUM_CATALOG_NAME_LENGTH|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAXIMUM_COLUMN_NAME_LENGTH|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAXIMUM_COLUMNS_IN_GROUP_BY|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAXIMUM_COLUMNS_IN_ORDER_BY|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAXIMUM_COLUMNS_IN_SELECT|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAXIMUM_COLUMNS_IN_TABLE|  
|SQL_MAX_CONCURRENT_ACTIVITIES|SQL_MAXIMUM_CONCURRENT_ACTIVITIES|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAXIMUM_CURSOR_NAME_LENGTH|  
|SQL_MAX_DRIVER_CONNECTIONS|SQL_MAXIMUM_DRIVER_CONNECTIONS|  
|SQL_MAX_IDENTIFIER_LEN|SQL_MAXIMUM_IDENTIFIER_LENGTH|  
|SQL_MAX_SCHEMA_NAME_LEN|SQL_MAXIMUM_SCHEMA_NAME_LENGTH|  
|SQL_MAX_STATEMENT_LEN|SQL_MAXIMUM_STATEMENT_LENGTH|  
|SQL_MAX_TABLE_NAME_LEN|SQL_MAXIMUM_TABLE_NAME_LENGTH|  
|SQL_MAX_TABLES_IN_SELECT|SQL_MAXIMUM_TABLES_IN_SELECT|  
|SQL_MAX_USER_NAME_LEN|SQL_MAXIMUM_USER_NAME_LENGTH|  
|SQL_MULT_RESULT_SETS|SQL_MULTIPLE_RESULT_SETS|  
|SQL_OJ_CAPABILITIES|SQL_OUTER_JOIN_CAPABILITIES|  
|SQL_TXN_CAPABLE|SQL_TRANSACTION_CAPABLE|  
|SQL_TXN_ISOLATION_OPTION|SQL_TRANSACTION_ISOLATION_OPTION|

