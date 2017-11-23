---
title: "SQLDrivers 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLDrivers
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDrivers
helpviewer_keywords: SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8528eb498b4c15a3d55aa3b3a09947c85329918b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqldrivers-function"></a>SQLDrivers 함수
**규칙**  
 도입 된 버전: ODBC 2.0 표준 준수: ODBC  
  
 **요약**  
 **SQLDrivers** 드라이버 설명 하 고 드라이버 특성 키워드를 나열 합니다. 이 함수는 드라이버 관리자에서만 구현 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLDrivers(  
     SQLHENV         EnvironmentHandle,  
     SQLUSMALLINT    Direction,  
     SQLCHAR *       DriverDescription,  
     SQLSMALLINT     BufferLength1,  
     SQLSMALLINT *   DescriptionLengthPtr,  
     SQLCHAR *       DriverAttributes,  
     SQLSMALLINT     BufferLength2,  
     SQLSMALLINT *   AttributesLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *EnvironmentHandle*  
 [입력] 환경 핸들입니다.  
  
 *방향*  
 [입력] 드라이버 관리자 목록 (SQL_FETCH_NEXT) 또는 (SQL_FETCH_FIRST) 목록의 시작 부분에서 검색이 시작 되는 여부에 다음 드라이버 설명을 인출 하는지 여부를 결정 합니다.  
  
 *DriverDescription*  
 [출력] 드라이버 설명을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 경우 *DriverDescription* 이 NULL 이면 *DescriptionLengthPtr* 여전히 문자 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 합니다에 반환할 사용할 수는 버퍼에서 가리키는 *DriverDescription*합니다.  
  
 *BufferLength1*  
 [입력] 길이 **DriverDescription* 문자에서 버퍼입니다.  
  
 *DescriptionLengthPtr*  
 [출력] 문자 (null 종결 문자 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *DriverDescription*합니다. 반환할 수 있는 문자 수는 보다 크거나 같은 경우 *BufferLength1*에서 드라이버 설명을 \* *DriverDescription* 잘립니다  *BufferLength1* null 종결 문자 길이 뺀 값입니다.  
  
 *DriverAttributes*  
 [출력] ("주석" 참조) 드라이버 특성 값 쌍의 목록을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 경우 *DriverAttributes* 이 NULL 이면 *AttributesLengthPtr* 여전히 바이트 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 버퍼에서 반환할 수 가 가리키는 *DriverAttributes*합니다.  
  
 *BufferLength2*  
 [입력] 길이 \* *DriverAttributes* 문자에서 버퍼입니다. 경우는  *\*DriverDescription* 값은 유니코드 문자열 (호출할 때 **SQLDriversW**), *BufferLength* 인수 수는 짝수 여야 합니다.  
  
 *AttributesLengthPtr*  
 [출력] 바이트 (null 종료 바이트 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *DriverAttributes*합니다. 보다 크거나 반환에 사용할 수 있는 바이트 수가 *BufferLength2*에서 특성 값 쌍의 목록 \* *DriverAttributes* 잘립니다  *BufferLength2* null 종결 문자 길이 뺀 값입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDrivers** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 관련된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 의 SQL_HANDLE_ENV 및 *처리* 의 *EnvironmentHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLDrivers** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|(DM) 드라이버 관리자 별 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|(DM) 버퍼 \* *DriverDescription* 하지 만큼 충분히 큰지 전체 드라이버 설명을 반환 합니다. 따라서 설명을 잘렸습니다. 전체 드라이버 설명의 길이에 반환 됩니다 \* *DescriptionLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)<br /><br /> (DM) 버퍼 \* *DriverAttributes* 충분히 특성 값 쌍의 전체 목록을 반환할 수 없습니다. 따라서 목록이 잘렸습니다. 특성 값 쌍의 잘리지 않은 목록의 길이에 반환 됩니다 **AttributesLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버 관리자에서 (DM) 함수는 완료 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대해 지정 된 값 (DM) *BufferLength1* 0 보다 작습니다.<br /><br /> 인수에 대해 지정 된 값 (DM) *BufferLength2* 0 보다 작거나 1로 되었습니다.|  
|HY103|검색 코드가 잘못 되었습니다|인수에 대해 지정 된 값 (DM) *방향* SQL_FETCH_FIRST 또는 SQL_FETCH_NEXT 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
  
## <a name="comments"></a>설명  
 **SQLDrivers** 드라이버 설명에서 반환 된 \* *DriverDescription* 버퍼입니다. 드라이버에 대 한 추가 정보를 반환 하는 것은 \* *DriverAttributes* 키워드-값 쌍의 목록으로 버퍼입니다. 드라이버에 대 한 모든 드라이버를 제외 하 고 반환 됩니다에 대 한 시스템 정보에 나열 된 모든 키워드가 **CreateDSN**, 데이터 원본 만들 것인지 묻는 메시지가 사용 되 고 있는 따라서 선택 사항입니다. Null 바이트가 각 쌍이 종료 되 고 전체 목록은 바이트 null로 종료 됩니다 (즉, 두 개의 null 바이트 표시 목록의 끝). 예를 들어 C 구문을 사용 하 여 파일 기반 드라이버는 다음과 같은 특성 ("\0" null 문자를 나타냄)를 반환할 수 있습니다.  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 경우 \* *DriverAttributes* 은 하지를 보유할 만큼 크지 전체 목록, 목록 잘리면 **SQLDrivers** SQLSTATE 01004 (데이터 잘림) 및 목록의 길이 반환 합니다 (제외 하 고는 최종 null 종료 바이트)에 반환 된 **AttributesLengthPtr*합니다.  
  
 드라이버 특성 키워드는 드라이버를 설치할 때 시스템 정보에서 추가 됩니다. 자세한 내용은 참조 [ODBC 구성 요소 설치](../../../odbc/reference/install/installing-odbc-components.md)합니다.  
  
 응용 프로그램에서 호출할 수 **SQLDrivers** 여러 번 모든 드라이버 설명을 검색할 수 있습니다. 드라이버 관리자는 시스템 정보에서이 정보를 검색합니다. 더 많은 드라이버 설명이 없을 때 **SQLDrivers** SQL_NO_DATA를 반환 합니다. 경우 **SQLDrivers** SQL_NO_DATA를 반환 된 후 첫 번째 드라이버 설명을 반환 하는 즉시 SQL_FETCH_NEXT 함께 호출 되었습니다. 응용 프로그램에서 반환 된 정보를 사용 하는 방법에 대 한 내용은 **SQLDrivers**, 참조 [데이터 원본이 나 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
 SQL_FETCH_NEXT에 전달 되 면 **SQLDrivers** 처음 호출 될 **SQLDrivers** 첫 번째 데이터 원본 이름을 반환 합니다.  
  
 때문에 **SQLDrivers** 구현 된 드라이버 관리자에서 특정 드라이버의 표준 준수에 관계 없이 모든 드라이버에 지원 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|검색 및 데이터 원본에 연결 하는 데 필요한 값을 나열|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본 이름 반환|[SQLDataSources 함수](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
