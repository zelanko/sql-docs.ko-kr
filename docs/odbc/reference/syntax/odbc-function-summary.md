---
title: ODBC 함수 요약 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298924"
---
# <a name="odbc-function-summary"></a>ODBC 함수 요약
다음 표에서는 태스크 유형별로 그룹화 된 ODBC 함수를 나열 하 고 각 함수의 용도에 대 한 규칙 지정 및 간단한 설명을 포함 합니다. 규칙을 준수 하는 방법에 대 한 자세한 내용은 [ODBC 및 표준 CLI](../../../odbc/reference/odbc-and-the-standard-cli.md)를 참조 하세요. 각 함수의 구문 및 의미 체계에 대 한 자세한 내용은 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)를 참조 하세요.  
  
 응용 프로그램은 **SQLGetInfo** 함수를 호출 하 여 드라이버에 대 한 규칙 정보를 얻을 수 있습니다. 드라이버의 특정 기능에 대 한 지원 정보를 얻기 위해 응용 프로그램은 **SQLGetFunctions**를 호출할 수 있습니다.  
  
|작업|함수 이름|규칙|목적|  
|----------|-------------------|-----------------|-------------|  
|데이터 원본에 연결|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|환경, 연결, 문 또는 설명자 핸들을 가져옵니다.|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|데이터 원본 이름, 사용자 ID 및 암호를 사용 하 여 특정 드라이버에 연결 합니다.|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|연결 문자열을 사용 하 여 특정 드라이버에 연결 하거나 사용자에 대 한 드라이버 관리자 및 드라이버 표시 연결 대화 상자를 요청 합니다.|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|연속 된 수준으로 연결 특성 및 유효한 특성 값을 반환 합니다. 각 연결 특성에 대해 값이 지정 된 경우는 데이터 원본에 연결 합니다.|  
|드라이버 및 데이터 원본에 대 한 정보 가져오기|[SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBC|사용 가능한 데이터 원본 목록을 반환 합니다.<br /><br /> 설치 된 드라이버와 해당 특성의 목록을 반환 합니다.|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|특정 드라이버와 데이터 원본에 대 한 정보를 반환 합니다.|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|지원 되는 드라이버 함수를 반환 합니다.|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|지원 되는 데이터 형식에 대 한 정보를 반환 합니다.|  
|드라이버 특성 설정 및 검색|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|연결 특성을 설정 합니다.<br /><br /> 연결 특성의 값을 반환 합니다.|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|환경 특성을 설정 합니다.|  
||[SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|환경 특성의 값을 반환 합니다.|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|문 특성을 설정 합니다.|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|문 특성의 값을 반환 합니다.|  
|설명자 필드 설정 및 검색|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|단일 설명자 필드의 값을 반환 합니다.<br /><br /> 여러 설명자 필드의 값을 반환 합니다.|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|단일 설명자 필드를 설정 합니다.|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|여러 설명자 필드를 설정 합니다.|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|한 설명자 핸들에서 다른 설명자 핸들로 설명자 정보를 복사 합니다.|  
|SQL 요청 준비|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|나중에 실행할 SQL 문을 준비 합니다.|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|SQL 문의 매개 변수에 대 한 저장소를 할당 합니다.|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|문 핸들과 연결 된 커서 이름을 반환 합니다.|  
||[SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|커서 이름을 지정 합니다.|  
||[SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|커서 동작을 제어 하는 옵션을 설정 합니다.|  
|요청 제출|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|준비된 문을 실행합니다.<br /><br /> 문을 실행합니다.|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|드라이버가 변환 된 SQL 문의 텍스트를 반환 합니다.|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|문의 특정 매개 변수에 대 한 설명을 반환 합니다.|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|문의 매개 변수 개수를 반환 합니다.|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|실행 시 매개 변수 데이터를 제공 하기 위해 **Sqlputdata** 와 함께 사용 됩니다. Long 데이터 값에 유용 합니다.|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|매개 변수에 대 한 데이터 값의 일부 또는 전체를 보냅니다. Long 데이터 값에 유용 합니다.|  
|결과 및 결과에 대 한 정보 검색|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|Insert, update 또는 delete 요청의 영향을 받는 행 수를 반환 합니다.<br /><br /> 결과 집합의 열 수를 반환합니다.|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|결과 집합의 열을 설명 합니다.|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|결과 집합에 있는 열의 특성을 설명 합니다.|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|결과 열에 대 한 저장소를 할당 하 고 데이터 형식을 지정 합니다.|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|여러 결과 행을 반환 합니다.|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|스크롤 가능한 결과 행을 반환 합니다.|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|결과 집합의 한 행에 있는 한 열의 일부 또는 전체를 반환 합니다. Long 데이터 값에 유용 합니다.|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|인출 된 데이터 블록 내에 커서를 놓고 응용 프로그램에서 행 집합의 데이터를 새로 고치거 나 결과 집합의 데이터를 업데이트 하거나 삭제할 수 있습니다.|  
||[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|업데이트, 삭제 및 페치를 포함 하 여 책갈피에 대 한 대량 삽입 및 대량 책갈피 작업을 수행 합니다.|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|사용할 수 있는 추가 결과 집합이 있는지 여부를 확인 하 고, 해당 하는 경우 다음 결과 집합에 대 한 처리를 초기화 합니다.|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|진단 데이터 구조의 단일 필드인 추가 진단 정보를 반환 합니다.|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|추가 진단 정보를 반환 합니다 (진단 데이터 구조의 여러 필드).|  
|데이터 원본의 시스템 테이블에 대 한 정보 가져오기 (카탈로그 함수)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> 그룹 열기|하나 이상의 테이블에 대 한 열 및 관련 된 권한 목록을 반환 합니다.<br /><br /> 지정 된 테이블의 열 이름 목록을 반환 합니다.|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|지정 된 테이블에 대해 외래 키가 있는 경우 해당 키를 구성 하는 열 이름의 목록을 반환 합니다.|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|테이블에 대 한 기본 키를 구성 하는 열 이름의 목록을 반환 합니다.|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|입력 및 출력 매개 변수의 목록과 지정 된 프로시저에 대 한 결과 집합을 구성 하는 열을 반환 합니다.|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|특정 데이터 원본에 저장 된 프로시저 이름의 목록을 반환 합니다.|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|그룹 열기|지정 된 테이블의 행을 고유 하 게 식별 하는 최적의 열 집합 또는 트랜잭션에 의해 행의 값이 업데이트 될 때 자동으로 업데이트 되는 열에 대 한 정보를 반환 합니다.|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|단일 테이블에 대 한 통계와 해당 테이블과 연결 된 인덱스 목록을 반환 합니다.|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|테이블 목록과 각 테이블과 연결 된 권한을 반환 합니다.|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|그룹 열기|특정 데이터 원본에 저장 된 테이블 이름의 목록을 반환 합니다.|  
|문 종료|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|문 처리를 종료 하 고, 보류 중인 결과를 삭제 하 고, 필요에 따라 문 핸들과 연결 된 모든 리소스를 해제 합니다.|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|문 핸들에서 열린 커서를 닫습니다.|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|문에서 처리를 취소 합니다.|  
||[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|문 또는 연결에 대 한 처리를 취소 합니다.|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|트랜잭션을 커밋하거나 롤백합니다.|  
|연결 종료|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|연결을 닫습니다.<br /><br /> 환경, 연결, 문 또는 설명자 핸들을 해제 합니다.|
