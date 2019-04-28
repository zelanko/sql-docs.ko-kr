---
title: 헤더 파일 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e6d0806a7c3eabd1c6f4cd1836308eba99a6d5a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724368"
---
# <a name="header-files"></a>헤더 파일
헤더 파일 Sql.h ODBC는 핵심 인터페이스 적합성 수준에서 기능에 대 한 프로토타입이 포함 되어 있습니다. Sqlext.h 헤더 파일에는 수준 1 및 수준 2 API 적합성 수준 기능에 대 한 프로토타입을 포함 되어 있습니다. 형식 정 및 SQL 데이터 형식에 대 한 지표 Sqltypes.h 헤더 파일에 포함 되어 있습니다.  
  
 모두 포함 하는 헤더 파일을 **#define**, ODBCVER 응용 프로그램 또는 드라이버는 ODBC의 다른 버전에 대해 컴파일해야 설정할 수는 있습니다.  
  
 ISO CLI 및 열린 그룹 CLI를 사용 하 여 맞게 헤더 파일에 대 한 호출에 사용 되는 정보 유형에 대 한 별칭을 포함 **SQLGetInfo**합니다. 다음 표에서 "ODBC name" 열 정보 형식에 대 한 ODBC 이름을 나타냅니다 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)합니다. "헤더 파일에서 별칭" 열에는 ISO CLI 및 열린 그룹 CLI에서 사용 되는 이름을 나타냅니다. 이러한 매니페스트 이름의 실제 숫자 값은 ODBC 및 표준 Cli 모두에서 동일 합니다. 표준 호환 응용 프로그램 또는 드라이버는 ODBC 3을 사용 하 여 컴파일하는 데 이러한 별칭을 사용 하도록 설정 *.x* 헤더 파일입니다.  
  
 이러한 별칭 이름을 더 이해할 수 있도록 ODBC 이름에 약어의 확장을 포함 합니다. "MAX"은 "OUTER_JOIN"에 "여러", "OJ" 및 "트랜잭션" "transaction."를 "최대", "LEN" "LENGTH", "MULT"까지 확장 되어  
  
|ODBC 이름|헤더 파일에서 별칭|  
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
