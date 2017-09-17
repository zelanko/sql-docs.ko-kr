---
title: "SQLReadFileDSN 함수 | Microsoft Docs"
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
- SQLReadFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLReadFileDSN
helpviewer_keywords:
- SQLReadFileDSN function [ODBC]
ms.assetid: ead464aa-cdc3-47dd-a0c0-997711205d31
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f3d74f900de16f8b2b257d9af6c65e8745139d3c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN 함수
**규칙**  
 ODBC 3.0 도입 된 버전:  
  
 **요약**  
 **SQLReadFileDSN** 파일 DSN에서 정보를 읽습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>인수  
 *lpszFileName*  
 [입력] .Dsn 파일의 이름이 포함 된 데이터 버퍼에 대 한 포인터입니다. .Dsn 확장.dsn 확장 아직 없는 모든 파일 이름에 추가 됩니다. 값 * \*lpszFileName* null로 끝나는 문자열 이어야 합니다.  
  
 *lpszAppName*  
 [입력] 응용 프로그램의 이름이 포함 된 데이터 버퍼에 대 한 포인터입니다. 이것이 ODBC 섹션에 대 한 "ODBC"입니다. 값 * \*lpszAppName* null로 끝나는 문자열 이어야 합니다.  
  
 *lpszkeyname 만들기*  
 [입력] 키를 읽을 수의 이름이 포함 된 데이터 버퍼에 대 한 포인터입니다. 예약 된 키워드 "설명"을 참조 하십시오. 값 * \*lpszAppName* null로 끝나는 문자열 이어야 합니다.  
  
 *lpszString*  
 [출력] 키를 읽을 수와 관련 된 문자열이 포함 된 데이터 버퍼에 대 한 포인터입니다.  
  
 경우 * \*lpszFileName* 는 유효한.dsn 파일 이름 이지만 *lpszAppName* 인수는 null 포인터 및 *lpszkeyname 만들기* 인수는 null 포인터 이면 다음 * \*lpszString* 유효한 응용 프로그램의 목록을 포함 합니다. 경우 * \*lpszFileName* 는 유효한.dsn 파일 이름 및 * \*lpszAppName* 은 올바른 응용 프로그램 이름 이지만 *lpszkeyname 만들기* 인수는 null 다음 포인터 * \*lpszString* 세미콜론으로 구분 된 DSN 파일의 해당 섹션에서 유효한 예약 된 키워드 목록을 포함 합니다. 경우 * \*lpszFileName* 유효한.dsn 파일 이름인 하지만 * \*lpszAppName* 가 null 포인터 및 *lpszkeyname 만들기* 인수는 null 포인터 그런 다음 * \*lpszString* 세미콜론으로 구분 된 DSN 파일에서 섹션의 목록을 포함 합니다.  
  
 *cbString*  
 [입력] 길이 * \*lpszString* 버퍼입니다.  
  
 *pcbString*  
 [출력] 반환 하려면 사용 가능한 바이트의 총 수 * \*lpszString*합니다. 보다 크거나 반환에 사용할 수 있는 바이트 수가 *cbString*의 출력 문자열 * \*lpszString* 잘립니다 *cbString* 빼기 null 종료 문자입니다. *pcbString* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLReadFileDSN** 관련 FALSE를 반환 * \*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에 * \*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*lpszString* 에 NULL 인수가 있습니다.<br /><br /> *cbString* 0 보다 작거나 같은 인수 했습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|에 지정 된 파일 이름의 경로 *lpszFileName* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|*lpszAppName* 에 NULL 인수가 동안는 *lpszkeyname 만들기* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|출력 문자열 잘림|반환 되는 문자열 * \*lpszString* 때문에 잘렸습니다 값 *cbString* 값 보다 작습니다 * \*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|요청이 실패 했습니다.|키워드 파일 DSN에에서 존재 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 ODBC 연결 정보를 저장 하는 섹션 이름 [ODBC]가 보유 합니다. 이 섹션에 대 한 예약 된 키워드에서 연결 문자열에 대 한 예약 된 것으로 동일 **SQLDriverConnect**합니다. (자세한 내용은 참조는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.)  
  
 응용 프로그램 이러한 예약 된 키워드를 사용 하 여 파일 DSN의 정보를 읽을 수 있습니다. 응용 프로그램에서 호출할 수 있는 파일 DSN와 관련 된 DSN 없는 연결 문자열 확인 하려는 경우 **SQLReadFileDSN** [ODBC] 섹션에서 예약 된 연결 문자열 키워드에 대 한 합니다. DSN 없는 연결 되는 전체 연결 문자열은 키워드 (예약 된 문자와 드라이버별) [ODBC] 섹션에 있는 모든의 조합입니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|파일 DSN에 정보를 기록|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
