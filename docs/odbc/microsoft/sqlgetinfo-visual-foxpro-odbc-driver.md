---
description: SQLGetInfo(Visual FoxPro ODBC 드라이버)
title: SQLGetInfo (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: fbc39e3d-67d9-4331-bf5f-76dbd74c4c45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 370661a9a0ade5c5159f93a9af37c17b675032c3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421677"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 연결 핸들 *hdbc*와 연결 된 VISUAL FoxPro ODBC 드라이버 및 데이터 원본에 대 한 일반 정보를 반환 합니다. 다음 목록에서는 각 *Finfotype* 인수에 대해 VISUAL FoxPro ODBC 드라이버에서 반환 되는 값과 반환 된 값에 대 한 설명을 보여 줍니다.  
  
 자세한 내용은 *ODBC 프로그래머 참조*에서 [SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md) 를 참조 하세요.  
  
## <a name="a"></a>A  
 SQL_ACCESSIBLE_PROCEDURES에서 ' N '을 반환 합니다.  
  
 SQL_ACCESSIBLE_TABLES는 ' Y '를 반환 합니다.  
  
 SQL_ACTIVE_CONNECTIONS는 0을 반환 합니다.  
  
 SQL_ACTIVE_STATEMENTS는 0을 반환 합니다.  
  
 SQL_ALTER_TABLE SQL_AT_ADD_COLUMN 또는 SQL_AT_DROP_COLUMN 반환 합니다.  
  
## <a name="b"></a>b  
 SQL_BOOKMARK_PERSISTENCE SQL_BP_SCROLL를 반환 합니다.  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS는 ' Y '를 반환 합니다.  
  
 SQL_CONCAT_NULL_BEHAVIOR SQL_CB_NULL를 반환 합니다.  
  
 SQL_CONVERT_BIGINT는 0을 반환 합니다. Visual FoxPro ODBC 드라이버는 *BigInt*를 지원 하지 않습니다.  
  
 SQL_CONVERT_BINARY는 0을 반환 합니다.  
  
 SQL_CONVERT_BIT는 0을 반환 합니다.  
  
 SQL_CONVERT_CHAR는 0을 반환 합니다.  
  
 SQL_CONVERT_DATE는 0을 반환 합니다.  
  
 SQL_CONVERT_DECIMAL는 0을 반환 합니다.  
  
 SQL_CONVERT_DOUBLE는 0을 반환 합니다.  
  
 SQL_CONVERT_FLOAT는 0을 반환 합니다.  
  
 SQL_CONVERT_INTEGER는 0을 반환 합니다.  
  
 SQL_CONVERT_LONGVARBINARY는 0을 반환 합니다.  
  
 SQL_CONVERT_LONGVARCHAR는 0을 반환 합니다.  
  
 SQL_CONVERT_NUMERIC는 0을 반환 합니다.  
  
 SQL_CONVERT_REAL는 0을 반환 합니다.  
  
 SQL_CONVERT_SMALLINT는 0을 반환 합니다.  
  
 SQL_CONVERT_TIME는 0을 반환 합니다.  
  
 SQL_CONVERT_TIMESTAMP는 0을 반환 합니다.  
  
 SQL_CONVERT_TINYINT는 0을 반환 합니다.  
  
 SQL_CONVERT_VARBINARY는 0을 반환 합니다.  
  
 SQL_CONVERT_VARCHAR는 0을 반환 합니다.  
  
 SQL_CONVERT_FUNCTIONS는 0을 반환 합니다.  
  
 SQL_CORRELATION_NAME SQL_CN_ANY를 반환 합니다.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR SQL_CB_PRESERVE를 반환 합니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR SQL_CB_PRESERVE를 반환 합니다.  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)또는 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)에 DSN으로 전달 된 값을 반환 합니다. DSN이 지정 되지 않은 경우 빈 문자열을 반환 합니다.  
  
 SQL_DATA_SOURCE_READ_ONLY에서 ' N '을 반환 합니다.  
  
 데이터 원본이 [데이터베이스인](../../odbc/microsoft/visual-foxpro-terminology.md)경우 SQL_DATABASE_NAME는 현재 데이터베이스에 대 한 전체 UNC 경로를 반환 합니다. 데이터 원본이 [테이블](../../odbc/microsoft/visual-foxpro-terminology.md)의 디렉터리에 연결 되는 경우이 함수는 디렉터리에 대 한 경로를 반환 합니다.  
  
 SQL_DBMS_NAME "Visual FoxPro"를 반환 합니다.  
  
 SQL_DBMS_VER "03.00.0000"를 반환 합니다.  
  
 SQL_DEFAULT_TXN_ISOLATION SQL_TXN_READ_COMMITTED를 반환 합니다. 더티 읽기는 불가능 하지만 반복할 reads 및 phantoms를 사용할 수 있습니다.  
  
 SQL_DRIVER_HDBC는 드라이버 관리자에 의해 구현 됩니다.  
  
 SQL_DRIVER_HENV는 드라이버 관리자에 의해 구현 됩니다.  
  
 SQL_DRIVER_HLIB는 드라이버 관리자에 의해 구현 됩니다.  
  
 SQL_DRIVER_HSTMT는 드라이버 관리자에 의해 구현 됩니다.  
  
 SQL_DRIVER_NAME "vfpodbc.dll"를 반환 합니다.  
  
 SQL_DRIVER_ODBC_VER "02.50" (SQL_SPEC_MAJOR, SQL_SPEC_MINOR)을 반환 합니다.  
  
 SQL_DRIVER_VER "01.00.0000"를 반환 합니다.  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY에서 ' N '을 반환 합니다.  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION 반환:  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK.  
  
 SQL_FILE_USAGE는 데이터베이스 (dbc 파일)와 자유 테이블 (.dbf 파일) 데이터 원본에 대 한 SQL_FILE_QUALIFIER 반환 합니다.  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS 반환:  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY SQL_GB_NO_RELATION를 반환 합니다.  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE SQL_IC_MIXED를 반환 합니다.  
  
 SQL_IDENTIFIER_QUOTE_CHAR 반환 합니다.  
  
