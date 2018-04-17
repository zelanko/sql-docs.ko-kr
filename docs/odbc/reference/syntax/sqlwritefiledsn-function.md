---
title: SQLWriteFileDSN 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2984c14d1a3fd7f912ca3e71ba33f05e92fe2061
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 함수
**규칙**  
 ODBC 3.0 도입 된 버전:  
  
 **요약**  
 **SQLWriteFileDSN** 파일 DSN에 정보를 씁니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>인수  
 *lpszFileName*  
 [입력] 파일 DSN의 이름에 대 한 포인터입니다. DSN 확장 아직 없는 모든 파일 이름에는 DSN 확장명이 추가 됩니다.  
  
 *lpszAppName*  
 [입력] 응용 프로그램의 이름에 대 한 포인터입니다. 이것이 ODBC 섹션에 대 한 "ODBC"입니다.  
  
 *lpszkeyname 만들기*  
 [입력] 키를 읽을 수의 이름에 대 한 포인터입니다. 예약 된 키워드 "설명"을 참조 하십시오.  
  
 *lpszString*  
 [출력] 쓸 키와 연결 된 문자열을 가리키는입니다. 이 인수에서 가리키는 문자열의 최대 길이 32, 767 바이트입니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLWriteFileDSN** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|에 지정 된 파일 이름의 경로 *lpszFileName* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|*lpszAppName*, *lpszkeyname 만들기*, 또는 *lpszString* 에 NULL 인수가 있습니다.|  
  
## <a name="comments"></a>설명  
 ODBC 연결 정보를 저장 하는 섹션 이름 [ODBC]가 보유 합니다. 이 섹션에 대 한 예약 된 키워드에서 연결 문자열에 대 한 예약 된 것으로 동일 **SQLDriverConnect**합니다. (자세한 내용은 참조는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.)  
  
 응용 프로그램 파일 DSN에 직접 정보를 기록 이러한 예약 된 키워드를 사용할 수 있습니다. 에서 응용 프로그램을 만들거나 파일 DSN와 관련 된 DSN 없는 연결 문자열을 수정 하려는 경우 호출할 수 **SQLWriteFileDSN** [ODBC] 섹션에서 예약 된 연결 문자열 키워드에 대 한 합니다.  
  
 경우는 *lpszString* 인수는 null 포인터에서 가리키는 키워드는 *lpszkeyname 만들기* 인수.dsn 파일에서 삭제 됩니다. 경우는 *lpszString* 및 *lpszkeyname 만들기* 인수는 모두 null 포인터에서 가리키는 섹션은 *lpszAppName* 인수.dsn 파일에서 삭제 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|파일 Dsn에서 정보를 읽는|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
