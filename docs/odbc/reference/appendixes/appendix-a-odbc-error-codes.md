---
title: '부록 A: ODBC 오류 코드 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error codes [ODBC]
- SQLSTATE [ODBC]
- error codes [ODBC], SQLSTATE
ms.assetid: c06902e4-721d-42e2-b818-05f0e18e4ce0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af288cf9f0564f6fe0dbef14f66143667120c656
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307524"
---
# <a name="appendix-a-odbc-error-codes"></a>부록 A: ODBC 오류 코드
이 항목에서는 ODBC 3에 대한 SQLSTATE 값에 대해 설명합니다. *x*. ODBC 3에 대한 자세한 내용은 *x* SQLSTATE 값은 [SQLSTATE 매핑을](../../../odbc/reference/develop-app/sqlstate-mappings.md)참조하십시오.  
  
 **SQLGetDiagRec** 또는 **SQLGetDiagField는** 오픈 그룹 *데이터 관리: SQL(구조화 쿼리 언어), 버전* 2(1995년 3월)에 정의된 SQLSTATE 값을 반환합니다. SQLSTATE 값은 5개의 문자를 포함하는 문자열입니다. 다음 표에는 드라이버가 **SQLGetDiagRec**에 대해 반환할 수 있는 SQLSTATE 값이 나열되어 있습니다.  
  
 SQLSTATE에 대해 반환되는 문자 문자열 값은 두 문자 클래스 값 다음에 세 문자 하위 클래스 값으로 구성됩니다. 클래스 값 "01"은 경고를 나타내며 반환 코드(반환 코드)SQL_SUCCESS_WITH_INFO 함께 제공됩니다. "IM"을 제외한 "01"이 아닌 클래스 값은 오류를 나타내고 SQL_ERROR 반환 값을 함께 수반합니다. 클래스 "IM"은 ODBC 자체의 구현에서 파생되는 경고 및 오류와 관련이 있습니다. 모든 클래스의 하위 클래스 값 "000"은 해당 SQLSTATE에 대한 하위 클래스가 없음을 나타냅니다. 클래스 및 하위 클래스 값의 할당은 SQL-92에 의해 정의됩니다.  
  
> [!NOTE]  
>  함수의 성공적인 실행은 일반적으로 SQL_SUCCESS 반환 값으로 표시되지만 SQLSTATE 00000은 성공을 나타냅니다.  
  
