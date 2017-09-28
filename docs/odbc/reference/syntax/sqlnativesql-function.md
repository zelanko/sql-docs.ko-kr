---
title: "SQLNativeSql 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLNativeSql
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNativeSql
helpviewer_keywords:
- SQLNativeSql function [ODBC]
ms.assetid: b8efc247-27ab-4a00-92b6-1400785783fe
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1672e4c1f21d223ed326c0e0649fc7cbb2376f74
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlnativesql-function"></a>SQLNativeSql 함수(SQLNativeSql Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLNativeSql** 드라이버에 의해 수정 된 대로 SQL 문자열을 반환 합니다. **SQLNativeSql** SQL 문을 실행 하지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLNativeSql(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      InStatementText,  
     SQLINTEGER     TextLength1,  
     SQLCHAR *      OutStatementText,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   TextLength2Ptr);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [입력] 연결 핸들입니다.  
  
 *InStatementText*  
 [입력] 번역 해야 SQL 텍스트 문자열입니다.  
  
 *TextLength1*  
 [입력] 문자 길이 **InStatementText* 텍스트 문자열입니다.  
  
 *OutStatementText*  
 [출력] 번역 된 SQL 문자열을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 경우 *OutStatementText* 이 NULL 이면 *TextLength2Ptr* 여전히 문자 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 버퍼에서 반환할 수 가 가리키는 *OutStatementText*합니다.  
  
 *BufferLength*  
 [입력] 문자 수는 \* *OutStatementText* 버퍼입니다. 에 값이 반환 하는 경우 * \*InStatementText* 는 유니코드 문자열 (호출할 때 **SQLNativeSqlW**), *BufferLength* 인수 수는 짝수 여야 합니다.  
  
 *TextLength2Ptr*  
 [출력] \(제외 null 종료) 사용할 수 있는 문자를 반환 하려면의 총 수를 반환 하는 버퍼에 대 한 포인터 \* *OutStatementText*합니다. 반환할 수 있는 문자 수는 보다 크거나 같은 경우 *BufferLength*에 SQL 문자열을 번역 \* *OutStatementText* 잘립니다 * BufferLength* null 종결 문자 길이 뺀 값입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLNativeSql** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 관련된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 와 *HandleType* sql_handle_dbc 라는의 및 *처리* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLNativeSql** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *OutStatementText* 충분히 SQL 문자열이 잘림 하므로 전체 SQL 문자열을 반환할 수 없습니다. 잘리지 않은 SQL 문자열의 길이에서 **TextLength2Ptr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08003|연결이 열려 있지 않습니다|*ConnectionHandle* 가 연결 된 상태가 아닙니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|22007|잘못 된 날짜/시간 형식|**InStatementText* 날짜, 시간 또는 타임 스탬프 값이 잘못 된 escape 절을 포함 합니다.|  
|24000|잘못된 커서 상태|문에서 참조 하는 커서 시작 이후 또는 결과 집합의 끝 이후에 결과 집합의 앞에 배치 되었습니다. 기본적인 DBMS 커서 구현이 필요 드라이버에서이 오류를 반환할 수 있습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 * \*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) **InStatementText* 는 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()를 비동기적으로 실행 중인 함수에 대해 호출 되었습니다는 *ConnectionHandle* 호출 되었을 때 계속 실행 하 고 있습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 인수 *TextLength1* 같지 않음 SQL_NTS 있지만 0 보다 작습니다.|  
|||(DM) 인수 *BufferLength* 가 0과 인수 보다 작은 *OutStatementText* null 포인터는 없습니다.|  
|HY109|잘못 된 커서 위치|커서의 현재 행 삭제 또는 페치 하지 했습니다. 기본적인 DBMS 커서 구현이 필요 드라이버에서이 오류를 반환할 수 있습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *ConnectionHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 다음은 항목의 예 **SQLNativeSql** CONVERT 스칼라 함수를 포함 하는 다음 입력된 SQL 문자열에 대 한 반환 될 수 있습니다. 데이터 원본에는 정수 유형의 열 empid 임을 가정 합니다.  
  
```  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server에 대 한 드라이버 번역된 된 다음 SQL 문자열을 반환할 수 있습니다.  
  
```  
SELECT convert (smallint, empid) FROM employee  
```  
  
 ORACLE 서버에 대 한 드라이버 번역된 된 다음 SQL 문자열을 반환할 수 있습니다.  
  
```  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres에 대 한 드라이버 번역된 된 다음 SQL 문자열을 반환할 수 있습니다.  
  
```  
SELECT int2 (empid) FROM employee  
```  
  
 자세한 내용은 참조 [직접 실행](../../../odbc/reference/develop-app/direct-execution-odbc.md) 및 [실행 준비](../../../odbc/reference/develop-app/prepared-execution-odbc.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
 없음  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
