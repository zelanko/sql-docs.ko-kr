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
manager: craigg
ms.openlocfilehash: 58002ec0e8ceacae49f4d54be5d3406ea3014d59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536777"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 함수
**규칙**  
 도입 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLWriteFileDSN** 파일 DSN에 정보를 씁니다.  
  
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
 [입력] 파일 DSN의 이름에 대 한 포인터입니다. DSN 확장 DSN 확장 되지 않은 모든 파일 이름에 추가 됩니다.  
  
 *lpszAppName*  
 [입력] 응용 프로그램의 이름에 대 한 포인터입니다. 이 "ODBC" ODBC 섹션입니다.  
  
 *lpszKeyName*  
 [입력] 읽을 키의 이름에 대 한 포인터입니다. 예약 된 키워드 "설명"을 참조 하십시오.  
  
 *lpszString*  
 [출력] 쓸 키와 연결 된 문자열을 가리킵니다. 이 인수에서 가리키는 문자열의 최대 길이 32,767 바이트입니다.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLWriteFileDSN** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|에 지정 된 파일 이름의 경로 *lpszFileName* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|합니다 *lpszAppName*를 *lpszkeyname 만들기*, 또는 *lpszString* 인수가 NULL입니다.|  
  
## <a name="comments"></a>주석  
 ODBC 연결 정보를 저장 하는 섹션 이름 [ODBC]를 예약 합니다. 이 섹션에 대 한 예약 된 키워드는 연결 문자열에 대 한 예약 된와 동일 **SQLDriverConnect**합니다. (자세한 내용은 참조는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.)  
  
 응용 프로그램 이러한 예약 된 키워드를 사용 하 여 파일 DSN에 직접 정보를 쓸 수 있습니다. 응용 프로그램 만들기 또는 파일 DSN과 사용 하 여 연결 된 DSN 없는 연결 문자열을 수정 하려는 호출할 수 있습니다 **SQLWriteFileDSN** [ODBC] 섹션에서 예약 된 연결 문자열 키워드 중 하나에 대 한 합니다.  
  
 경우는 *lpszString* 인수가 null 포인터에서 가리키는 키워드는 *lpszkeyname 만들기* 인수.dsn 파일에서 삭제 됩니다. 경우는 *lpszString* 하 고 *lpszkeyname 만들기* 인수는 모두 null 포인터에서 가리키는 섹션의 *lpszAppName* 인수.dsn 파일에서 삭제 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|파일 Dsn에서 정보를 읽는|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
