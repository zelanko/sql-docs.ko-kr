---
title: SQLGetInfo (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: fbc39e3d-67d9-4331-bf5f-76dbd74c4c45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b05ab71a12059535986cbd452e993e01178342fa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 수준 1 ODBC API 적용:  
  
 Visual FoxPro ODBC 드라이버 및 연결 핸들에 연결 된 데이터 원본에 대 한 일반 정보를 반환 *hdbc*합니다. 다음 목록은 각 Visual FoxPro ODBC 드라이버에서 반환 되는 값 *fInfoType* 인수 및 반환된 된 값에 대 한 의견 합니다.  
  
 자세한 내용은 참조 [SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md) 에 *ODBC Programmer's Reference*합니다.  
  
## <a name="a"></a>변수를 잠그기 위한  
 SQL_ACCESSIBLE_PROCEDURES 반환 ' N '입니다.  
  
 SQL_ACCESSIBLE_TABLES 'Y'를 반환합니다.  
  
 SQL_ACTIVE_CONNECTIONS 0을 반환합니다.  
  
 SQL_ACTIVE_STATEMENTS 0을 반환합니다.  
  
 SQL_ALTER_TABLE는 SQL_AT_ADD_COLUMN 또는 SQL_AT_DROP_COLUMN 중 하나를 반환합니다.  
  
## <a name="b"></a>B  
 SQL_BOOKMARK_PERSISTENCE SQL_BP_SCROLL를 반환합니다.  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS 'Y'를 반환합니다.  
  
 SQL_CONCAT_NULL_BEHAVIOR SQL_CB_NULL를 반환합니다.  
  
 SQL_CONVERT_BIGINT 0을 반환합니다. Visual FoxPro ODBC 드라이버가 지원 하지 않으면 *BigInt*합니다.  
  
 SQL_CONVERT_BINARY 0을 반환합니다.  
  
 SQL_CONVERT_BIT 0을 반환합니다.  
  
 SQL_CONVERT_CHAR 0을 반환합니다.  
  
 SQL_CONVERT_DATE 0을 반환합니다.  
  
 SQL_CONVERT_DECIMAL 0을 반환합니다.  
  
 SQL_CONVERT_DOUBLE 0을 반환합니다.  
  
 SQL_CONVERT_FLOAT 0을 반환합니다.  
  
 SQL_CONVERT_INTEGER 0을 반환합니다.  
  
 SQL_CONVERT_LONGVARBINARY 0을 반환합니다.  
  
 SQL_CONVERT_LONGVARCHAR 0을 반환합니다.  
  
 SQL_CONVERT_NUMERIC 0을 반환합니다.  
  
 SQL_CONVERT_REAL 0을 반환합니다.  
  
 SQL_CONVERT_SMALLINT 0을 반환합니다.  
  
 SQL_CONVERT_TIME 0을 반환합니다.  
  
 SQL_CONVERT_TIMESTAMP 0을 반환합니다.  
  
 SQL_CONVERT_TINYINT 0을 반환합니다.  
  
 SQL_CONVERT_VARBINARY 0을 반환합니다.  
  
 SQL_CONVERT_VARCHAR 0을 반환합니다.  
  
 SQL_CONVERT_FUNCTIONS 0을 반환합니다.  
  
 SQL_CORRELATION_NAME SQL_CN_ANY를 반환합니다.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR SQL_CB_PRESERVE를 반환합니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR SQL_CB_PRESERVE를 반환합니다.  
  
## <a name="d"></a>D  
 DSN을 변수로 전달 된 값을 반환 하는 SQL_DATA_SOURCE_NAME [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md), 또는 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md); 없는 DSN이 지정 된 경우 빈 문자열을 반환 합니다.  
  
 SQL_DATA_SOURCE_READ_ONLY 반환 ' N '입니다.  
  
 데이터 원본이 경우 현재 데이터베이스에 전체 UNC 경로 SQL_DATABASE_NAME 반환는 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)합니다. 데이터의 디렉터리에 연결 하는 경우 [테이블](../../odbc/microsoft/visual-foxpro-terminology.md), 함수는 디렉터리에 경로 반환 합니다.  
  
 SQL_DBMS_NAME "Visual FoxPro"를 반환합니다.  
  
 SQL_DBMS_VER "03.00.0000"를 반환합니다.  
  
 SQL_DEFAULT_TXN_ISOLATION SQL_TXN_READ_COMMITTED를 반환합니다. 더티 읽기 가능 하지만 읽기가 및 팬텀 있을 수도 있습니다.  
  
 SQL_DRIVER_HDBC는 드라이버 관리자에서 구현 됩니다.  
  
 SQL_DRIVER_HENV는 드라이버 관리자에서 구현 됩니다.  
  
 SQL_DRIVER_HLIB은 드라이버 관리자에서 구현 됩니다.  
  
 SQL_DRIVER_HSTMT은 드라이버 관리자에서 구현 됩니다.  
  
 SQL_DRIVER_NAME "vfpodbc.dll"를 반환합니다.  
  
 SQL_DRIVER_ODBC_VER "02.50" (SQL_SPEC_MAJOR, SQL_SPEC_MINOR)를 반환합니다.  
  
 SQL_DRIVER_VER "01.00.0000"를 반환합니다.  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY 반환 ' N '입니다.  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION를 반환합니다.  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK 합니다.  
  
 SQL_FILE_USAGE는 데이터베이스 (.dbc 파일)에 대 한 SQL_FILE_QUALIFIER 모두를 반환 하 고 무료로 (.dbf 파일) 데이터 원본 테이블입니다.  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS를 반환합니다.  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY SQL_GB_NO_RELATION를 반환합니다.  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE는 sql_ic_mixed 입니다를 반환합니다.  
  
 SQL_IDENTIFIER_QUOTE_CHAR 반환 '.  
  
