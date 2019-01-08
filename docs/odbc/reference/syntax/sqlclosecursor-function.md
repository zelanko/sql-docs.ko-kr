---
title: SQLCloseCursor 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCloseCursor
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCloseCursor
helpviewer_keywords:
- SQLCloseCursor function [ODBC]
ms.assetid: 05b0a054-e28d-4e16-b5b0-07418486b372
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 912e4d109a9e769442c65d292ff190d79705eb21
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201542"
---
# <a name="sqlclosecursor-function"></a>SQLCloseCursor 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLCloseCursor** 문에서 열린 및 보류 중인 결과가 삭제 하는 커서를 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLCloseCursor(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLCloseCursor** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* sql _HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLCloseCursor** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|24000|잘못된 커서 상태|커서가 없습니다에서 열리는 합니다 *StatementHandle*합니다. (이 메서드는 ODBC 3에서만 반환 됩니다. *x* 드라이버입니다.)|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연결 된 연결 핸들에 대 한 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLCloseCursor** 커서가 없습니다 열려 있으면 SQLSTATE 24000 (잘못 된 커서 상태)를 반환 합니다. 호출 **SQLCloseCursor** 호출 하는 것과 같습니다 **SQLFreeStmt** 예외를 사용 하 여 SQL_CLOSE 옵션을 사용 하는 **SQLFreeStmt** SQL_CLOSE를 사용 하 여에 영향을 주지 않습니다 합니다 응용 프로그램 없음 커서 문에서 열려 있으면 while **SQLCloseCursor** SQLSTATE 24000 (잘못 된 커서 상태)를 반환 합니다.  
  
> [!NOTE]  
>  ODBC 3 경우입니다. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출 **SQLCloseCursor** 커서가 없습니다가 열려 있으면 SQLSTATE 24000 (잘못 된 커서 상태) 반환 되지 않으면 드라이버 관리자를 매핑하므로 **SQLCloseCursor** 를**SQLFreeStmt** SQL_CLOSE를 사용 하 여 합니다.  
  
 자세한 내용은 [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) 하 고 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|여러 결과 집합 처리|[SQLMoreResults 함수](../../../odbc/reference/syntax/sqlmoreresults-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
