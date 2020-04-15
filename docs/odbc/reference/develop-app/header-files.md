---
title: 헤더 파일 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62364d828e7b1f1ed8c70cae7ae1fc7dc3bc33fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300193"
---
# <a name="header-files"></a>헤더 파일
Sql.h 헤더 파일에는 코어 ODBC 인터페이스 준수 수준의 함수 및 기능에 대한 프로토타입이 포함되어 있습니다. Sqlext.h 헤더 파일에는 수준 1 및 수준 2 API 준수 수준의 함수 및 기능에 대한 프로토타입이 포함되어 있습니다. Sqltypes.h 헤더 파일에는 SQL 데이터 형식에 대한 형식 정의 및 표시등이 포함되어 있습니다.  
  
 헤더 파일에는 모두 응용 프로그램 또는 드라이버가 다른 버전의 ODBC에 대해 컴파일되도록 설정할 수 있는 **#define**ODBCVER가 포함되어 있습니다.  
  
 ISO CLI 및 열기 그룹 CLI에 맞추기 위해 헤더 파일에는 **SQLGetInfo**에 대한 호출에 사용되는 정보 유형에 대한 별칭이 포함되어 있습니다. 다음 표에서 "ODBC 이름" 열은 [ODBC API 참조의](../../../odbc/reference/syntax/odbc-api-reference.md)정보 형식에 대한 ODBC 이름을 나타냅니다. "헤더 파일의 별칭" 열은 ISO CLI 및 열린 그룹 CLI에 사용되는 이름을 나타냅니다. 이러한 매니페스트 이름의 실제 숫자 값은 ODBC와 표준 CLI 모두에서 동일합니다. 이러한 별칭을 사용하면 표준을 준수하는 응용 프로그램 이나 드라이버가 ODBC *3.x* 헤더 파일로 컴파일할 수 있습니다.  
  
 이러한 별칭에는 ODBC 이름의 약어 확장이 포함되어 있으므로 이름을 더 이해할 수 있습니다. "MAX"는 "최대", "LEN"에서 "길이"로, "MULT"에서 "MULTIPLE"으로, "OJ"를 "OUTER_JOIN"로, "TXN"을 "트랜잭션"으로 확장합니다.  
  
|ODBC 이름|헤더 파일의 별칭|  
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
