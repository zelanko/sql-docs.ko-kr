---
title: SQLWriteFileDSN 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8b1ce34074a2326d17a199537b308a9a670d8163
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039436"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 함수
**규칙**  
 소개 된 버전: ODBC 3.0  
  
 **요약**  
 **Sqlwritefiledsn** 은 파일 DSN에 정보를 씁니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>인수  
 *lpszFileName*  
 입력 파일 DSN의 이름에 대 한 포인터입니다. Dsn 확장이 아직 없는 모든 파일 이름에 DSN 확장이 추가 됩니다.  
  
 *lpszAppName*  
 입력 응용 프로그램의 이름에 대 한 포인터입니다. ODBC 섹션에 대 한 "ODBC"입니다.  
  
 *lpszKeyName*  
 입력 읽을 키의 이름에 대 한 포인터입니다. 예약 된 키워드는 "Comments"를 참조 하십시오.  
  
 *lpszString*  
 출력 쓸 키와 연결 된 문자열을 가리킵니다. 이 인수에 의해 가리키는 문자열의 최대 길이는 32767 바이트입니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlwritefiledsn** 이 FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 연결 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|*LpszFileName* 인수에 지정 된 파일 이름의 경로가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못 된 요청 유형|*LpszAppName*, *lpszKeyName*또는 *lpszString* 인수가 NULL입니다.|  
  
## <a name="comments"></a>주석  
 ODBC는 연결 정보를 저장할 섹션 이름 [ODBC]를 예약 합니다. 이 섹션에 대 한 예약 된 키워드는 **SQLDriverConnect**의 연결 문자열에 예약 된 키워드와 동일 합니다. 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조 하세요.  
  
 응용 프로그램은 이러한 예약 키워드를 사용 하 여 파일 DSN에 직접 정보를 쓸 수 있습니다. 응용 프로그램에서 파일 DSN과 연결 된 DSN 없는 연결 문자열을 만들거나 수정 하려는 경우 [ODBC] 섹션의 예약 된 연결 문자열 키워드에 대해 **Sqlwritefiledsn** 을 호출할 수 있습니다.  
  
 *LpszString* 인수가 null 포인터인 경우 *lpszKeyName* 인수에서 가리키는 키워드가 dsn 파일에서 삭제 됩니다. *LpszString* 및 *lpszKeyName* 인수가 모두 null 포인터인 경우 *lpszAppName* 인수에 의해 가리키는 섹션이 dsn 파일에서 삭제 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|파일 Dsn에서 정보 읽기|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
