---
title: "SQLInstallerError 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLInstallerError
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLInstallerError
helpviewer_keywords: SQLInstallerError [ODBC]
ms.assetid: e6474b79-4d55-458f-81ce-abfafe357f83
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3cdc3ae1e4efe4292077851a4f457bae4af17bd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 함수
**규칙**  
 ODBC 3.0 도입 된 버전:  
  
 **요약**  
 **SQLInstallerError** ODBC 설치 관리자 기능에 대 한 오류 또는 상태 정보를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>인수  
 *iError*  
 [입력] 오류 레코드 수입니다. 유효한 숫자는 1-8입니다.  
  
 *pfErrorCode*  
 [출력] Installer 오류 코드입니다. (자세한 내용은 "설명" 참조)  
  
 *lpszErrorMsg*  
 [출력] 오류 메시지 텍스트에 대 한 저장소에 대 한 포인터입니다.  
  
 *cbErrorMsgMax*  
 [입력] 최대 길이 *szErrorMsg* 버퍼입니다. 이 작거나 null 종결 문자가 뺀 SQL_MAX_MESSAGE_LENGTH 같음 여야 합니다.  
  
 *cbErrorMsgMax*  
 [입력] 최대 길이 *szErrorMsg* 버퍼입니다. 이 작거나 null 종결 문자가 뺀 SQL_MAX_MESSAGE_LENGTH 같음 여야 합니다.  
  
 *pcbErrorMsg*  
 [출력] 바이트 (null 종결 문자 제외)의 총 수에 대 한 포인터를 반환 하려면 사용 가능한 *lpszErrorMsg*합니다. 보다 크거나 반환에 사용할 수 있는 바이트 수가 *cbErrorMsgMax*, 오류 메시지 텍스트에 *lpszErrorMsg* 잘립니다 *cbErrorMsgMax* 빼기는 null 종결 문자 바이트 수입니다. *pcbErrorMsg* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, 또는 SQL_ERROR 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLInstallerError** 자체에 대 한 오류 값을 게시 하지 않습니다. **SQLInstallerError** 오류 정보를 검색할 수 없는 경우 sql_no_data가 반환 (이 경우 *pfErrorCode* 정의 되지 않습니다). 경우 **SQLInstallerError** 일반적으로 SQL_ERROR를 반환 하는 어떤 이유로 오류 값에 액세스할 수 없습니다 **SQLInstallerError** SQL_ERROR를 반환 하지만 모든 오류 값을 게시 하지 않습니다. 경고 문자열의 길이 알지 못하는 경우 (*lpszErrorMsg*)를 설정할 수 있습니다 *lpszErrorMsg* NULL 호출으로 **SQLInstallerError**합니다. **SQLInstallerError** 다음 반환에 경고 문자열의 길이 *cbErrorMsgMax*합니다. 오류 메시지에 대 한 버퍼가 너무 짧은 경우 **SQLInstallerError** SQL_SUCCESS_WITH_INFO를 반환 하 고 올바른 반환 *pfErrorCode* 값에 대 한 **SQLInstallerError**.  
  
 잘림은 오류 메시지에서 발생 했는지를 확인 하려면 응용 프로그램에 값을 비교는 *cbErrorMsgMax* 에 기록 된 메시지 텍스트의 실제 길이 인수는 *pcbErrorMsg* 인수입니다. 에 대 한 올바른 버퍼 길이 할당 해야 하면, *lpszErrorMsg* 및 **SQLInstallerError** 해당와 다시 호출 해야 *iError*레코드입니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램이 호출 **SQLInstallerError** ODBC 설치 관리자 함수에 대 한 이전 호출에서 FALSE를 반환 하는 경우. ODBC 설치 관리자 및 드라이버 또는 변환기 설치 함수는 함수가 실패할 때에 0 개 이상의 오류를 게시할 (FALSE를 반환 합니다). 따라서 응용 프로그램이 호출 **SQLInstallerError** ODBC 설치 관리자 함수 실패 한 후에 합니다.  
  
 ODBC 설치 관리자 오류 큐는 새 설치 관리자 함수를 호출할 때마다가 플러시됩니다. 따라서 응용 프로그램은 마지막 installer 함수 호출에서 아닌 다른 함수에 대 한 오류를 검색할 기대할 수 없습니다.  
  
 함수 호출에 대 한 여러 오류를 검색 하려면 응용 프로그램이 호출 **SQLInstallerError** 여러 번입니다.  
  
 추가 정보가 없는 경우 **SQLInstallerError** 에서 SQL_NO_DATA를 반환 된 *pfErrorCode* 인수는 정의 되지는 *pcbErrorMsg* 인수에 0 및 *lpszErrorMsg* 인수에 단일 null 종결 문자 포함 (하지 않는 한는 *cbErrorMsgMax* 인수는 0).
