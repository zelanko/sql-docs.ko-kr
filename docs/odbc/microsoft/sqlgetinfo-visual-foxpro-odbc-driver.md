---
title: SQLGetInfo (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.openlocfilehash: 2d4b976083b46bf632c4890c7fce3b0f13a9a761
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295193"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 레벨 1  
  
 연결 핸들, *hdbc와*관련된 비주얼 FoxPro ODBC 드라이버 및 데이터 소스에 대한 일반 정보를 반환합니다. 다음 목록은 각 *fInfoType* 인수에 대해 Visual FoxPro ODBC 드라이버에서 반환된 값과 반환된 값에 대한 주석을 보여 주십습니다.  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLGetInfo를](../../odbc/reference/syntax/sqlgetinfo-function.md) 참조하십시오.  
  
## <a name="a"></a>A  
 SQL_ACCESSIBLE_PROCEDURES 'N'을 반환합니다.  
  
 SQL_ACCESSIBLE_TABLES 'Y'를 반환합니다.  
  
 SQL_ACTIVE_CONNECTIONS 0을 반환합니다.  
  
 SQL_ACTIVE_STATEMENTS 0을 반환합니다.  
  
 SQL_ALTER_TABLE SQL_AT_ADD_COLUMN 또는 SQL_AT_DROP_COLUMN 반환합니다.  
  
## <a name="b"></a>b  
 SQL_BOOKMARK_PERSISTENCE SQL_BP_SCROLL 반환합니다.  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS 'Y'를 반환합니다.  
  
 SQL_CONCAT_NULL_BEHAVIOR SQL_CB_NULL 반환합니다.  
  
 SQL_CONVERT_BIGINT 0을 반환합니다. 비주얼 폭스프로 ODBC 드라이버는 *BigInt를*지원하지 않습니다.  
  
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
  
 SQL_CORRELATION_NAME SQL_CN_ANY 반환합니다.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR SQL_CB_PRESERVE 반환합니다.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR SQL_CB_PRESERVE 반환합니다.  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME DSN으로 전달된 값을 [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)또는 [SQLDriverConnect에](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)반환합니다. DSN이 지정되지 않은 경우 빈 문자열을 반환합니다.  
  
 SQL_DATA_SOURCE_READ_ONLY 'N'을 반환합니다.  
  
 SQL_DATABASE_NAME 데이터 원본이 데이터베이스인 경우 현재 데이터베이스에 전체 UNC 경로를 [반환합니다.](../../odbc/microsoft/visual-foxpro-terminology.md) 데이터 원본이 [테이블](../../odbc/microsoft/visual-foxpro-terminology.md)디렉터리에 연결되면 함수는 디렉터리로 경로를 반환합니다.  
  
 SQL_DBMS_NAME "비주얼 폭스프로"를 반환합니다.  
  
 SQL_DBMS_VER "03.00.0000"을 반환합니다.  
  
 SQL_DEFAULT_TXN_ISOLATION SQL_TXN_READ_COMMITTED 반환합니다. 더티 읽기는 불가능하지만 반복할 수 없는 읽기 및 팬텀은 가능합니다.  
  
 SQL_DRIVER_HDBC 드라이버 관리자에 의해 구현됩니다.  
  
 SQL_DRIVER_HENV 드라이버 관리자에 의해 구현 됩니다.  
  
 SQL_DRIVER_HLIB 드라이버 관리자에 의해 구현됩니다.  
  
 SQL_DRIVER_HSTMT 드라이버 관리자에 의해 구현됩니다.  
  
 SQL_DRIVER_NAME "vfpodbc.dll"을 반환합니다.  
  
 SQL_DRIVER_ODBC_VER "02.50"(SQL_SPEC_MAJOR, SQL_SPEC_MINOR)을 반환합니다.  
  
 SQL_DRIVER_VER "01.00.0000"을 반환합니다.  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY 'N'을 반환합니다.  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION 반환합니다.  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK.  
  
 SQL_FILE_USAGE 데이터베이스(.dbc 파일)와 무료 테이블(.dbf 파일) 데이터 원본에 대해 모두 SQL_FILE_QUALIFIER 반환합니다.  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS 반환:  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY SQL_GB_NO_RELATION 반환합니다.  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE SQL_IC_MIXED 반환합니다.  
  
 SQL_IDENTIFIER_QUOTE_CHAR 돌아온다.'  
  
