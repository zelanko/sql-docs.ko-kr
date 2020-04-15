---
title: SQLReadFileDSN 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abda956ee7682c9ac49270e8bf69fb039641790
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303954"
---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN 함수
**규칙**  
 버전 출시: ODBC 3.0  
  
 **요약**  
 **SQLReadFileDSN은** 파일 DSN의 정보를 읽습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>인수  
 *lpsz파일이름*  
 [입력] .dsn 파일의 이름을 포함하는 데이터 버퍼에 대한 포인터입니다. .dsn 확장은 .dsn 확장명이 없는 모든 파일 이름에 추가됩니다. * \*lpszFileName의* 값은 null-종료된 문자열이어야 합니다.  
  
 *lpszApp이름*  
 [입력] 응용 프로그램의 이름을 포함하는 데이터 버퍼에 대한 포인터입니다. ODBC 섹션의 "ODBC"입니다. * \*lpszAppName의* 값은 null 종료 문자열이어야 합니다.  
  
 *lpszKeyName*  
 [입력] 읽을 키의 이름이 포함된 데이터 버퍼에 대한 포인터입니다. 예약된 키워드는 '댓글'을 참조하세요. * \*lpszAppName의* 값은 null 종료 문자열이어야 합니다.  
  
 *lpszString*  
 [출력] 읽을 키와 연결된 문자열을 포함하는 데이터 버퍼에 대한 포인터입니다.  
  
 * \*lpszFileName이* 유효한 .dsn 파일 이름이지만 *lpszAppName* 인수가 null 포인터이고 *lpszKeyName* 인수가 null 포인터인 경우 * \*lpszString에는* 유효한 응용 프로그램 목록이 포함됩니다. * \*lpszFileName이* 유효한 .dsn 파일 이름이고 * \*lpszAppName이* 유효한 응용 프로그램 이름이지만 *lpszKeyName* 인수가 null 포인터인 경우 * \*lpszString은* 세미콜론으로 구분된 DSN 파일의 해당 섹션에 유효한 예약 된 키워드 목록을 포함합니다. * \*lpszFileName이* 유효한 .dsn 파일 이름이지만 * \*lpszAppName이* null 포인터이고 *lpszKeyName* 인수가 null 포인터인 경우 * \*lpszString은* 세미콜론으로 구분된 DSN 파일의 섹션 목록을 포함합니다.  
  
 *cbString*  
 [입력] * \*lpszString* 버퍼의 길이입니다.  
  
 *pcbString*  
 [출력] * \*lpszString에서*반환할 수 있는 총 바이트 수입니다. 반환할 수 있는 바이트 수가 *cbString보다*크거나 같으면 * \*lpszString의* 출력 문자열은 *cbString에서* null-termination 문자를 뺀 값으로 잘립니다. *pcbString* 인수는 null 포인터일 수 있습니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLReadFileDSN이** FALSE를 반환하는 경우 **SQLInstaller Error**를 호출하여 연결된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못된 버퍼 길이|*lpszString* 인수는 NULL이었습니다.<br /><br /> *cbString* 인수가 0보다 적거나 같습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못된 설치 경로|*lpszFileName* 인수에 지정된 파일 이름의 경로가 잘못되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못된 요청 유형|*lpszAppName* 인수는 NULL이었지만 *lpszKeyName* 인수는 유효합니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|잘린 출력 문자열|*cbString의* 값이 * \*pcbString의*값보다 적거나 같기 때문에 * \*lpszString에서* 반환된 문자열이 잘렸습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청 실패|DSN 파일에 키워드가 없습니다.|  
  
## <a name="comments"></a>주석  
 ODBC는 연결 정보를 저장할 섹션 이름 [ODBC]를 예약합니다. 이 섹션의 예약키워드는 **SQLDriverConnect**에서 연결 문자열에 대해 예약된 키워드와 동일합니다. 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조하십시오.  
  
 응용 프로그램은 이러한 예약된 키워드를 사용하여 파일 DSN의 정보를 읽을 수 있습니다. 응용 프로그램이 파일 DSN과 연결된 DSN 없는 연결 문자열을 찾으려면 [ODBC] 섹션에서 예약된 연결 문자열 키워드에 대해 **SQLReadFileDSN을** 호출할 수 있습니다. DSN이 없는 연결에서 전달되는 전체 연결 문자열은 [ODBC] 섹션의 모든 키워드(예약 및 드라이버별)의 조합입니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|파일 DSN에 정보 작성|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