## <a name="k"></a>K  
 SQL_KEYWORDS ""를 반환 합니다.  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE에서 ' N '을 반환 합니다.  
  
 SQL_LOCK_TYPES SQL_LCK_NO_CHANGE를 반환 합니다.  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN는 0을 반환 합니다.  
  
 SQL_MAX_CHAR_LITERAL_LEN는 254을 반환 합니다.  
  
 SQL_MAX_COLUMN_NAME_LEN는 128을 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY는 16을 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY는 16을 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_INDEX는 0을 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_SELECT는 254을 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_TABLE는 254을 반환 합니다.  
  
 SQL_MAX_CURSOR_NAME_LEN는 254을 반환 합니다.  
  
 SQL_MAX_INDEX_SIZE는 0을 반환 합니다.  
  
 SQL_MAX_OWNER_NAME_LEN는 0을 반환 합니다.  
  
 SQL_MAX_PROCEDURE_NAME_LEN는 0을 반환 합니다. Visual FoxPro ODBC 드라이버는 Visual FoxPro 저장 프로시저에 대 한 직접 액세스를 허용 하지 않습니다.  
  
 SQL_MAX_QUALIFIER_NAME_LEN은 최대 운영 체제 경로 길이를 반환 합니다.  
  
 SQL_MAX_ROW_SIZE은 254 ^ 2를 반환 합니다.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG에서 ' N '을 반환 합니다.  
  
 SQL_MAX_STATEMENT_LEN는 8192을 반환 합니다.  
  
 SQL_MAX_TABLE_NAME_LEN는 128을 반환 합니다.  
  
 SQL_MAX_TABLES_IN_SELECT는 16을 반환 합니다.  
  
 SQL_MAX_USER_NAME_LEN는 0을 반환 합니다.  
  
 SQL_MULT_RESULT_SETS는 ' Y '를 반환 합니다.  
  
 SQL_MULTIPLE_ACTIVE_TXN는 ' Y '를 반환 합니다. 여러 연결에서 한 번에 여러 트랜잭션을 열 수 있습니다.  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN에서 ' N '을 반환 합니다.  
  
 SQL_NON_NULLABLE_COLUMNS SQL_NNC_NON_NULL를 반환 합니다.  
  
 SQL_NULL_COLLATION SQL_NC_LOW를 반환 합니다.  
  
 SQL_NUMERIC_FUNCTIONS는 Visual FoxPro ODBC 드라이버에서 지원 하지 않는 SQL_FN_NUM_POWER를 제외한 모든 함수를 반환 합니다. 지원되는 함수는 다음과 같습니다.  
  
