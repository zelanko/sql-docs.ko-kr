---
description: 헤더 파일
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec8eede80f88f10e0b1ca43696e75dddec121ffe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476655"
---
# <a name="header-files"></a>헤더 파일
Sql .h 헤더 파일에는 핵심 ODBC 인터페이스 규칙 수준의 함수 및 기능에 대 한 프로토타입이 포함 되어 있습니다. Sqlext .h 헤더 파일에는 수준 1 및 수준 2 API 규칙 수준의 함수 및 기능에 대 한 프로토타입이 포함 되어 있습니다. Sqltypes 헤더 파일에는 SQL 데이터 형식에 대 한 형식 정의와 표시기가 포함 되어 있습니다.  
  
 헤더 파일에는 응용 프로그램 또는 드라이버가 서로 다른 버전의 ODBC에 대해 컴파일되도록 설정할 수 있는 **#define**ODBCVER이 포함 되어 있습니다.  
  
 ISO CLI에 맞추고 그룹 CLI를 열면 헤더 파일에 **SQLGetInfo**호출에 사용 되는 정보 형식에 대 한 별칭이 포함 됩니다. 다음 표에서 "ODBC 이름" 열은 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)의 정보 유형에 대 한 odbc 이름을 나타냅니다. "헤더 파일의 별칭" 열은 ISO CLI 및 오픈 그룹 CLI에서 사용 되는 이름을 나타냅니다. 이러한 매니페스트 이름의 실제 숫자 값은 ODBC와 표준 CLIs에서 동일 합니다. 이러한 별칭을 사용 하면 표준 규격 응용 프로그램 또는 드라이버 *에서 ODBC 2.x* 헤더 파일을 사용 하 여 컴파일할 수 있습니다.  
  
 이러한 별칭에는 이름이 더 이해 하기 쉽도록 ODBC 이름에 약어 확장이 포함 되어 있습니다. "MAX"는 "MAXIMUM", "LEN" to "LENGTH", "MULT" to "MULTIPLE", "OJ" to "OUTER_JOIN" 및 "TRANSACTION"으로 확장 됩니다.  
  
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