|SQLSTATE|Error|에서 반환할 수 있습니다.|  
|--------------|-----------|--------------------------|  
|01000|일반 경고|다음을 제외한 모든 ODBC 함수:<br /><br /> **SQL오류**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|01001|커서 작업 충돌|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|01002|연결 오류|**SQL분리**|  
|01003|설정 함수에서 NULL 값 제거|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01004|문자열 데이터, 오른쪽 잘린|**SQLBrowseConnect**<br /><br /> **SQLBulk운영**<br /><br /> **SQLColAttribute**<br /><br /> **SQLDataSource**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLDrivers**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQL네이티브**<br /><br /> **Sql SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetCursorName**|  
|01006|권한 취소되지 않음|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01007|권한이 부여되지 않음|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01S00|잘못된 연결 문자열 특성|**SQLBrowseConnect**<br /><br /> **SQL드라이버코네크**|  
|01S01|행의 오류|**SQLBulk운영**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLSetPos**|  
|01S02|옵션 값이 변경되었습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**|  
|01S06|결과 집합이 첫 번째 행 집합을 반환하기 전에 가져오기를 시도합니다.|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|01S07|분수 잘림|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|01S08|오류 저장 파일 DSN|**SQLDriverConnect**|  
|01S09|잘못된 키워드|**SQLDriverConnect**|  
|07001|잘못된 수의 매개 변수|**SQLExecDirect**<br /><br /> **SQLExecute**|  
|07002|카운트 필드가 올바르지 않습니다.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|07005|*커서 사양이* 아닌 준비된 문|**SQLColAttribute**<br /><br /> **SQLDescribeCol**|  
|07006|제한된 데이터 형식 특성 위반|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|07009|잘못된 설명자 인덱스|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulk운영**<br /><br /> **SQLColAttribute**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLParamData**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRecSQLSetPos**|  
|07S01|기본 매개 변수의 잘못된 사용|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**|  
|08001|연결을 설정할 수 없는 클라이언트|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|08002|사용 중 연결 이름|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLSetConnectAttr**|  
|08003|연결이 열려 있지 않음|**SQLAlloc핸들**<br /><br /> **SQL분리**<br /><br /> **SQLEndTran**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLNativeSql**<br /><br /> **SQLSetConnectAttr**|  
|08004|서버가 연결을 거부했습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|08007|트랜잭션 중 연결 오류|**SQLEndTran**|  
|08S01|통신 링크 오류|**SQLBrowseConnect**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNativeSql**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|21S01|삽입 값 목록이 열 목록과 일치하지 않음|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|21S02|파생 테이블의 정도가 열 목록과 일치하지 않음|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetPos**|  
|22001|문자열 데이터, 오른쪽 잘린|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetPos**|  
|22002|표시기 변수가 필요하지만 제공되지 않음|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**|  
|22003|범위를 벗어난 숫자 값|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLGetInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22007|잘못된 날짜 시간 형식|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22008|일시 필드 오버플로|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **QLParam데이터**<br /><br /> **SQLPutData**|  
|22012|0으로 나누기|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLPutData**|  
|22015|간격 필드 오버플로|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22018|캐스트 사양에 대해 잘못된 문자 값|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22019|유효하지 않은 이스케이프 문자|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|22025|잘못된 이스케이프 시퀀스|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|22026|문자열 데이터, 길이가 일치하지 않음|**SQLParamData**|  
|23000|무결성 제약 조건 위반|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|24000|잘못된 커서 상태|**SQLBulk운영**<br /><br /> **SQLCloseCursor**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetData**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLNativeSql**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|25000|잘못된 트랜잭션 상태|**SQL분리**|  
|25S01|트랜잭션 상태|**SQLEndTran**|  
|25S02|트랜잭션이 여전히 활성 상태|**SQLEndTran**|  
|25S03|트랜잭션이 롤백됩니다.|**SQLEndTran**|  
|28000|잘못된 권한 부여 사양|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|34000|잘못된 커서 이름|**SQLExecDirect**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetCursorName**|  
|3C000|중복 커서 이름|**SQLSetCursorName**|  
|3D000|카탈로그 이름이 잘못되었습니다.|**SQLExecDirect**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetConnectAttr**|  
|3F000|잘못된 스키마 이름|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|40001|직렬화 실패|**SQLBulk운영**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLParamData**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|40002|무결성 제약 조건 위반|**SQLEndTran**|  
|40003|명령문 완료를 알 수 없음|**SQLBulk운영**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|42000|구문 오류 또는 액세스 위반|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetPos**|  
|42S01|기본 테이블 또는 뷰가 이미 있습니다.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S02|기본 테이블 또는 뷰를 찾을 수 없습니다.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S11|인덱스가 이미 있습니다.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S12|인덱스를 찾을 수 없습니다.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S21|열이 이미 있습니다.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S22|열을 찾을 수 없습니다.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|44000|WITH CHECK OPTION 위반|**SQLBulk운영**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|HY000|일반 오류|다음을 제외한 모든 ODBC 함수:<br /><br /> **SQL오류**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY01|메모리 할당 오류|다음을 제외한 모든 ODBC 함수:<br /><br /> **SQL오류**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY003|잘못된 응용 프로그램 버퍼 유형|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLGetData**|  
|HY004|잘못된 SQL 데이터 형식|**SQLBindParameter**<br /><br /> **SQLGetTypeInfo**|  
|HY007|관련 문이 준비되지 않았습니다.|**SQLCopyDesc**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**|  
|HY08|작업 취소됨|비동기적으로 처리할 수 있는 모든 ODBC 함수:<br /><br /> **SQLBrowseConnect**<br /><br /> **SQLBulk운영**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQL분리**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetData**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY09|null 포인터의 잘못된 사용|**SQLAlloc핸들**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulk운영**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLNativeSql**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY010|함수 시퀀스 오류|**SQLAlloc핸들**<br /><br /> **SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulk운영**<br /><br /> **SQLCloseCursor**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQL분리**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLRowCount**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY011|특성을 지금 설정할 수 없습니다.|**SQLBulk운영**<br /><br /> **SQLParamData**<br /><br /> **QLSetPos**<br /><br /> **SQLSetStmtAttr**|  
|HY012|잘못된 트랜잭션 작업 코드|**SQLEndTran**|  
|HY013|메모리 관리 오류|다음을 제외한 모든 ODBC 함수:<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY014|초과된 핸들 수 제한|**SQLAlloc핸들**|  
|HY015|사용할 수 있는 커서 이름이 없습니다.|**SQLGetCursorName**|  
|HY016|구현 행 설명자 수정할 수 없습니다.|**SQLCopyDesc**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**|  
|HY017|자동으로 할당된 설명자 핸들의 잘못된 사용|**SQLFreeHandle**<br /><br /> **SQLSetStmtAttr**|  
|HY018|서버 취소 요청 거부|**SQLCancel**|  
|HY019|조각으로 전송되는 비문자 및 비이진 데이터|**SQLPutData**|  
|HY020|null 값을 연결하려고 시도|**SQLPutData**|  
|HY021|일관되지 않은 설명자 정보|**SQLBindParameter**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLGetDescField**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**|  
|HY024|잘못된 특성 값|**SQLSetConnectAttr**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBrowseConnect**<br /><br /> **SQLBulk운영**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDataSource**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLDrivers**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNativeSql**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY091|잘못된 설명자 필드 식별자|**SQLColAttribute**<br /><br /> **SQLGetDescField**<br /><br /> **SQLSetDescField**|  
|HY092|잘못된 특성/옵션 식별자|**SQLAlloc핸들**<br /><br /> **QLBulk운영**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetEnvAttr**<br /><br /> **QLParam데이터**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**|  
|HY095|범위를 벗어난 함수 유형|**SQLGetFunctions**|  
|HY096|잘못된 정보 유형|**SQLGetInfo**|  
|HY097|범위를 벗어난 열 유형|**SQLSpecialColumns**|  
|HY098|범위를 벗어난 범위 유형|**SQLSpecialColumns**|  
|HY099|범위를 벗어난 Null 형식|**SQLSpecialColumns**|  
|HY100|범위를 벗어난 고유성 옵션 유형|**SQLStatistics**|  
|HY101|범위를 벗어난 정확도 옵션 유형|**SQLStatistics**|  
|HY103|잘못된 검색 코드|**SQLDataSource**<br /><br /> **SQLDrivers**|  
|HY104|잘못된 정밀도 또는 축척 값|**SQLBindParameter**|  
|HY105|잘못된 매개 변수 유형|**SQLBindParameter**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetDescField**|  
|HY106|범위를 벗어난 형식 가져오기|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|HY107|범위를 벗어난 행 값|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLSetPos**|  
|HY109|잘못된 커서 위치|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLGetData**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNativeSql**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|HY110|드라이버가 잘못 완료되었습니다.|**SQLDriverConnect**|  
|HY11|책갈피 값이 잘못되었습니다.|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|하이크00|구현되지 않은 선택적 기능|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulk운영**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetData**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HYT00|제한 시간이 만료되었습니다.|**SQLBrowseConnect**<br /><br /> **SQLBulk운영**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HYT01|연결 시간 시간이 만료되었습니다.|다음을 제외한 모든 ODBC 함수:<br /><br /> **SQLDrivers**<br /><br /> **SQLDataSource**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLSetEnvAttr**|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|다음을 제외한 모든 ODBC 함수:<br /><br /> **SQLAlloc핸들**<br /><br /> **SQLDataSource**<br /><br /> **SQLDrivers**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLGetFunctions**|  
|IM002|데이터 원본 이름을 찾을 수 없으며 기본 드라이버가 지정되지 않았습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM003|지정된 드라이버를 로드할 수 없습니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM004|SQL_HANDLE_ENV 대한 드라이버의 **SQLAllocHandle실패**|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM005|SQL_HANDLE_DBC 드라이버의 **SQLAllocHandle실패**|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM006|드라이버의 **SQLSetConnectAttr** 실패|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM007|데이터 원본또는 드라이버를 지정하지 않습니다. 대화 상자 금지|**SQLDriverConnect**|  
|IM008|대화 상자에 실패했습니다.|**SQLDriverConnect**|  
|IM009|번역 DLL을 로드할 수 없음|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLSetConnectAttr**|  
|IM010|데이터 원본 이름이 너무 깁니다.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM011|드라이버 이름이 너무 깁니다.|**SQLBrowseConnect**<br /><br /> **SQLDriverConnect**|  
|IM012|DRIVER 키워드 구문 오류|**SQLBrowseConnect**<br /><br /> **SQLDriverConnect**|  
|IM013|추적 파일 오류|모든 ODBC 함수.|  
|IM014|파일 DSN의 잘못된 이름|**SQLDriverConnect**|  
|IM015|손상된 파일 데이터 원본|**SQLDriverConnect**|