## <a name="k"></a>K  
 SQL_KEYWORDS 반환 ""입니다.  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE 반환 ' N '입니다.  
  
 SQL_LOCK_TYPES SQL_LCK_NO_CHANGE를 반환합니다.  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN 0을 반환합니다.  
  
 SQL_MAX_CHAR_LITERAL_LEN 254를 반환합니다.  
  
 SQL_MAX_COLUMN_NAME_LEN 128을 반환합니다.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY 16을 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY 16을 반환 합니다.  
  
 SQL_MAX_COLUMNS_IN_INDEX 0을 반환합니다.  
  
 SQL_MAX_COLUMNS_IN_SELECT 254를 반환합니다.  
  
 SQL_MAX_COLUMNS_IN_TABLE 254를 반환합니다.  
  
 SQL_MAX_CURSOR_NAME_LEN 254를 반환합니다.  
  
 SQL_MAX_INDEX_SIZE 0을 반환합니다.  
  
 SQL_MAX_OWNER_NAME_LEN 0을 반환합니다.  
  
 SQL_MAX_PROCEDURE_NAME_LEN 0을 반환합니다. Visual FoxPro ODBC 드라이버 Visual FoxPro 저장 프로시저에 대 한 직접 액세스를 허용 하지 않습니다.  
  
 SQL_MAX_QUALIFIER_NAME_LEN 최대 운영 체제 경로 길이 반환합니다.  
  
 SQL_MAX_ROW_SIZE 반환 254 ^2입니다.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG 반환 ' N '입니다.  
  
 SQL_MAX_STATEMENT_LEN 8192를 반환합니다.  
  
 SQL_MAX_TABLE_NAME_LEN 128을 반환합니다.  
  
 SQL_MAX_TABLES_IN_SELECT 16을 반환 합니다.  
  
 SQL_MAX_USER_NAME_LEN 0을 반환합니다.  
  
 SQL_MULT_RESULT_SETS 'Y'를 반환합니다.  
  
 SQL_MULTIPLE_ACTIVE_TXN 'Y'를 반환합니다. 여러 연결이 여러 트랜잭션을 한 번에 열을 가질 수 있습니다.  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN 반환 ' N '입니다.  
  
 SQL_NON_NULLABLE_COLUMNS SQL_NNC_NON_NULL를 반환합니다.  
  
 SQL_NULL_COLLATION SQL_NC_LOW를 반환합니다.  
  
 SQL_NUMERIC_FUNCTIONS Visual FoxPro ODBC 드라이버에서 지원 되지 않는 SQL_FN_NUM_POWER 제외한 모든 함수를 반환 합니다. 다음 기능을 지원 합니다.  
  
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
 SQL_ODBC_API_CONFORMANCE SQL_OAC_LEVEL1를 반환합니다.  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE SQL_OSCC_COMPLIANT를 반환합니다.  
  
 SQL_ODBC_SQL_CONFORMANCE는 sql_osc_minimum이 합니다를 반환합니다. 최소 SQL 구문이 지원 됩니다.  
  
 SQL_ODBC_SQL_OPT_IEF "N"를 반환 합니다.  
  
 SQL_ODBC_VER는 드라이버 관리자에서 구현 됩니다.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT "N"를 반환 합니다.  
  
 SQL_OUTER_JOINS "N"를 반환 합니다.  
  
 SQL_OWNER_TERM 반환 ""입니다. Visual FoxPro ODBC 드라이버는 해당 개체에 대 한 소유자를 지원 하지 않습니다.  
  
 SQL_OWNER_USAGE 0을 반환합니다. Visual FoxPro ODBC 드라이버는 해당 개체에 대 한 소유자를 지원 하지 않습니다.  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS SQL_POS_POSITION를 반환합니다.  
  
 SQL_POSITIONED_STATEMENTS 0을 반환합니다.  
  
 SQL_PROCEDURE_TERM 반환 ""입니다.  
  
 SQL_PROCEDURES 반환 ' N '입니다.  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION SQL_QL_START를 반환합니다.  
  
 SQL_QUALIFIER_NAME_SEPARATOR 반환 '!' 또는 '\\'. 데이터베이스와 테이블 사이의 구분 기호는 '!'에 연결 된 데이터 원본에 대 한 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md), 및 '\\'의 디렉터리에 있는 데이터 원본에 대 한 [테이블 있음](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.  
  
 SQL_QUALIFIER_TERM "데이터베이스" 또는 "directory"를 반환합니다. 한정자 "데이터베이스"에 연결 된 데이터 원본에 대 한가 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md), 및의 디렉터리에 있는 데이터 원본에 대 한 "디렉터리" [테이블 있음](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.  
  
 SQL_QUALIFIER_USAGE SQL_QU_PRIVILEGE_DEFINITION;를 지원 하지 않습니다. SQL_QU_DML_STATEMENT 또는 SQL_QU_TABLE_DEFINITION 중 하나를 반환합니다.  
  
 SQL_QUOTED_IDENTIFIER_CASE는 sql_ic_mixed 입니다를 반환합니다.  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES "N"를 반환 합니다. Visual FoxPro ODBC 드라이버는만 정적 및 앞으로 커서를 지원합니다.  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY SQL_SCCO_READ_ONLY를 반환합니다.  
  
 SQL_SCROLL_OPTIONS는 SQL_SO_STATIC 또는 SQL_SO_READONLY 중 하나를 반환합니다.  
  
 SQL_SEARCH_PATTERN_ESCAPE 반환 "\\"입니다.  
  
 SQL_SERVER_NAME 반환 ""입니다.  
  
 SQL_SPECIAL_CHARACTERS 반환 "~ @# $% ^"입니다.  
  
 SQL_STATIC_SENSITIVITY 0을 반환합니다. Visual FoxPro ODBC 드라이버는 위치 업데이트를 지원 하지 않습니다.  
  
 SQL_FN_STR_INSERT, SQL_FN_STR_LOCATE, SQL_FN_STR_LOCATE_2, 또는 SQL_FN_STR_SOUNDEX SQL_STRING_FUNCTIONS 지원 하지 않습니다.  
  
 반환합니다.  
  
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
  
-   SQL_FN_STR_SPACE 합니다.  
  
 SQL_SUBQUERIES를 반환합니다.  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED 합니다.  
  
 SQL_SYSTEM_FUNCTIONS를 반환합니다.  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNULL  
  
 하지만 없습니다.  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM "table"를 반환합니다.  
  
 SQL_TIMEDATE_ADD_INTERVALS를 반환합니다.  
  
-   SQL_FN_TSI_ 초  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 하지만 없습니다.  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS를 반환합니다.  
  
-   SQL_FN_TSI_ 초  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_FN_TD_QUARTER, SQL_FN_TD_TIMESTAMPADD, SQL_FN_TD_DAYOFYEAR, 또는 SQL_FN_TD_WEEK SQL_TIMEDATE_FUNCTIONS 지원 하지 않습니다.  
  
 반환합니다.  
  
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
  
-   SQL_FN_TD_YEAR 합니다.  
  
 SQL_TXN_CAPABLE SQL_TC_DML를 반환합니다.  
  
 SQL_TXN_ISOLATION_OPTION SQL_TXN_READ_COMMITTED를 반환합니다.  
  
## <a name="u-z"></a>U + Z  
 SQL_UNION은 SQL_U_UNION 또는 SQL_U_UNION_ALL 중 하나를 반환합니다.  
  
 SQL_USER_NAME 반환 \<빈 > 합니다.
