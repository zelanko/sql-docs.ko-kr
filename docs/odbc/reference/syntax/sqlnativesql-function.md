---
title: SQLNativeSql 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9666bc767affb3b6bb624c416614079193d4b921
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304724"
---
# <a name="sqlnativesql-function"></a>SQLNativeSql 함수(SQLNativeSql Function)
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLNativeSql** 는 드라이버에 의해 수정 된 SQL 문자열을 반환 합니다. **SQLNativeSql** 는 SQL 문을 실행 하지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
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
 [Input] 연결 핸들입니다.  
  
 *온 Atementtext*  
 입력 변환할 SQL 텍스트 문자열입니다.  
  
 *TextLength1*  
 입력 **의* 문자 길이입니다.  
  
 *OutStatementText*  
 출력 번역 된 SQL 문자열을 반환할 버퍼에 대 한 포인터입니다.  
  
 *OutStatementText* 가 NULL 인 경우 *TextLength2Ptr* 는 *OutStatementText*가 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 문자 데이터의 NULL 종료 문자를 제외한 총 문자 수를 반환 합니다.  
  
 *BufferLength*  
 입력 \* *OutStatementText* 버퍼의 문자 수입니다. **SQLNativeSqlW**를 호출 하는 경우에 호출 된 * \*atementtext* 에서 반환 된 값이 유니코드 문자열이 면 *bufferlength* 인수는 짝수 여야 합니다.  
  
 *TextLength2Ptr*  
 출력 \* *OutStatementText*에서 반환 하는 데 사용할 수 있는 총 문자 수 (null 종료 제외)를 반환할 버퍼에 대 한 포인터입니다. 반환할 수 있는 문자 수가 *bufferlength*보다 크거나 같은 경우 \* *OutStatementText* 의 변환 된 SQL 문자열은 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLNativeSql** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_DBC의 *HandleType* 및 *ConnectionHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLNativeSql** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|버퍼 \* *OutStatementText* 는 전체 sql 문자열을 반환 하기에 충분 하지 않아 sql 문자열이 잘렸습니다. 잘리지 않는 SQL 문자열의 길이는 **TextLength2Ptr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08003|연결이 열려 있지 않음|*ConnectionHandle* 가 연결 된 상태가 아닙니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|22007|날짜/시간 형식이 잘못 되었습니다.|*사용 중인 *Atementtext* 에 잘못 된 날짜, 시간 또는 타임 스탬프 값을 가진 이스케이프 절이 포함 되어 있습니다.|  
|24000|잘못된 커서 상태|문에서 참조 되는 커서가 결과 집합의 시작 앞 이나 결과 집합의 끝 앞에 배치 되었습니다. 기본 DBMS 커서 구현이 있는 드라이버에서는이 오류가 반환 되지 않을 수 있습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|(DM) * on*Atementtext* 가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *ConnectionHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며이 함수가 호출 될 때 여전히 실행 되 고 있습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *TextLength1* 가 0 보다 작지만 SQL_NTS와 같지 않습니다.|  
|||(DM) 인수 *Bufferlength* 가 0 보다 작고 *OutStatementText* 인수가 null 포인터가 아닙니다.|  
|HY109|커서 위치가 잘못 되었습니다.|커서의 현재 행이 삭제 되었거나 인출 되지 않았습니다. 기본 DBMS 커서 구현이 있는 드라이버에서는이 오류가 반환 되지 않을 수 있습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *ConnectionHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 다음은 스칼라 함수 CONVERT를 포함 하는 **SQLNativeSql** 입력 SQL 문자열에 대해 반환 될 수 있는 작업의 예입니다. Empid 열이 데이터 원본에서 정수 형식 이라고 가정 합니다.  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server에 대 한 드라이버는 다음과 같은 번역 된 SQL 문자열을 반환할 수 있습니다.  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 ORACLE Server 용 드라이버는 다음과 같은 번역 된 SQL 문자열을 반환할 수 있습니다.  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres 드라이버는 다음과 같은 번역 된 SQL 문자열을 반환할 수 있습니다.  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 자세한 내용은 [직접 실행](../../../odbc/reference/develop-app/direct-execution-odbc.md) 및 [준비 된 실행](../../../odbc/reference/develop-app/prepared-execution-odbc.md)을 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
 없음  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
