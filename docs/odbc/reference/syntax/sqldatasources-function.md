---
description: SQLDataSources 함수
title: SQLDataSources 원본 함수 | Microsoft Docs
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
ms.openlocfilehash: bcf57779916b7a9d3189a5ce37b8603e5da5cb74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461185"
---
# <a name="sqldatasources-function"></a>SQLDataSources 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqldatasources** 원본은 데이터 원본에 대 한 정보를 반환 합니다. 이 함수는 드라이버 관리자만 구현 합니다.  
  
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
 *EnvironmentHandle*  
 입력 환경 핸들.  
  
 *Direction*  
 입력 드라이버 관리자가 정보를 반환 하는 데이터 원본을 결정 합니다. 다음 값 중 하나일 수 있습니다.  
  
 SQL_FETCH_NEXT (목록에서 다음 데이터 원본 이름을 페치) SQL_FETCH_FIRST (목록의 시작 부분에서 인출 하려면) SQL_FETCH_FIRST_USER (첫 번째 사용자 DSN을 페치 하려면) 또는 SQL_FETCH_FIRST_SYSTEM (첫 번째 시스템 DSN 페치)를 사용 합니다.  
  
 *Direction* 이 SQL_FETCH_FIRST로 설정 된 경우 *방향이* SQL_FETCH_NEXT로 설정 된 **sqldatasources 원본** 에 대 한 후속 호출은 사용자 및 시스템 dsn을 모두 반환 합니다. *Direction* 이 SQL_FETCH_FIRST_USER로 설정 된 경우 *방향이* SQL_FETCH_NEXT로 설정 된 **sqldatasources** 의 모든 후속 호출은 사용자 dsn만 반환 합니다. *Direction* 이 SQL_FETCH_FIRST_SYSTEM로 설정 된 경우 *방향이* SQL_FETCH_NEXT로 설정 된 **sqldatasources 원본** 에 대 한 모든 후속 호출은 시스템 dsn만 반환 합니다.  
  
 *데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면*  
 출력 데이터 소스 이름을 반환할 버퍼에 대 한 포인터입니다.  
  
 *Servername* 이 NULL 인 경우 *NameLength1Ptr* 는 *servername*이 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 문자 데이터의 NULL 종료 문자를 제외한 총 문자 수를 반환 합니다.  
  
 *BufferLength1*  
 입력 **ServerName* 버퍼의 길이 (문자)입니다. 이는 SQL_MAX_DSN_LENGTH 및 null 종료 문자 보다 길 필요가 없습니다.  
  
 *NameLength1Ptr*  
 출력 ServerName에서 반환 하는 데 사용할 수 있는 총 문자 수 (null 종결 문자 제외)를 반환할 버퍼에 대 한 포인터 \* *ServerName*입니다. 반환할 수 있는 문자 수가 *BufferLength1*보다 크거나 같으면 ServerName의 데이터 원본 이름이 \* *ServerName* *BufferLength1* 로 잘리고 null 종료 문자의 길이를 뺀 값입니다.  
  
 *설명*  
 출력 데이터 원본과 연결 된 드라이버에 대 한 설명을 반환할 버퍼에 대 한 포인터입니다. 예를 들어 dBASE 또는 SQL Server입니다.  
  
 *Description* 이 NULL 인 경우 *NameLength2Ptr* 는 *설명*에 의해 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 문자 데이터의 NULL 종료 문자를 제외 하 고 전체 문자 수를 반환 합니다.  
  
 *BufferLength2*  
 입력 **설명* 버퍼의 문자 길이입니다.  
  
 *NameLength2Ptr*  
 출력 설명에서 반환 하는 데 사용할 수 있는 전체 문자 수 (null 종결 문자 제외)를 반환할 버퍼에 대 한 포인터 \* *Description*입니다. 반환할 수 있는 문자 수가 *BufferLength2*보다 크거나 같으면 설명의 드라이버 설명이 \* *Description* *BufferLength2* 로 잘리고 null 종료 문자의 길이를 뺀 값입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqldatasources** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_ENV의 *HandleType* 및 *EnvironmentHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **Sqldatasources 원본** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|(DM) 드라이버 관리자 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|(DM) 버퍼 \* *ServerName* 이 전체 데이터 소스 이름을 반환할 만큼 크지 않습니다. 따라서 이름이 잘렸습니다. 전체 데이터 원본 이름의 길이가 NameLength1Ptr에서 반환 됩니다 \* *NameLength1Ptr*. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.<br /><br /> (DM) 버퍼 \* *설명이* 충분 하지 않아 전체 드라이버 설명을 반환할 수 없습니다. 따라서 설명이 잘렸습니다. 잘린 데이터 원본 설명의 길이는 **NameLength2Ptr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|HY000|일반 오류|(DM) 특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|(DM) 드라이버 관리자가 함수의 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *BufferLength1* 에 지정 된 값이 0 보다 작은 경우<br /><br /> (DM) 인수 *BufferLength2* 에 지정 된 값이 0 보다 작은 경우|  
|HY103|잘못 된 검색 코드|(DM) 인수 *방향* 에 지정 된 값이 SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM 또는 SQL_FETCH_NEXT와 같지 않습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
  
## <a name="comments"></a>주석  
 **Sqldatasources 원본은** 드라이버 관리자에서 구현 되므로 특정 드라이버의 표준 준수에 관계 없이 모든 드라이버에 대해 지원 됩니다.  
  
 응용 프로그램은 **sqldatasources** 소스를 여러 번 호출 하 여 모든 데이터 소스 이름을 검색할 수 있습니다. 드라이버 관리자는 시스템 정보에서이 정보를 검색 합니다. 더 이상 데이터 원본 이름이 없으면 드라이버 관리자는 SQL_NO_DATA를 반환 합니다. SQL_NO_DATA 반환 된 후 즉시 SQL_FETCH_NEXT를 사용 하 여 **sqldatasources** 원본을 호출 하는 경우 첫 번째 데이터 원본 이름을 반환 합니다. 응용 프로그램에서 **Sqldatasources**원본에 의해 반환 되는 정보를 사용 하는 방법에 대 한 자세한 내용은 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)을 참조 하십시오.  
  
 SQL_FETCH_NEXT 처음 호출 될 때 **sqldatasources** 원본에 전달 되는 경우 첫 번째 데이터 원본 이름이 반환 됩니다.  
  
 드라이버는 데이터 원본 이름이 실제 데이터 원본에 매핑되는 방식을 결정 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 원본에 연결 하는 데 필요한 값 검색 및 나열|[SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|데이터 원본에 연결|[SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|드라이버 설명 및 특성 반환|[SQLDrivers 함수](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
