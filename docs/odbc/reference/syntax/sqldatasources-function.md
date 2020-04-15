---
title: SQLDataSource 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b56a6c25e54897e67beaf39d3b7797ac45391d7b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301183"
---
# <a name="sqldatasources-function"></a>SQLDataSources 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLDataSource는** 데이터 원본에 대한 정보를 반환합니다. 이 함수는 드라이버 관리자에서만 구현됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
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
 *환경 핸들*  
 [입력] 환경 핸들입니다.  
  
 *방향*  
 [입력] 드라이버 관리자가 정보를 반환하는 데이터 원본을 결정합니다. 다음 값 중 하나일 수 있습니다.  
  
 SQL_FETCH_NEXT(목록의 다음 데이터 원본 이름을 가져오려면), SQL_FETCH_FIRST(목록의 시작 부분에서 가져오기), SQL_FETCH_FIRST_USER(첫 번째 사용자 DSN 가져오기) 또는 SQL_FETCH_FIRST_SYSTEM(첫 번째 시스템 DSN을 가져오기 위해)  
  
 *방향이* SQL_FETCH_FIRST 설정되면 *방향이* 있는 **SQLDataSource에** 대한 후속 호출이 사용자 및 시스템 DSN을 모두 반환하지 SQL_FETCH_NEXT 설정됩니다. *방향이* SQL_FETCH_FIRST_USER 설정되면 *방향이* 있는 **SQLDataSource에** 대한 모든 후속 호출은 사용자 DSN만 반환하도록 SQL_FETCH_NEXT 설정됩니다. *방향이* SQL_FETCH_FIRST_SYSTEM 설정되면 *방향이* 있는 **SQLDataSource에** 대한 모든 후속 호출이 시스템 DSN만 반환하도록 SQL_FETCH_NEXT 설정됩니다.  
  
 *ServerName*  
 [출력] 데이터 원본 이름을 반환할 버퍼에 대한 포인터입니다.  
  
 *ServerName이* NULL인 경우 *NameLength1Ptr은* *서버이름으로*가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼길이1*  
 [입력] * 서버*이름* 버퍼의 길이( 문자) 이 SQL_MAX_DSN_LENGTH null 종료 문자보다 길 필요는 없습니다.  
  
 *이름길이1Ptr*  
 [출력] \* *ServerName에서*반환할 수 있는 총 문자 수(null-termination 문자 제외)를 반환하는 버퍼에 대한 포인터입니다. 반환할 수 있는 문자 수가 *BufferLength1보다*크거나 같으면 \* *ServerName의* 데이터 원본 이름이 *BufferLength1에* 잘려null 종료 문자의 길이를 뺀 값입니다.  
  
 *설명*  
 [출력] 데이터 원본과 연결된 드라이버에 대한 설명을 반환할 버퍼에 대한 포인터입니다. 예를 들어, dBASE 또는 SQL Server.  
  
 *설명이* NULL인 경우 *NameLength2Ptr은* *설명에서*가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼길이2*  
 [입력] **설명* 버퍼의 문자 길이입니다.  
  
 *이름길이2Ptr*  
 [출력] \* *설명에서*반환할 수 있는 총 문자 수(null-termination 문자 제외)를 반환하는 버퍼에 대한 포인터입니다. 반환할 수 있는 문자 수가 *BufferLength2보다*크거나 같으면 \* *설명의* 드라이버 설명이 *BufferLength2로* 잘려null 종료 문자의 길이를 뺀 값입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLDataSource** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 *핸들 유형* SQL_HANDLE_ENV 및 *환경 핸들*핸들을 호출 하 여 가져올 수 *Handle* **있습니다.** 다음 표에서는 일반적으로 **SQLDataSource에서** 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|(DM) 드라이버 관리자 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|(DM) 버퍼 \* *서버이름이* 전체 데이터 원본 이름을 반환할 만큼 크지 않았습니다. 따라서 이름이 잘렸습니다. 전체 데이터 원본 이름의 길이는 \* *NameLength1Ptr*에서 반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)<br /><br /> (DM) 버퍼 \* *설명이* 전체 드라이버 설명을 반환할 만큼 충분히 크지 않았습니다. 따라서 설명이 잘렸습니다. 잘린 데이터 원본 설명의 길이는 **NameLength2Ptr*에서 반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|HY000|일반 오류|(DM) 특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|(DM) 드라이버 관리자가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) *인수 BufferLength1에* 대해 지정된 값이 0보다 적습니다.<br /><br /> (DM) *인수 BufferLength2에* 대해 지정된 값이 0보다 적습니다.|  
|HY103|잘못된 검색 코드|(DM) 인수 *방향에* 대해 지정된 값이 SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM 또는 SQL_FETCH_NEXT 같지 않았습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
  
## <a name="comments"></a>주석  
 **SQLDataSource는** 드라이버 관리자에서 구현되므로 특정 드라이버의 표준 준수에 관계없이 모든 드라이버에 대해 지원됩니다.  
  
 응용 프로그램은 **SQLDataSource를** 여러 번 호출하여 모든 데이터 원본 이름을 검색할 수 있습니다. 드라이버 관리자는 시스템 정보에서 이 정보를 검색합니다. 데이터 원본 이름이 더 이상 없는 경우 드라이버 관리자는 SQL_NO_DATA 반환합니다. **SQLDataSource는** SQL_NO_DATA 반환한 직후 SQL_FETCH_NEXT 호출하면 첫 번째 데이터 원본 이름이 반환됩니다. 응용 프로그램이 **SQLDataSource에서**반환하는 정보를 사용하는 방법에 대한 자세한 내용은 [데이터 원본 또는 드라이버 선택을](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)참조하십시오.  
  
 SQL_FETCH_NEXT 처음 호출될 때 **SQLDataSource에** 전달되면 첫 번째 데이터 원본 이름이 반환됩니다.  
  
 드라이버는 데이터 원본 이름이 실제 데이터 원본에 매핑되는 방법을 결정합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본에 연결하는 데 필요한 값 검색 및 목록 지정|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용하여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|드라이버 설명 및 특성 반환|[SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
