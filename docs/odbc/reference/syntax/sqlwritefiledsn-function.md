---
title: SQLWriteFileDSN 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteFileDSN
helpviewer_keywords:
- SQLWriteFileDSN [ODBC]
ms.assetid: 9e18f56f-1061-416b-83d4-ffeec42ab5a9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e781f1be79e0079f33b3d0800c665f5f5e9fda4d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286893"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 함수
**규칙**  
 버전 출시: ODBC 3.0  
  
 **요약**  
 **SQLWriteFileDSN은** 파일 DSN에 정보를 씁니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>인수  
 *lpsz파일이름*  
 [입력] 파일 DSN의 이름에 대한 포인터입니다. DSN 확장은 DSN 확장명이 없는 모든 파일 이름에 추가됩니다.  
  
 *lpszApp이름*  
 [입력] 응용 프로그램의 이름에 대한 포인터입니다. ODBC 섹션의 "ODBC"입니다.  
  
 *lpszKeyName*  
 [입력] 읽을 키의 이름에 대한 포인터입니다. 예약된 키워드는 '댓글'을 참조하세요.  
  
 *lpszString*  
 [출력] 쓸 키와 연결된 문자열을 가리켰습니다. 이 인수로 가리키는 문자열의 최대 길이는 32,767바이트입니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLWriteFileDSN이** FALSE를 반환하는 경우 **SQLInstaller Error**를 호출하여 연결된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못된 설치 경로|*lpszFileName* 인수에 지정된 파일 이름의 경로가 잘못되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못된 요청 유형|*lpszAppName,* *lpszKeyName*또는 *lpszString* 인수는 NULL이었습니다.|  
  
## <a name="comments"></a>주석  
 ODBC는 연결 정보를 저장할 섹션 이름 [ODBC]를 예약합니다. 이 섹션의 예약키워드는 **SQLDriverConnect**에서 연결 문자열에 대해 예약된 키워드와 동일합니다. 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조하십시오.  
  
 응용 프로그램은 이러한 예약된 키워드를 사용하여 파일 DSN에 직접 정보를 쓸 수 있습니다. 응용 프로그램이 파일 DSN과 연결된 DSN 없는 연결 문자열을 만들거나 수정하려는 경우 [ODBC] 섹션에서 예약된 연결 문자열 키워드에 대해 **SQLWriteFileDSN을** 호출할 수 있습니다.  
  
 *lpszString* 인수가 null 포인터인 경우 *lpszKeyName* 인수가 가리키는 키워드는 .dsn 파일에서 삭제됩니다. *lpszString* 및 *lpszKeyName* 인수가 모두 null 포인터인 경우 *lpszAppName* 인수가 가리키는 섹션은 .dsn 파일에서 삭제됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|파일 DSN의 정보 읽기|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
