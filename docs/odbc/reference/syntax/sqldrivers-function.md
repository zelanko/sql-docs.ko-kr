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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104659"
---
# <a name="sqldrivers-function"></a>SQLDrivers 함수
**규칙**  
 소개 된 버전: ODBC 2.0 표준 준수: ODBC  
  
 **요약**  
 **Sqldrivers** 는 드라이버 설명 및 드라이버 특성 키워드를 나열 합니다. 이 함수는 드라이버 관리자만 구현 합니다.  
  
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
 입력 환경 핸들.  
  
 *방향도*  
 입력 드라이버 관리자가 목록에서 다음 드라이버 설명 (SQL_FETCH_NEXT)을 페치 하는지 또는 목록의 처음부터 검색을 시작할지 (SQL_FETCH_FIRST)를 결정 합니다.  
  
 *DriverDescription*  
 출력 드라이버 설명을 반환할 버퍼에 대 한 포인터입니다.  
  
 *Driverdescription* 이 NULL 인 경우 *DescriptionLengthPtr* 는 *driverdescription*이 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 문자 데이터의 NULL 종료 문자를 제외 하 고 전체 문자 수를 반환 합니다.  
  
 *BufferLength1*  
 입력 **Driverdescription* 버퍼의 길이 (문자)입니다.  
  
 *DescriptionLengthPtr*  
 출력 \* *Driverdescription*에서 반환 하는 데 사용할 수 있는 총 문자 수 (null 종결 문자 제외)를 반환할 버퍼에 대 한 포인터입니다. 반환할 수 있는 문자 수가 *BufferLength1*보다 크거나 같으면 \* *driverdescription* 의 드라이버 설명이 *BufferLength1* 로 잘리고 null 종료 문자의 길이를 뺀 값입니다.  
  
 *DriverAttributes*  
 출력 드라이버 특성 값 쌍의 목록을 반환할 버퍼에 대 한 포인터입니다 ("Comments" 참조).  
  
 *Driverattributes* 가 NULL 인 경우 *AttributesLengthPtr* 는 *driverattributes*가 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 총 바이트 수 (문자 데이터의 NULL 종료 문자 제외)를 반환 합니다.  
  
 *BufferLength2*  
 입력 \* *Driverattributes* 버퍼의 길이 (문자)입니다. Driverdescription 값이 유니코드 문자열이 면 ( **sqldriversw**호출 시) *bufferlength* 인수는 짝수 여야 합니다. * \**  
  
 *AttributesLengthPtr*  
 출력 \* *Driverattributes*에서 반환 하는 데 사용할 수 있는 총 바이트 수 (null 종결 바이트 제외)를 반환할 버퍼에 대 한 포인터입니다. 반환 하는 데 사용할 수 있는 바이트 수가 *BufferLength2*보다 크거나 같으면 \* *driverattributes* 의 특성 값 쌍 목록이 *BufferLength2* 로 잘리고 null 종료 문자의 길이를 뺀 값입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqldrivers** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_ENV의 *HandleType* 및 *EnvironmentHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **Sqldrivers** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|(DM) 드라이버 관리자 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|(DM) 버퍼 \* *driverdescription* 의 크기가 작아 전체 드라이버 설명을 반환할 수 없습니다. 따라서 설명이 잘렸습니다. 전체 드라이버 설명의 길이는 \* *DescriptionLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.<br /><br /> (DM) 버퍼 \* *driverattributes* 의 크기가 작아 특성 값 쌍의 전체 목록을 반환할 수 없습니다. 따라서 목록이 잘렸습니다. 특성 값 쌍의 잘린 잘림 목록 길이는 **AttributesLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|(DM) 드라이버 관리자가 함수의 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *BufferLength1* 에 지정 된 값이 0 보다 작은 경우<br /><br /> (DM) 인수 *BufferLength2* 에 지정 된 값이 0 보다 작거나 1과 같습니다.|  
|HY103|잘못 된 검색 코드|(DM) 인수 *방향* 에 지정 된 값이 SQL_FETCH_FIRST 또는 SQL_FETCH_NEXT와 같지 않습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
  
## <a name="comments"></a>주석  
 **Sqldrivers** \* *는 드라이버 설명 버퍼에* 드라이버 설명을 반환 합니다. \* *Driverattributes* 버퍼의 드라이버에 대 한 추가 정보를 키워드-값 쌍의 목록으로 반환 합니다. 데이터 원본 만들기를 묻는 메시지를 표시 하는 데 사용 되는 **CreateDSN**를 제외 하 고 모든 드라이버에 대해 드라이버에 대 한 시스템 정보에 나열 된 모든 키워드가 반환 됩니다 .이는 선택 사항입니다. 각 쌍은 null 바이트로 종료 되 고 전체 목록은 null 바이트로 종료 됩니다. 즉, 두 개의 null 바이트는 목록의 끝을 표시 합니다. 예를 들어 C 구문을 사용 하는 파일 기반 드라이버는 다음 특성 목록을 반환할 수 있습니다 ("\ 0"은 null 문자를 나타냄).  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 \* *Driverattributes* 가 전체 목록을 저장 하기에 충분히 크지 않은 경우 목록은 잘립니다. **sqldrivers** 는 SQLSTATE 01004 (데이터 잘림)을 반환 하 고 목록의 길이 (마지막 null 종결 바이트 제외)는 **AttributesLengthPtr*에 반환 됩니다.  
  
 드라이버 특성 키워드는 드라이버를 설치할 때 시스템 정보에서 추가 됩니다. 자세한 내용은 [ODBC 구성 요소 설치](../../../odbc/reference/install/installing-odbc-components.md)를 참조 하세요.  
  
 응용 프로그램은 **Sqldrivers** 를 여러 번 호출 하 여 모든 드라이버 설명을 검색할 수 있습니다. 드라이버 관리자는 시스템 정보에서이 정보를 검색 합니다. 드라이버 설명이 더 이상 없는 경우 **sqldrivers** 는 SQL_NO_DATA을 반환 합니다. SQL_NO_DATA 반환 된 후 즉시 SQL_FETCH_NEXT를 사용 하 여 **sqldrivers** 를 호출 하는 경우 첫 번째 드라이버 설명을 반환 합니다. 응용 프로그램이 **Sqldrivers**에서 반환 하는 정보를 사용 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)을 참조 하세요.  
  
 SQL_FETCH_NEXT 처음 호출 될 때 **sqldrivers** 에 전달 되는 경우 **sqldrivers** 는 첫 번째 데이터 원본 이름을 반환 합니다.  
  
 **Sqldrivers** 는 드라이버 관리자에서 구현 되므로 특정 드라이버의 표준 준수에 관계 없이 모든 드라이버에 대해 지원 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 원본에 연결 하는 데 필요한 값 검색 및 나열|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|데이터 원본 이름 반환|[SQLDataSources 함수](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수(SQLDriverConnect Function)](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
