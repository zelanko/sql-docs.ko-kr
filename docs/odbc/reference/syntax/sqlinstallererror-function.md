---
title: SQLInstallerError 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallerError
helpviewer_keywords:
- SQLInstallerError [ODBC]
ms.assetid: e6474b79-4d55-458f-81ce-abfafe357f83
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0ae475ba4dc290f57eadf94d1e45e8a203a7ce5
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536593"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 함수
**규칙**  
 도입 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLInstallerError** ODBC 설치 관리자 기능에 대 한 오류 또는 상태 정보를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>인수  
 *iError*  
 [입력] 오류 레코드 수입니다. 1에서 8 사이의 유효한 숫자는입니다.  
  
 *pfErrorCode*  
 [출력] 설치 관리자 오류 코드입니다. (자세한 내용은 "설명입니다." 참조)  
  
 *lpszErrorMsg*  
 [출력] 오류 메시지 텍스트에 대 한 저장소에 대 한 포인터입니다.  
  
 *cbErrorMsgMax*  
 [입력] 최대 길이 *szErrorMsg* 버퍼입니다. 이 작아야 보다 크거나 SQL_MAX_MESSAGE_LENGTH null 종결 문자가 뺀 값입니다.  
  
 *cbErrorMsgMax*  
 [입력] 최대 길이 *szErrorMsg* 버퍼입니다. 이 작아야 보다 크거나 SQL_MAX_MESSAGE_LENGTH null 종결 문자가 뺀 값입니다.  
  
 *pcbErrorMsg*  
 [출력] 총 바이트 (null 종결 문자가 제외)에 대 한 포인터를 반환 하려면 사용 가능한 *lpszErrorMsg*합니다. 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *cbErrorMsgMax*에서 오류 메시지 텍스트 *lpszErrorMsg* 잘립니다 *cbErrorMsgMax* 빼기는 null 종결 문자 바이트 수입니다. 합니다 *pcbErrorMsg* 인수로 null 포인터를 사용할 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, 또는 SQL_ERROR  
  
## <a name="diagnostics"></a>진단  
 **SQLInstallerError** 자체에 대 한 오류 값을 게시 하지 않습니다. **SQLInstallerError** 오류 정보를 검색할 수 없는 경우에 SQL_NO_DATA를 반환 합니다 (이 예제의 *pfErrorCode* 정의 되지 않습니다). 하는 경우 **SQLInstallerError** 일반적으로 SQL_ERROR를 반환 하는 어떤 이유로 오류 값에 액세스할 수 없습니다 **SQLInstallerError** SQL_ERROR를 반환 하지만 오류 값을 게시 하지 않습니다. 경고 문자열의 길이 알지 못하는 경우 (*lpszErrorMsg*)를 설정할 수 있습니다 *lpszErrorMsg* NULL 및 호출 **SQLInstallerError**합니다. **SQLInstallerError** 에 경고 문자열의 길이 반환 합니다 *cbErrorMsgMax*합니다. 오류 메시지에 대 한 버퍼 너무 짧으면 **SQLInstallerError** SQL_SUCCESS_WITH_INFO를 반환 하 고 올바른 반환 *pfErrorCode* 값 **SQLInstallerError**.  
  
 오류 메시지에서 잘림이 발생 했는지를 확인 하려면 응용 프로그램에서 값을 비교 합니다 *cbErrorMsgMax* 에 기록 된 메시지 텍스트의 실제 길이 인수를 *pcbErrorMsg* 인수입니다. 잘림이 발생할 경우 올바른 버퍼 길이 할당 해야 *lpszErrorMsg* 하 고 **SQLInstallerError** 사용 하 여 해당 다시 호출 해야 *iError*레코드입니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램 호출 **SQLInstallerError** ODBC 설치 관리자 함수에 대 한 이전 호출에서 FALSE를 반환 하는 경우. ODBC 및 드라이버 관리자나 translator 설치 함수는 함수가 실패 하는 경우에 0 개 이상의 오류를 게시할 (FALSE를 반환 합니다). 따라서 응용 프로그램 호출 **SQLInstallerError** ODBC 설치 관리자 함수 실패 후에 합니다.  
  
 ODBC 설치 관리자 오류 큐는 새 설치 관리자 함수를 호출할 때마다가 플러시됩니다. 따라서 응용 프로그램은 마지막 installer 함수 호출에서 다른 함수에 대 한 오류를 검색할 기대할 수 없습니다.  
  
 함수 호출에 대 한 여러 오류를 검색 하려면 응용 프로그램 호출 **SQLInstallerError** 여러 번입니다.  
  
 추가 정보가 없는 경우 **SQLInstallerError** 에서 SQL_NO_DATA를 반환 합니다 *pfErrorCode* 인수 정의 되어 있지는 *pcbErrorMsg* 인수가 0과 같으면 및 합니다 *lpszErrorMsg* 단일 null 종료 문자를 포함 하는 인수 (하지 않는 한 합니다 *cbErrorMsgMax* 인수가 0).