## <a name="k"></a>K  
 SQL_KEYWORDS ""를 반환합니다.  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE 'N'을 반환합니다.  
  
 SQL_LOCK_TYPES SQL_LCK_NO_CHANGE 반환합니다.  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN 0을 반환합니다.  
  
 SQL_MAX_CHAR_LITERAL_LEN 254를 반환합니다.  
  
 SQL_MAX_COLUMN_NAME_LEN 128을 반환합니다.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY 16을 반환합니다.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY 16을 반환합니다.  
  
 SQL_MAX_COLUMNS_IN_INDEX 0을 반환합니다.  
  
 SQL_MAX_COLUMNS_IN_SELECT 254를 반환합니다.  
  
 SQL_MAX_COLUMNS_IN_TABLE 254를 반환합니다.  
  
 SQL_MAX_CURSOR_NAME_LEN 254를 반환합니다.  
  
 SQL_MAX_INDEX_SIZE 0을 반환합니다.  
  
 SQL_MAX_OWNER_NAME_LEN 0을 반환합니다.  
  
 SQL_MAX_PROCEDURE_NAME_LEN 0을 반환합니다. Visual FoxPro ODBC 드라이버는 Visual FoxPro 저장 프로 저장 프로에 직접 액세스할 수 없습니다.  
  
 SQL_MAX_QUALIFIER_NAME_LEN 최대 운영 체제 경로 길이를 반환합니다.  
  
 SQL_MAX_ROW_SIZE 254^2를 반환합니다.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG 'N'을 반환합니다.  
  
 SQL_MAX_STATEMENT_LEN 8192를 반환합니다.  
  
 SQL_MAX_TABLE_NAME_LEN 128을 반환합니다.  
  
 SQL_MAX_TABLES_IN_SELECT 16을 반환합니다.  
  
 SQL_MAX_USER_NAME_LEN 0을 반환합니다.  
  
 SQL_MULT_RESULT_SETS 'Y'를 반환합니다.  
  
 SQL_MULTIPLE_ACTIVE_TXN 'Y'를 반환합니다. 여러 연결이 한 번에 여러 트랜잭션을 열 수 있습니다.  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN 'N'을 반환합니다.  
  
 SQL_NON_NULLABLE_COLUMNS SQL_NNC_NON_NULL 반환합니다.  
  
 SQL_NULL_COLLATION SQL_NC_LOW 반환합니다.  
  
 SQL_NUMERIC_FUNCTIONS Visual FoxPro ODBC 드라이버에서 지원되지 않는 SQL_FN_NUM_POWER 제외한 모든 함수를 반환합니다. 다음 기능이 지원됩니다.  
  
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
 SQL_ODBC_API_CONFORMANCE SQL_OAC_LEVEL1 반환합니다.  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE SQL_OSCC_COMPLIANT 반환합니다.  
  
 SQL_ODBC_SQL_CONFORMANCE SQL_OSC_MINIMUM 반환합니다. 최소 SQL 구문이 지원됩니다.  
  
 SQL_ODBC_SQL_OPT_IEF "N"을 반환합니다.  
  
 SQL_ODBC_VER 드라이버 관리자에 의해 구현 됩니다.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT "N"을 반환합니다.  
  
 SQL_OUTER_JOINS "N"을 반환합니다.  
  
 SQL_OWNER_TERM ""를 반환합니다. Visual FoxPro ODBC 드라이버는 해당 개체에 대한 소유자를 지원하지 않습니다.  
  
 SQL_OWNER_USAGE 0을 반환합니다. Visual FoxPro ODBC 드라이버는 해당 개체에 대한 소유자를 지원하지 않습니다.  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS SQL_POS_POSITION 반환합니다.  
  
 SQL_POSITIONED_STATEMENTS 0을 반환합니다.  
  
 SQL_PROCEDURE_TERM ""를 반환합니다.  
  
 SQL_PROCEDURES 'N'을 반환합니다.  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION SQL_QL_START 반환합니다.  
  
 SQL_QUALIFIER_NAME_SEPARATOR '!' 또는\\'를 반환합니다. 데이터베이스와 테이블 사이의 구분기호는 [데이터베이스에](../../odbc/microsoft/visual-foxpro-terminology.md)연결된 데이터 원본의 경우 '!'이고\\ [' 무료 테이블의](../../odbc/microsoft/visual-foxpro-terminology.md)디렉터리인 데이터 원본의 경우 '입니다.  
  
 SQL_QUALIFIER_TERM "데이터베이스" 또는 "디렉터리"를 반환합니다. 한정자는 [데이터베이스에](../../odbc/microsoft/visual-foxpro-terminology.md)연결된 데이터 원본에 대한 "데이터베이스"이고 [무료 테이블의](../../odbc/microsoft/visual-foxpro-terminology.md)디렉터리인 데이터 원본의 경우 "디렉터리"입니다.  
  
 SQL_QUALIFIER_USAGE SQL_QU_PRIVILEGE_DEFINITION 지원하지 않습니다. SQL_QU_DML_STATEMENT 또는 SQL_QU_TABLE_DEFINITION 반환합니다.  
  
 SQL_QUOTED_IDENTIFIER_CASE SQL_IC_MIXED 반환합니다.  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES "N"을 반환합니다. Visual FoxPro ODBC 드라이버는 정적 및 정방향 커서만 지원합니다.  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY SQL_SCCO_READ_ONLY 반환합니다.  
  
 SQL_SCROLL_OPTIONS SQL_SO_STATIC 또는 SQL_SO_READONLY 반환합니다.  
  
 SQL_SEARCH_PATTERN_ESCAPE 반환\\" ".  
  
 SQL_SERVER_NAME ""를 반환합니다.  
  
 SQL_SPECIAL_CHARACTERS "~@#$%^"를 반환합니다.  
  
 SQL_STATIC_SENSITIVITY 0을 반환합니다. 비주얼 FoxPro ODBC 드라이버는 위치 업데이트를 지원하지 않습니다.  
  
 SQL_STRING_FUNCTIONS SQL_FN_STR_INSERT, SQL_FN_STR_LOCATE, SQL_FN_STR_LOCATE_2 또는 SQL_FN_STR_SOUNDEX 지원하지 않습니다.  
  
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
  
 하지만 하지:  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM "테이블"을 반환합니다.  
  
 SQL_TIMEDATE_ADD_INTERVALS 반환:  
  
-   SQL_FN_TSI_ 두 번째  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 하지만 하지:  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS 반환:  
  
-   SQL_FN_TSI_ 두 번째  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS SQL_FN_TD_QUARTER, SQL_FN_TD_TIMESTAMPADD, SQL_FN_TD_DAYOFYEAR 또는 SQL_FN_TD_WEEK 지원하지 않습니다.  
  
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
  
-   SQL_FN_TD_YEAR .  
  
 SQL_TXN_CAPABLE SQL_TC_DML 반환합니다.  
  
 SQL_TXN_ISOLATION_OPTION SQL_TXN_READ_COMMITTED 반환합니다.  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION SQL_U_UNION 또는 SQL_U_UNION_ALL 반환합니다.  
  
 SQL_USER_NAME \<빈> 반환합니다.
