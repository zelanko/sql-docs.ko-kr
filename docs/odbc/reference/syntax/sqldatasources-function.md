---
title: "SQLDataSources 함수 | Microsoft Docs"
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
- SQLDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSources
helpviewer_keywords:
- SQLDataSources function [ODBC]
ms.assetid: 3f63b1b4-e70e-44cd-96c6-6878d50d0117
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fc056c3877b76bebdb0402248b6fe6cb9a919d49
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqldatasources-function"></a>SQLDataSources 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLDataSources** 데이터 원본에 대 한 정보를 반환 합니다. 이 함수는 드라이버 관리자에서만 구현 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLDataSources(  
     SQLHENV          EnvironmentHandle,  
     SQLUSMALLINT     Direction,  
     SQLCHAR *        ServerName,  
     SQLSMALLINT      BufferLength1,  
     SQLSMALLINT *    NameLength1Ptr,  
     SQLCHAR *        Description,  
     SQLSMALLINT      BufferLength2,  
     SQLSMALLINT *    NameLength2Ptr);  
```  
  
## <a name="arguments"></a>인수  
 *EnvironmentHandle*  
 [입력] 환경 핸들입니다.  
  
 *방향*  
 [입력] 데이터 소스에 드라이버 관리자 정보에 대 한 반환을 결정 합니다. 다음 값 중 하나일 수 있습니다.  
  
 SQL_FETCH_NEXT (을 인출 하는 목록에는 다음 데이터 원본 이름), SQL_FETCH_FIRST (목록의 시작 부분에서 fetch)을, SQL_FETCH_FIRST_USER (사용자에 게 첫 번째 인출 DSN) 또는 SQL_FETCH_FIRST_SYSTEM (을 인출 하는 첫 번째 시스템 DSN).  
  
 때 *방향* SQL_FETCH_FIRST에 대 한 후속 호출으로 설정 된 **SQLDataSources** 와 *방향* 사용자와 시스템 Dsn을 반환 하는 SQL_FETCH_NEXT로 설정 합니다. 때 *방향* SQL_FETCH_FIRST_USER, 모든 후속 호출으로 설정 된 **SQLDataSources** 와 *방향* SQL_FETCH_NEXT로 설정 사용자 Dsn만 반환 합니다. 때 *방향* SQL_FETCH_FIRST_SYSTEM, 모든 후속 호출으로 설정 된 **SQLDataSources** 와 *방향* SQL_FETCH_NEXT로 설정 시스템 Dsn만 반환 합니다.  
  
 *데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면*  
 [출력] 데이터 원본 이름을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 경우 *ServerName* 이 NULL 이면 *NameLength1Ptr* 는 문자 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 여전히 가리키는 버퍼에서 반환할 수 *ServerName*합니다.  
  
 *BufferLength1*  
 [입력] 길이 **ServerName* 문자에서 버퍼링; SQL_MAX_DSN_LENGTH와 null 종료 문자 보다 길 수에 필요 하지 않습니다.  
  
 *NameLength1Ptr*  
 [출력] 문자 (null 종결 문자 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *ServerName*합니다. 반환할 수 있는 문자 수는 보다 크거나 같은 경우 *BufferLength1*, 데이터 원본 이름 \* *ServerName* 잘립니다 *BufferLength1* null 종결 문자 길이 뺀 값입니다.  
  
 *설명*  
 [출력] 데이터 소스와 연결 된 드라이버의 설명을 반환 하는 버퍼에 대 한 포인터입니다. 예를 들어 dBASE 또는 SQL Server입니다.  
  
 경우 *설명* 이 NULL 이면 *NameLength2Ptr* 는 문자 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 여전히 가리키는 버퍼에서 반환할 수 *설명*합니다.  
  
 *BufferLength2*  
 [입력] 문자 길이 **설명* 버퍼입니다.  
  
 *NameLength2Ptr*  
 [출력] 문자 (null 종결 문자 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *설명*합니다. 반환할 수 있는 문자 수는 보다 크거나 같은 경우 *BufferLength2*에서 드라이버 설명을 \* *설명* 잘립니다 *BufferLength2 * null 종결 문자 길이 뺀 값입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDataSources** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 관련된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 와 *HandleType*SQL_HANDLE_ENV의 및 *처리* 의 *EnvironmentHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLDataSources** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|(DM) 드라이버 관리자 별 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|(DM) 버퍼 \* *ServerName* 충분히 완전 한 데이터 원본 이름을 반환할 수 없습니다. 따라서 이름이 잘렸습니다. 전체 데이터 원본 이름의 길이가 반환 됩니다 \* *NameLength1Ptr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)<br /><br /> (DM) 버퍼 \* *설명* 하지 만큼 충분히 큰지 전체 드라이버 설명을 반환 합니다. 따라서 설명을 잘렸습니다. 잘리지 않은 데이터 원본 설명의 길이에서 **NameLength2Ptr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|(DM)에 대 한 특정 없는 SQLSTATE 했습니다는 하는 오류가 발생 없는 구현 별 SQLSTATE가 정의 된 합니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 * \*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버 관리자에서 (DM) 함수는 완료 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대해 지정 된 값 (DM) *BufferLength1* 0 보다 작습니다.<br /><br /> 인수에 대해 지정 된 값 (DM) *BufferLength2* 0 보다 작습니다.|  
|HY103|검색 코드가 잘못 되었습니다|인수에 대해 지정 된 값 (DM) *방향* SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM, 또는 SQL_FETCH_NEXT 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
  
## <a name="comments"></a>설명  
 때문에 **SQLDataSources** 구현 된 드라이버 관리자에서 특정 드라이버의 표준 준수에 관계 없이 모든 드라이버에 지원 됩니다.  
  
 응용 프로그램에서 호출할 수 **SQLDataSources** 모든 데이터 원본 이름을 검색 하기 위해 여러 번입니다. 드라이버 관리자는 시스템 정보에서이 정보를 검색합니다. 데이터 원본 이름이 더 이상 없으면 때 드라이버 관리자는 SQL_NO_DATA를 반환 합니다. 경우 **SQLDataSources** SQL_FETCH_NEXT 첫 번째 데이터 원본 이름을 반환 합니다 SQL_NO_DATA를 반환 된 후 즉시 호출 됩니다. 응용 프로그램에서 반환 된 정보를 사용 하는 방법에 대 한 내용은 **SQLDataSources**, 참조 [데이터 원본이 나 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
 SQL_FETCH_NEXT에 전달 되 면 **SQLDataSources** 처음 호출 될 첫 번째 데이터 원본 이름을 반환 합니다.  
  
 드라이버는 데이터 원본 이름은 실제 데이터 원본에 매핑하는 방식을 결정 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|검색 및 데이터 원본에 연결 하는 데 필요한 값을 나열|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|드라이버 설명 및 특성을 반환합니다.|[SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

