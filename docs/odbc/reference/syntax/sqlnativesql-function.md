---
title: SQL네이티브Sql 함수 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304724"
---
# <a name="sqlnativesql-function"></a>SQLNativeSql 함수(SQLNativeSql Function)
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLNativeSql은** 드라이버에서 수정한 SQL 문자열을 반환합니다. **SQLNativeSql은** SQL 문을 실행하지 않습니다.  
  
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
 *연결 핸들*  
 [Input] 연결 핸들입니다.  
  
 *명문 텍스트*  
 [입력] SQL 텍스트 문자열을 번역할 수 있습니다.  
  
 *텍스트 길이1*  
 [입력] **InStatementText* 텍스트 문자열의 문자 길이입니다.  
  
 *OutStatementText*  
 [출력] 번역된 SQL 문자열을 반환할 버퍼에 대한 포인터입니다.  
  
 *OutStatementText가* NULL인 경우 *TextLength2Ptr은* *OutStatementText로*가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] \* *OutStatementText* 버퍼의 문자 수입니다. * \*InStatementText에서* 반환되는 값이 유니코드 문자열인 **경우(SQLNativeSqlW를**호출할 때) *BufferLength* 인수는 짝수여야 합니다.  
  
 *텍스트 길이2Ptr*  
 [출력] \* *OutStatementText에서*반환할 수 있는 총 문자 수(null-termination 제외)를 반환하는 버퍼에 대한 포인터입니다. 반환할 수 있는 문자 수가 *BufferLength보다*크거나 같으면 \* *OutStatementText의* 변환된 SQL 문자열이 *BufferLength에서* null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLNativeSql이** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_DBC 및 *연결 핸들*핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. *Handle* 다음 표에서는 **SQLNativeSql에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|버퍼 \* *OutStatementText* 전체 SQL 문자열을 반환 하기에 충분 하지 않은, 그래서 SQL 문자열 잘 린 된. 잘린 SQL 문자열의 길이는 **TextLength2Ptr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08003|연결이 열려 있지 않음|*연결 핸들이* 연결된 상태가 아닙니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|22007|잘못된 날짜 시간 형식|**InStatementText에는* 잘못된 날짜, 시간 또는 타임스탬프 값이 있는 이스케이프 절이 포함되어 있습니다.|  
|24000|잘못된 커서 상태|명령문에서 참조된 커서는 결과 집합이 시작되기 전이나 결과 집합이 끝난 후에 배치되었습니다. 기본 DBMS 커서 구현을 가진 드라이버에서 이 오류가 반환되지 않을 수 있습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY09|null 포인터의 잘못된 사용|(DM) **InStatementText는* null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) 비동기적으로 실행 되는 *함수는 ConnectionHandle에* 대 한 호출 하 고이 함수를 호출 하는 때 여전히 실행 되 고.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) *인수 TextLength1은* 0보다 작지만 SQL_NTS 같지 는 않습니다.|  
|||(DM) 인수 *버퍼길이* 0보다 적고 *인수 OutStatementText가* null 포인터가 아닙니다.|  
|HY109|잘못된 커서 위치|커서의 현재 행이 삭제되었거나 가져오지 않았습니다. 기본 DBMS 커서 구현을 가진 드라이버에서 이 오류가 반환되지 않을 수 있습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *연결 핸들과* 연결된 드라이버가 기능을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 다음은 **SQLNativeSql이** 스칼라 함수 CONVERT를 포함하는 다음 입력 SQL 문자열에 대해 반환할 수 있는 작업의 예입니다. 열 이 데이터 원본에서 형식 정수기라고 가정합니다.  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server용 드라이버는 다음과 같은 번역된 SQL 문자열을 반환할 수 있습니다.  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 ORACLE Server의 드라이버는 다음과 같은 번역된 SQL 문자열을 반환할 수 있습니다.  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres에 대한 드라이버는 다음과 같은 번역된 SQL 문자열을 반환할 수 있습니다.  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 자세한 내용은 [직접 실행](../../../odbc/reference/develop-app/direct-execution-odbc.md) 및 [준비된 실행을](../../../odbc/reference/develop-app/prepared-execution-odbc.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
 없음  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
