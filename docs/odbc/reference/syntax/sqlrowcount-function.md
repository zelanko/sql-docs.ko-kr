---
title: SQLRowCount Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ab7046e036a6f50f8009a481f92345d7ce12aea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62656071"
---
# <a name="sqlrowcount-function"></a>SQLRowCount 함수(SQLRowCount Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLRowCount** 영향을 받는 행 수를 반환 합니다는 **업데이트**합니다 **삽입**, 또는 **삭제** 문;는 SQL_ADD SQL_UPDATE_BY_BOOKMARK, 또는 SQL_ DELETE_BY_BOOKMARK 작업 **SQLBulkOperations**; 또는에서 SQL_UPDATE 또는 SQL_DELETE 연산 **SQLSetPos**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *RowCountPtr*  
 [출력] 행 개수를 반환 하는 버퍼를 가리킵니다. 에 대 한 **업데이트**를 **삽입**, 및 **삭제** 에 SQL_ADD, SQL_UPDATE_BY_BOOKMARK, 및 SQL_DELETE_BY_BOOKMARK 작업에 대 한의 문을  **SQLBulkOperations**, 및에서 SQL_UPDATE 또는 SQL_DELETE 작업에 대 한 **SQLSetPos**에서 반환 된 값 **RowCountPtr* 영향을 받는 행 수를 요청 또는 영향을 받는 행 수를 사용할 수 없는 경우-1입니다.  
  
 때 **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**하십시오 **SQLSetPos 또는 SQLMoreResults** 호출 되는 SQL_DIAG_ROW_COUNT 진단 데이터 구조의 필드를 행 수로 설정 하 고 행 개수는 구현에 따라 다릅니다 방식으로 캐시 됩니다. **SQLRowCount** 캐시 된 행 개수 값을 반환 합니다. 문 핸들 할당 또는 준비 된 상태로 다시 설정 될 때까지 캐시 된 행 개수 값을 유효 합니다. 문을 다시 실행은, 또는 **SQLCloseCursor** 라고 합니다. SQL_DIAG_ROW_COUNT 필드 설정 되었으므로 함수 호출 된 경우 값을 반환 하 여 유의 **SQLRowCount** SQL_DIAG_ROW_COUNT 필드는으로 다시 설정 하므로 SQL_DIAG_ROW_COUNT 필드의 값에서 다를 수 있습니다 함수 호출에 의해 0입니다.  
  
 다른 문 및 함수에 대 한 드라이버에서 반환 되는 값을 정의할 수 있습니다 \* *RowCountPtr*합니다. 예를 들어 일부 데이터 소스에서 반환 된 행 수를 반환 하는 일을 할 수 있습니다는 **선택** 문 또는 행을 인출 하기 전에 카탈로그 함수입니다.  
  
> [!NOTE]  
>  여러 데이터 원본을 결과 페치 하며 전에 집합에 행의 수를 반환할 수 없습니다. 응용 프로그램 최대 상호 운용성을 위해이 동작에 의존 하지 해야 합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLRowCount** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* SQL_의 HANDLE_STMT와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLRowCount** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLRowCount** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 함수를 호출한 호출 하기 전에 **SQLExecute**를 **SQLExecDirect**에 **SQLBulkOperations**, 또는 **SQLSetPos** 합니다 에대한 *StatementHandle*합니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 문 핸들에서 실행 된 마지막 SQL 문이 경우 없었습니다는 **업데이트**, **삽입**, 또는 **삭제** 문 또는 경우에는 *작업* 이전 호출에서 인수 **SQLBulkOperations** SQL_ADD, SQL_UPDATE_BY_BOOKMARK, 또는 SQL_DELETE_BY_BOOKMARK, 또는 경우에는 *작업* 에대한이전호출의인수 **SQLSetPos** SQL_UPDATE 또는 SQL_DELETE, 값 **RowCountPtr* 드라이버 정의 됩니다. 자세한 내용은 [영향을 받는 행 개수 확인](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|SQL 문을 실행합니다.|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
