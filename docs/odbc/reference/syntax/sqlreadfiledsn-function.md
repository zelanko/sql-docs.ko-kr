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
ms.openlocfilehash: ad1e3dc4901fc7251528e6040b9250469f8fef6c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053660"
---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN 함수
**규칙**  
 소개 된 버전: ODBC 3.0  
  
 **요약**  
 **Sqlreadfiledsn** 은 파일 DSN에서 정보를 읽습니다.  
  
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
 *lpszFileName*  
 입력 Dsn 파일의 이름을 포함 하는 데이터 버퍼에 대 한 포인터입니다. . Dsn 확장명은 아직 확장명이 없는 모든 파일 이름에 추가 됩니다. * \*LpszFileName* 의 값은 null로 끝나는 문자열 이어야 합니다.  
  
 *lpszAppName*  
 입력 응용 프로그램의 이름을 포함 하는 데이터 버퍼에 대 한 포인터입니다. ODBC 섹션에 대 한 "ODBC"입니다. * \*LpszAppName* 의 값은 null로 끝나는 문자열 이어야 합니다.  
  
 *lpszKeyName*  
 입력 읽을 키의 이름을 포함 하는 데이터 버퍼에 대 한 포인터입니다. 예약 된 키워드는 "Comments"를 참조 하십시오. * \*LpszAppName* 의 값은 null로 끝나는 문자열 이어야 합니다.  
  
 *lpszString*  
 출력 읽을 키와 연결 된 문자열을 포함 하는 데이터 버퍼에 대 한 포인터입니다.  
  
 * \*LpszFileName* 이 유효한 dsn 파일 이름 이지만 *lpszAppName* 인수가 null 포인터이 고 *lpszKeyName* 인수가 null 포인터인 경우 * \*lpszString* 에는 유효한 응용 프로그램 목록이 포함 됩니다. * \*LpszFileName* 이 유효한 dsn 파일 이름이 고 * \*lpszAppName* 가 유효한 응용 프로그램 이름 이지만 *lpszKeyName* 인수가 null 포인터인 경우 * \*lpszString* 는 dsn 파일의 해당 섹션에서 세미콜론으로 구분 된 올바른 예약 키워드 목록을 포함 합니다. * \*LpszFileName* 가 유효한. i n t 파일 이름 이지만 * \*lpszAppName* 가 null 포인터이 고 *lpszKeyName* 인수가 null 포인터인 경우 * \*lpszString* 는 dsn 파일의 섹션 목록을 세미콜론으로 구분 하 여 포함 합니다.  
  
 *cbString*  
 입력 LpszString 버퍼의 길이입니다. * \**  
  
 *pcbString*  
 출력 * \*LpszString*에서 반환할 수 있는 총 바이트 수입니다. 반환할 수 있는 바이트 수가 *cbstring*보다 크거나 같으면 * \*lpszString* 의 출력 문자열이 *cbstring* 에서 null 종료 문자를 뺀 값으로 잘립니다. *Pcbstring* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlreadfiledsn** 이 FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*LpszString* 인수가 NULL입니다.<br /><br /> *Cbstring* 인수가 0 보다 작거나 같습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|*LpszFileName* 인수에 지정 된 파일 이름의 경로가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못 된 요청 유형|*LpszAppName* 인수가 NULL 이지만 *lpszKeyName* 인수가 유효 합니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|출력 문자열이 잘렸습니다.|*Cbstring* 의 값이 * \*pcbstring*의 값 보다 작거나 같으므로 * \*lpszString* 에 반환 된 문자열이 잘렸습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청 실패|키워드가 파일 DSN에 없습니다.|  
  
## <a name="comments"></a>주석  
 ODBC는 연결 정보를 저장할 섹션 이름 [ODBC]를 예약 합니다. 이 섹션에 대 한 예약 된 키워드는 **SQLDriverConnect**의 연결 문자열에 예약 된 키워드와 동일 합니다. 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조 하세요.  
  
 응용 프로그램은 이러한 예약 키워드를 사용 하 여 파일 DSN의 정보를 읽을 수 있습니다. 응용 프로그램에서 파일 DSN과 연결 된 DSN 없는 연결 문자열을 확인 하려는 경우 [ODBC] 섹션의 예약 된 연결 문자열 키워드에 대해 **Sqlreadfiledsn** 을 호출할 수 있습니다. DSN 없는 연결로 전달 되는 전체 연결 문자열은 [ODBC] 섹션의 모든 키워드 (예약 된 드라이버와 드라이버 관련)의 조합입니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|파일 DSN에 정보 쓰기|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