-   SQL_FN_NUM_ABS  
  
-   SQL_FN_NUM_ACOS  
  
-   SQL_FN_NUM_ASIN  
  
-   SQL_FN_NUM_ATAN  
  
-   SQL_FN_NUM_ATAN2  
  
-   SQL_FN_NUM_CELING  
  
-   SQL_FN_NUM_COS  
  
-   SQL_FN_NUM_COT  
  
-   SQL_FN_NUM_DEGREES  
  
-   SQL_FN_NUM_EXP  
  
-   SQL_FN_NUM_FLOOR  
  
-   SQL_FN_NUM_LOG  
  
-   SQL_FN_NUM_LOG10  
  
-   SQL_FN_NUM_MOD  
  
-   SQL_FN_NUM_PI  
  
-   SQL_FN_NUM_RADIANS  
  
-   SQL_FN_NUM_RAND  
  
-   SQL_FN_NUM_ROUND  
  
-   SQL_FN_NUM_SIGN  
  
-   SQL_FN_NUM_SIN  
  
-   SQL_FN_NUM_SQRT  
  
-   SQL_FN_NUM_TAN  
  
## <a name="o"></a>O  
 SQL_ODBC_API_CONFORMANCE SQL_OAC_LEVEL1를 반환 합니다.  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE SQL_OSCC_COMPLIANT를 반환 합니다.  
  
 SQL_ODBC_SQL_CONFORMANCE SQL_OSC_MINIMUM를 반환 합니다. 최소 SQL 구문이 지원 됩니다.  
  
 SQL_ODBC_SQL_OPT_IEF "N"을 반환 합니다.  
  
 SQL_ODBC_VER는 드라이버 관리자에 의해 구현 됩니다.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT "N"을 반환 합니다.  
  
 SQL_OUTER_JOINS "N"을 반환 합니다.  
  
 SQL_OWNER_TERM ""를 반환 합니다. Visual FoxPro ODBC 드라이버는 해당 개체에 대 한 소유자를 지원 하지 않습니다.  
  
 SQL_OWNER_USAGE는 0을 반환 합니다. Visual FoxPro ODBC 드라이버는 해당 개체에 대 한 소유자를 지원 하지 않습니다.  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS SQL_POS_POSITION를 반환 합니다.  
  
 SQL_POSITIONED_STATEMENTS는 0을 반환 합니다.  
  
 SQL_PROCEDURE_TERM ""를 반환 합니다.  
  
 SQL_PROCEDURES에서 ' N '을 반환 합니다.  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION SQL_QL_START를 반환 합니다.  
  
 SQL_QUALIFIER_NAME_SEPARATOR는 '! ' 또는 ' \\ '을 반환 합니다. 데이터베이스와 테이블 간의 구분 기호는 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)에 연결 된 데이터 원본의 경우 '! '이 고, \\ [사용 가능한 테이블](../../odbc/microsoft/visual-foxpro-terminology.md)의 디렉터리에 해당 하는 데이터 원본의 경우에는 ' '입니다.  
  
 SQL_QUALIFIER_TERM "database" 또는 "directory"를 반환 합니다. 한정자는 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)에 연결 된 데이터 원본의 경우 "database"이 고, [사용 가능한 테이블](../../odbc/microsoft/visual-foxpro-terminology.md)의 디렉터리인 데이터 원본의 경우 "directory"입니다.  
  
 SQL_QUALIFIER_USAGE에서 SQL_QU_PRIVILEGE_DEFINITION를 지원 하지 않습니다. SQL_QU_DML_STATEMENT 또는 SQL_QU_TABLE_DEFINITION을 반환 합니다.  
  
 SQL_QUOTED_IDENTIFIER_CASE SQL_IC_MIXED를 반환 합니다.  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES "N"을 반환 합니다. Visual FoxPro ODBC 드라이버는 정적 커서와 전방 커서만 지원 합니다.  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY SQL_SCCO_READ_ONLY를 반환 합니다.  
  
 SQL_SCROLL_OPTIONS SQL_SO_STATIC 또는 SQL_SO_READONLY 반환 합니다.  
  
 SQL_SEARCH_PATTERN_ESCAPE " \\ "를 반환 합니다.  
  
 SQL_SERVER_NAME ""를 반환 합니다.  
  
 SQL_SPECIAL_CHARACTERS "~ @ # $% ^"을 (를) 반환 합니다.  
  
 SQL_STATIC_SENSITIVITY는 0을 반환 합니다. Visual FoxPro ODBC 드라이버는 위치 업데이트를 지원 하지 않습니다.  
  
 SQL_STRING_FUNCTIONS는 SQL_FN_STR_INSERT, SQL_FN_STR_LOCATE, SQL_FN_STR_LOCATE_2 또는 SQL_FN_STR_SOUNDEX를 지원 하지 않습니다.  
  
 그러면 다음을 반환합니다.  
  
