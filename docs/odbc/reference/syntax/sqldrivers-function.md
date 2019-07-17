---
title: SQLDrivers 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDrivers
helpviewer_keywords:
- SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f54be3d11f4870533513f464c1afdae13e04f367
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104659"
---
# <a name="sqldrivers-function"></a>SQLDrivers 함수
**규칙**  
 도입 된 버전: ODBC 2.0 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLDrivers** 드라이버 설명 하 고 드라이버 특성 키워드를 나열 합니다. 이 함수에만 드라이버 관리자에 의해 구현 됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
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
  
 *Direction*  
 [입력] 드라이버 관리자 목록 (SQL_FETCH_NEXT) 또는 (SQL_FETCH_FIRST) 목록의 시작 부분에서 검색이 시작 되는 여부에 다음 드라이버 설명을 인출 하는지 여부를 결정 합니다.  
  
 *DriverDescription*  
 [출력] 드라이버 설명을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 하는 경우 *DriverDescription* 가 null 인 경우 *DescriptionLengthPtr* (문자 데이터에 대 한 null 종료 문자를 제외한) 문자의 총 수를 반환 계속 됩니다에서 반환할 수는 가리키는 버퍼 *DriverDescription*합니다.  
  
 *BufferLength1*  
 [입력] 길이 **DriverDescription* 문자에서 버퍼입니다.  
  
 *DescriptionLengthPtr*  
 [출력] 문자 (null 종결 문자가 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *DriverDescription*합니다. 반환할 사용 가능한 문자 개수 보다 크거나 같은 경우 *BufferLength1*에서 드라이버 설명을 \* *DriverDescription* 잘립니다  *BufferLength1* null 종료 문자 길이 뺀 값입니다.  
  
 *DriverAttributes*  
 [출력] \("주석" 참조) 드라이버 특성 값 쌍의 목록을 반환 하는 버퍼에 대 한 포인터입니다.  
  
 하는 경우 *DriverAttributes* 가 null 인 경우 *AttributesLengthPtr* 바이트 (문자 데이터에 대 한 null 종료 문자 제외)의 총 수를 반환 여전히는 버퍼에서 반환할 사용 가능한 가 가리키는 *DriverAttributes*합니다.  
  
 *BufferLength2*  
 [입력] 길이 \* *DriverAttributes* 문자에서 버퍼입니다. 경우는  *\*DriverDescription* 값은 유니코드 문자열 (호출할 때 **SQLDriversW**), *BufferLength* 인수 수는 짝수 여야 합니다.  
  
 *AttributesLengthPtr*  
 [출력] 바이트 (null 종료 바이트 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *DriverAttributes*합니다. 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *BufferLength2*에 있는 특성 값 쌍의 목록 \* *DriverAttributes* 잘립니다  *BufferLength2* null 종료 문자 길이 뺀 값입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDrivers** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 연관된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 SQL_HANDLE_ENV와 *처리할* 의 *EnvironmentHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLDrivers** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|(DM) 드라이버 관리자 별 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|(DM) 버퍼 \* *DriverDescription* 전체 드라이버 설명을 반환 하는 충분히 큰 수 없습니다. 따라서 설명을 잘렸습니다. 전체 드라이버 설명의 길이에 반환 됩니다 \* *DescriptionLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)<br /><br /> (DM) 버퍼 \* *DriverAttributes* 충분히 특성 값 쌍의 전체 목록을 반환할 수 없습니다. 따라서 목록이 잘렸습니다. 특성 값 쌍의 잘리지 않은 목록의 길이에서 **AttributesLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|(DM)의 드라이버 관리자 지원 함수 완료 또는 실행 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대 한 지정 된 값 (DM) *BufferLength1* 0 보다 작습니다.<br /><br /> 인수에 대 한 지정 된 값 (DM) *BufferLength2* 보다 작거나 0 또는 1과 같습니다.|  
|HY103|검색 코드가 잘못 되었습니다|인수에 지정 된 값 (DM) *방향을* SQL_FETCH_FIRST 또는 SQL_FETCH_NEXT 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
  
## <a name="comments"></a>주석  
 **SQLDrivers** 에 대 한 드라이버 설명을 반환 합니다 \* *DriverDescription* 버퍼입니다. 드라이버에 대 한 추가 정보를 반환 합니다 \* *DriverAttributes* 키워드-값 쌍의 목록으로 버퍼입니다. 드라이버에 대 한 모든 드라이버를 제외 하 고 반환 됩니다에 대 한 시스템 정보에 나열 된 모든 키워드 **CreateDSN**, 데이터 원본 만들 것인지 묻는 메시지가 사용 되 고 따라서은 선택 사항입니다. 각 쌍을 null 바이트를 사용 하 여 종료 되 고 전체 목록은 null 바이트를 사용 하 여 종료 됩니다 (즉, 두 개의 null 바이트 표시를 목록의 끝). 예를 들어 C 구문을 사용 하 여 파일 기반 드라이버는 다음과 같은 특성 ("\0" null 문자를 나타냄)을 반환할 수 있습니다.  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 경우 \* *DriverAttributes* 는 하지을 저장할 만큼 큰 전체 목록, 목록 잘리면 **SQLDrivers** SQLSTATE 01004 (데이터 잘림) 및 목록의 길이 반환 합니다 (제외 합니다 최종 null 종료 바이트)에서 반환은 **AttributesLengthPtr*합니다.  
  
 드라이버 특성 키워드는 드라이버를 설치할 때 시스템 정보에서 추가 됩니다. 자세한 내용은 [ODBC 구성 요소 설치](../../../odbc/reference/install/installing-odbc-components.md)합니다.  
  
 응용 프로그램에서 호출할 수 있습니다 **SQLDrivers** 여러 번 모든 드라이버 설명 검색 합니다. 드라이버 관리자는 시스템 정보에서이 정보를 검색합니다. 더 많은 드라이버 설명 없음 있을 때 **SQLDrivers** SQL_NO_DATA를 반환 합니다. 하는 경우 **SQLDrivers** SQL_FETCH_NEXT SQL_NO_DATA가 반환 후 첫 번째 드라이버 설명을 반환 하는 즉시 호출 됩니다. 응용 프로그램에서 반환 된 정보를 사용 하는 방법에 대 한 자세한 **SQLDrivers**를 참조 하세요 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)합니다.  
  
 SQL_FETCH_NEXT에 전달 되 면 **SQLDrivers** 처음 호출 되 **SQLDrivers** 첫 번째 데이터 원본 이름을 반환 합니다.  
  
 때문에 **SQLDrivers** 구현 된 드라이버 관리자에서 특정 드라이버의 표준 준수에 관계 없이 모든 드라이버에 대 한 지원 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|검색 및 데이터 원본에 연결 하는 데 필요한 값을 나열|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본 이름 반환|[SQLDataSources 함수](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
