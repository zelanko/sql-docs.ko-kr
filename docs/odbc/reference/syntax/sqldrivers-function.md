---
title: SQL드라이버 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2496e7cd5f2abe0831c72484bed374d7aa1513ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302764"
---
# <a name="sqldrivers-function"></a>SQLDrivers 함수
**규칙**  
 버전 출시: ODBC 2.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLDriver는** 드라이버 설명 및 드라이버 특성 키워드를 나열합니다. 이 함수는 드라이버 관리자에서만 구현됩니다.  
  
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
 *환경 핸들*  
 [입력] 환경 핸들입니다.  
  
 *방향*  
 [입력] 드라이버 관리자가 목록(SQL_FETCH_NEXT)에서 다음 드라이버 설명을 가져오는지 또는 검색이 목록의 시작 부분(SQL_FETCH_FIRST)부터 시작되는지 여부를 결정합니다.  
  
 *DriverDescription*  
 [출력] 드라이버 설명을 반환할 버퍼에 대한 포인터입니다.  
  
 *DriverDescription가* NULL인 경우 *설명LengthPtr은* *DriverDescription에서*가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼길이1*  
 [입력] * 드라이버*설명* 버퍼의 길이입니다.  
  
 *설명길이Ptr*  
 [출력] \* *DriverDescription에서*반환할 수 있는 총 문자 수(null-termination 문자 제외)를 반환하는 버퍼에 대한 포인터입니다. 반환할 수 있는 문자 수가 *BufferLength1보다*크거나 같으면 \* *DriverDescription의* 드라이버 설명이 *BufferLength1에서* null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
 *드라이버 속성*  
 [출력] 드라이버 특성 값 쌍 목록을 반환할 버퍼에 대한 포인터입니다("주석" 참조).  
  
 *DriverAttributes가* NULL인 경우 *AttributesLengthPtr은 DriverAttributes가* 가리키는 버퍼에서 반환할 수 있는 총 바이트 수(문자 데이터에 대한 null 종료 문자 제외)를 *반환합니다.*  
  
 *버퍼길이2*  
 [입력] \* *문자로 드라이버 특성* 버퍼의 길이입니다. DriverDescription 값이 유니코드 문자열인 **경우(SQLDriverW를**호출할 때) *BufferLength* 인수는 짝수여야 합니다. * \**  
  
 *속성길이Ptr*  
 [출력] \* *DriverAttributes에서*반환할 수 있는 총 바이트 수(null-termination 바이트 제외)를 반환하는 버퍼에 대한 포인터입니다. 반환할 수 있는 바이트 수가 *BufferLength2보다*크거나 같으면 \* *DriverAttributes의* 특성 값 쌍 목록이 *BufferLength2에서* null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLDriver가** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_ENV 및 *환경 핸들*핸들을 사용 하 *Handle* 여 **SQLGetDiagRec를** 호출 하 여 관련 된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLDriver에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|(DM) 드라이버 관리자 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|(DM) 버퍼 \* *드라이버설명이* 전체 드라이버 설명을 반환할 만큼 충분히 크지 않았습니다. 따라서 설명이 잘렸습니다. 전체 드라이버 설명의 길이는 \* *설명LengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)<br /><br /> (DM) 버퍼 \* *DriverAttributes* 특성 값 쌍의 전체 목록을 반환 하기에 충분 하지 않았습니다. 따라서 목록이 잘렸습니다. 특성 값 쌍의 잘린 목록의 길이는 **AttributesLengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|(DM) 드라이버 관리자가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) *인수 BufferLength1에* 대해 지정된 값이 0보다 적습니다.<br /><br /> (DM) *인수 BufferLength2에* 대해 지정된 값은 0보다 적거나 1과 같습니다.|  
|HY103|잘못된 검색 코드|(DM) 인수 *방향에* 대해 지정된 값이 SQL_FETCH_FIRST SQL_FETCH_NEXT 같지 않았습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
  
## <a name="comments"></a>주석  
 **SQLDriver** \* *드라이버 설명* 버퍼에서 드라이버 설명을 반환 합니다. \* *DriverAttributes* 버퍼의 드라이버에 대한 추가 정보를 키워드 값 쌍 목록으로 반환합니다. 드라이버의 시스템 정보에 나열된 모든 키워드는 데이터 원본 생성을 요청하는 데 사용되는 **CreateDSN을**제외한 모든 드라이버에 대해 반환되므로 선택 사항입니다. 각 쌍은 null 바이트로 종료되고 전체 목록은 null 바이트로 종료됩니다(즉, 두 개의 null 바이트가 목록의 끝을 표시). 예를 들어 C 구문을 사용하는 파일 기반 드라이버는 다음 특성 목록을 반환할 수 있습니다("\0"은 null 문자를 나타냅니다).  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 \* *DriverAttribute가* 전체 목록을 보유할 만큼 크지 않은 경우 목록이 잘리고 **SQLDriver가** SQLSTATE 01004(데이터 잘린 데이터)를 반환하고 목록의 길이(최종 null-termination 바이트 제외)가 **AttributesLengthPtr에서*반환됩니다.  
  
 드라이버 특성 키워드는 드라이버를 설치할 때 시스템 정보에서 추가됩니다. 자세한 내용은 [ODBC 구성 요소 설치를](../../../odbc/reference/install/installing-odbc-components.md)참조하십시오.  
  
 응용 프로그램은 **SQLDriver를** 여러 번 호출하여 모든 드라이버 설명을 검색할 수 있습니다. 드라이버 관리자는 시스템 정보에서 이 정보를 검색합니다. 드라이버 설명이 더 이상 없는 경우 **SQLDriver는** SQL_NO_DATA 반환합니다. **SQLDriver가** SQL_NO_DATA 반환한 직후 SQL_FETCH_NEXT 함께 호출되면 첫 번째 드라이버 설명이 반환됩니다. 응용 프로그램이 **SQLDriver에서**반환하는 정보를 사용하는 방법에 대한 자세한 내용은 [데이터 원본 또는 드라이버 선택을](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)참조하십시오.  
  
 SQL_FETCH_NEXT 처음 호출될 때 **SQLDriver에** 전달되면 **SQLDriver는** 첫 번째 데이터 원본 이름을 반환합니다.  
  
 **SQLDriver는** 드라이버 관리자에서 구현되므로 특정 드라이버의 표준 준수에 관계없이 모든 드라이버에 대해 지원됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본에 연결하는 데 필요한 값 검색 및 목록 지정|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본 이름 반환|[SQLDataSources 함수](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|연결 문자열 또는 대화 상자를 사용하여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