-   SQL_FN_STR_ASCII  
  
-   SQL_FN_STR_CHAR  
  
-   SQL_FN_STR_CONCAT  
  
-   SQL_FN_STR_DIFFERENCE  
  
-   SQL_FN_STR_LCASE  
  
-   SQL_FN_STR_LEFT  
  
-   SQL_FN_STR_LENGTH  
  
-   SQL_FN_STR_LTRIM  
  
-   SQL_FN_STR_REPEAT  
  
-   SQL_FN_STR_REPLACE  
  
-   SQL_FN_STR_RIGHT  
  
-   SQL_FN_STR_RTRIM  
  
-   SQL_FN_STR_SUBSTRING  
  
-   SQL_FN_STR_UCASE  
  
-   SQL_FN_STR_SPACE.  
  
 SQL_SUBQUERIES 반환:  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED.  
  
 SQL_SYSTEM_FUNCTIONS 반환:  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNULL  
  
 그렇지 않음:  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM "TABLE"을 반환 합니다.  
  
 SQL_TIMEDATE_ADD_INTERVALS 반환:  
  
-   SQL_FN_TSI_ 초  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 그렇지 않음:  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS 반환:  
  
-   SQL_FN_TSI_ 초  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS는 SQL_FN_TD_QUARTER, SQL_FN_TD_TIMESTAMPADD, SQL_FN_TD_DAYOFYEAR 또는 SQL_FN_TD_WEEK를 지원 하지 않습니다.  
  
 그러면 다음을 반환합니다.  
  
-   SQL_FN_TD_CURDATE  
  
-   SQL_FN_TD_CURTIME  
  
-   SQL_FN_TD_DAYNAME  
  
-   SQL_FN_TD_DAYOFMONTH  
  
-   SQL_FN_TD_DAYOFWEEK  
  
-   SQL_FN_TD_HOUR  
  
-   SQL_FN_TD_MINUTE  
  
-   SQL_FN_TD_MONTH  
  
-   SQL_FN_TD_MONTHNAME  
  
-   SQL_FN_TD_NOW  
  
-   SQL_FN_TD_SECOND  
  
-   SQL_FN_TD_TIMESTAMPDIFF  
  
-   SQL_FN_TD_YEAR.  
  
 SQL_TXN_CAPABLE SQL_TC_DML를 반환 합니다.  
  
 SQL_TXN_ISOLATION_OPTION SQL_TXN_READ_COMMITTED를 반환 합니다.  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION SQL_U_UNION 또는 SQL_U_UNION_ALL 반환 합니다.  
  
 SQL_USER_NAME 반환 \<blank> 됩니다.
