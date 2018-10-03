---
title: SQLReadFileDSN 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd56404bfedece75d78ebaabd670cf25f19cbb0d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680231"
---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN 함수
**규칙**  
 ODBC 3.0 버전에 도입 되었습니다.  
  
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
 [입력] .Dsn 파일의 이름을 포함 하는 데이터 버퍼에 대 한 포인터입니다. .Dsn 확장명은.dsn 확장 되지 않은 모든 파일 이름에 추가 됩니다. 값  *\*lpszFileName* null로 끝나는 문자열 이어야 합니다.  
  
 *lpszAppName*  
 [입력] 응용 프로그램의 이름을 포함 하는 데이터 버퍼에 대 한 포인터입니다. 이 "ODBC" ODBC 섹션입니다. 값  *\*lpszAppName* null로 끝나는 문자열 이어야 합니다.  
  
 *lpszkeyname 만들기*  
 [입력] 읽을 키의 이름을 포함 하는 데이터 버퍼에 대 한 포인터입니다. 예약 된 키워드 "설명"을 참조 하십시오. 값  *\*lpszAppName* null로 끝나는 문자열 이어야 합니다.  
  
 *lpszString*  
 [출력] 읽을 키와 연결 된 문자열을 포함 하는 데이터 버퍼에 대 한 포인터입니다.  
  
 경우  *\*lpszFileName* 유효한.dsn 파일 이름이 있지만 *lpszAppName* 인수가 null 포인터 인지 하며 *lpszkeyname 만들기* 인수가 null 포인터 이면  *\*lpszString* 올바른 응용 프로그램의 목록을 포함 합니다. 경우  *\*lpszFileName* 은 유효한.dsn 파일 이름 및  *\*lpszAppName* 유효한 응용 프로그램 이름이 있지만 *lpszkeyname 만들기* 인수가 null 그런 다음 포인터  *\*lpszString* 세미콜론으로 구분 된 DSN 파일의 해당 섹션에서 유효한 예약어 목록을 포함 합니다. 경우  *\*lpszFileName* 유효한.dsn 파일 이름이 있지만  *\*lpszAppName* 가 null 포인터와 *lpszkeyname 만들기* 인수가 null 포인터인 경우 그런 다음  *\*lpszString* 세미콜론으로 구분 된 DSN 파일에서 섹션의 목록을 포함 합니다.  
  
 *cbString*  
 [입력] 길이  *\*lpszString* 버퍼입니다.  
  
 *pcbString*  
 [출력] 반환할 사용 가능한 바이트의 총  *\*lpszString*합니다. 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *cbString*, 출력 문자열  *\*lpszString* 잘립니다 *cbString* 빼기 null 종료 문자입니다. 합니다 *pcbString* 인수로 null 포인터를 사용할 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLReadFileDSN** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|합니다 *lpszString* 인수가 NULL입니다.<br /><br /> 합니다 *cbString* 인수가 0 보다 작습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|에 지정 된 파일 이름의 경로 *lpszFileName* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|*lpszAppName* 인수가 NULL 이면 하는 동안 합니다 *lpszkeyname 만들기* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|출력 문자열 잘림|반환 된 문자열  *\*lpszString* 때문에 잘렸습니다 값 *cbString* 의 값 보다 작거나 되었습니다  *\*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|요청이 실패 했습니다.|키워드 파일 DSN에서에서 존재 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 ODBC 연결 정보를 저장 하는 섹션 이름 [ODBC]를 예약 합니다. 이 섹션에 대 한 예약 된 키워드는 연결 문자열에 대 한 예약 된와 동일 **SQLDriverConnect**합니다. (자세한 내용은 참조는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.)  
  
 응용 프로그램 이러한 예약 된 키워드를 사용 하 여 파일 dsn에서 정보를 읽을 수 있습니다. 응용 프로그램을 호출할 수 있는 파일 DSN과 사용 하 여 연결 된 DSN 없는 연결 문자열 확인 하려는 경우 **SQLReadFileDSN** [ODBC] 섹션에서 예약 된 연결 문자열 키워드 중 하나에 대 한 합니다. DSN가 지정 되지 않은 연결에서 전달 된 전체 연결 문자열에는 모든 [ODBC] 섹션에서 키워드 (예약 된 문자와 드라이버별)의 조합입니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|파일 DSN에 정보 쓰기|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
