---
title: ODBC 함수 요약 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], listed by task
ms.assetid: 7aa635da-e6b7-439f-8e9b-c3860e24de5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10cc7880cf941a1490f963e21e8b44bc91db215
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298924"
---
# <a name="odbc-function-summary"></a>ODBC 함수 요약
다음 표에는 ODBC 함수가 작업 유형별로 그룹화되어 나열되며 적합성 지정 및 각 함수의 목적에 대한 간략한 설명이 포함되어 있습니다. 적합성 지정에 대한 자세한 내용은 [ODBC 및 표준 CLI를](../../../odbc/reference/odbc-and-the-standard-cli.md)참조하십시오. 각 함수에 대한 구문 및 의미 체계에 대한 자세한 내용은 [ODBC API 참조를](../../../odbc/reference/syntax/odbc-api-reference.md)참조하십시오.  
  
 응용 프로그램은 **SQLGetInfo** 함수를 호출하여 드라이버에 대한 적합성 정보를 가져올 수 있습니다. 드라이버의 특정 함수에 대한 지원에 대한 정보를 얻기 위해 응용 프로그램은 **SQLGetFunctions**를 호출할 수 있습니다.  
  
|Task|함수 이름|규칙|용도|  
|----------|-------------------|-----------------|-------------|  
|데이터 원본에 연결|[SQLAlloc핸들](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|환경, 연결, 명령문 또는 설명자 핸들을 가져옵니다.|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|데이터 원본 이름, 사용자 ID 및 암호로 특정 드라이버에 연결합니다.|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|연결 문자열을 통해 특정 드라이버에 연결하거나 드라이버 관리자와 드라이버가 사용자에 대한 연결 대화 상자를 표시하도록 요청합니다.|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|연속적인 수준의 연결 특성과 유효한 특성 값을 반환합니다. 각 연결 특성에 대해 값을 지정하면 데이터 원본에 연결합니다.|  
|드라이버 및 데이터 원본에 대한 정보 얻기|[SQLDataSource](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBC|사용 가능한 데이터 원본 목록을 반환합니다.<br /><br /> 설치된 드라이버 및 해당 특성 목록을 반환합니다.|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|특정 드라이버 및 데이터 원본에 대한 정보를 반환합니다.|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|지원되는 드라이버 함수를 반환합니다.|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|지원되는 데이터 형식에 대한 정보를 반환합니다.|  
|드라이버 특성 설정 및 검색|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|연결 특성을 설정합니다.<br /><br /> 연결 특성의 값을 반환합니다.|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|환경 특성을 설정합니다.|  
||[SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|환경 특성의 값을 반환합니다.|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|문 특성을 설정합니다.|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|문 특성의 값을 반환합니다.|  
|설명자 필드 설정 및 검색|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|단일 설명자 필드의 값을 반환합니다.<br /><br /> 여러 설명자 필드의 값을 반환합니다.|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|단일 설명자 필드를 설정합니다.|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|여러 설명자 필드를 설정합니다.|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|한 설명자 핸들에서 다른 설명자 핸들로 설명자 정보를 복사합니다.|  
|SQL 요청 준비|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|나중에 실행을 위해 SQL 문을 준비합니다.|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|SQL 문에서 매개 변수에 대한 저장소를 할당합니다.|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|문 핸들과 연결된 커서 이름을 반환합니다.|  
||[SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|커서 이름을 지정합니다.|  
||[SQLSet스크롤 옵션](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|커서 동작을 제어하는 옵션을 설정합니다.|  
|요청 제출|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|준비된 문을 실행합니다.<br /><br /> 문을 실행합니다.|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|드라이버에서 번역한 SQL 문의 텍스트를 반환합니다.|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|명령문의 특정 매개 변수에 대한 설명을 반환합니다.|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|명령문의 매개 변수 수를 반환합니다.|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|**SQLPutData와** 함께 실행 시 매개 변수 데이터를 제공하는 데 사용됩니다. (긴 데이터 값에 유용합니다.)|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|매개 변수에 대한 데이터 값의 일부 또는 전부를 보냅니다. (긴 데이터 값에 유용합니다.)|  
|결과 및 결과에 대한 정보 검색|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|삽입, 업데이트 또는 삭제 요청의 영향을 받는 행 수를 반환합니다.<br /><br /> 결과 집합의 열 수를 반환합니다.|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|결과 집합의 열을 설명합니다.|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|결과 집합에서 열의 특성을 설명합니다.|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|결과 열에 대 한 저장소를 할당 하 고 데이터 형식을 지정 합니다.|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|여러 결과 행을 반환합니다.|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|스크롤 가능한 결과 행을 반환합니다.|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|결과 집합의 한 행의 한 열의 일부 또는 전부를 반환합니다. (긴 데이터 값에 유용합니다.)|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|커서를 가져온 데이터 블록 내에 배치하고 응용 프로그램이 행 집합에서 데이터를 새로 고치거나 결과 집합의 데이터를 업데이트하거나 삭제할 수 있습니다.|  
||[SQLBulk운영](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|책갈피별로 업데이트, 삭제 및 가져오기를 포함하여 대량 삽입 및 대량 북마크 작업을 수행합니다.|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|사용 가능한 결과 집합이 더 있는지 여부를 결정하고, 이 경우 다음 결과 집합에 대한 처리를 초기화합니다.|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|추가 진단 정보(진단 데이터 구조의 단일 필드)를 반환합니다.|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|추가 진단 정보(진단 데이터 구조의 여러 필드)를 반환합니다.|  
|데이터 원본의 시스템 테이블(카탈로그 함수)에 대한 정보 얻기|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> 그룹 열기|하나 이상의 테이블에 대한 열 및 관련 권한 목록을 반환합니다.<br /><br /> 지정된 테이블의 열 이름 목록을 반환합니다.|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|지정된 테이블에 대해 있는 경우 외래 키를 구성하는 열 이름 목록을 반환합니다.|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|테이블의 기본 키를 구성하는 열 이름 목록을 반환합니다.|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|지정된 프로시저에 대한 결과 집합을 구성하는 열뿐만 아니라 입력 및 출력 매개 변수 목록을 반환합니다.|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|특정 데이터 원본에 저장된 프로시저 이름 목록을 반환합니다.|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|그룹 열기|지정된 테이블에서 행을 고유하게 식별하는 최적 열 집합 또는 트랜잭션에 의해 행의 값이 업데이트될 때 자동으로 업데이트되는 열에 대한 정보를 반환합니다.|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|단일 테이블및테이블과연관된 인덱스 목록에 대한 통계를 반환합니다.|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|테이블 목록및 각 테이블과 연결된 권한 목록을 반환합니다.|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|그룹 열기|특정 데이터 원본에 저장된 테이블 이름 목록을 반환합니다.|  
|명령문 종료|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|문 처리를 종료하고 보류 중인 결과를 삭제하며, 선택적으로 명령문 핸들과 관련된 모든 리소스를 해제합니다.|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|문 핸들에서 열린 커서를 닫습니다.|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|명령문에서 처리를 취소합니다.|  
||[SQLCancel핸들](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|명령문 또는 연결에서 처리를 취소합니다.|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|트랜잭션을 커밋하거나 롤백합니다.|  
|연결 종료|[SQL분리](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|연결을 닫습니다.<br /><br /> 환경, 연결, 명령문 또는 설명자 핸들을 해제합니다.|
