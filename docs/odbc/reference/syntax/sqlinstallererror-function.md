---
title: SQLInstaller 오류 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e749237cf87c5054b8273f38531d9336d316e040
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302104"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 함수
**규칙**  
 버전 출시: ODBC 3.0  
  
 **요약**  
 **SQLInstaller 오류** ODBC 설치 프로그램 기능에 대 한 오류 또는 상태 정보를 반환 합니다.  
  
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
 [입력] 오류 레코드 번호입니다. 유효한 숫자는 1에서 8사이입니다.  
  
 *pfErrorCode*  
 [출력] 설치 관리자 오류 코드입니다. (자세한 내용은 "댓글"을 참조하십시오.)  
  
 *lpszErrorMsg*  
 [출력] 오류 메시지 텍스트에 대한 저장소에 대한 포인터입니다.  
  
 *cbErrorMsgMax*  
 [입력] *szErrorMsg* 버퍼의 최대 길이입니다. 이 값은 null 종료 문자를 뺀 SQL_MAX_MESSAGE_LENGTH 같아야 합니다.  
  
 *cbErrorMsgMax*  
 [입력] *szErrorMsg* 버퍼의 최대 길이입니다. 이 값은 null 종료 문자를 뺀 SQL_MAX_MESSAGE_LENGTH 같아야 합니다.  
  
 *pcbErrorMsg*  
 [출력] *lpszErrorMsg에서*반환할 수 있는 총 바이트 수(null-종료 문자 제외)에 대한 포인터입니다. 반환할 수 있는 바이트 수가 *cbErrorMsgMax보다*크거나 같으면 *lpszErrorMsg의* 오류 메시지 텍스트가 null 종료 문자 바이트를 뺀 *cbErrorMsgMax로* 잘립니다. *pcbErrorMsg* 인수는 null 포인터일 수 있습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA 또는 SQL_ERROR.  
  
## <a name="diagnostics"></a>진단  
 **SQLInstallerError** 자체에 대 한 오류 값을 게시 하지 않습니다. **SQLInstallerError** 오류 정보를 검색할 수 없는 경우 SQL_NO_DATA 반환 합니다 (이 경우 *pfErrorCode* 정의 되지 않습니다). **SQLInstallerError일반적으로** SQL_ERROR 반환 하는 어떤 이유로 오류 값에 액세스할 수 없습니다 하는 **경우, SQLInstallerError** SQL_ERROR 반환 하지만 오류 값을 게시 하지 않습니다. 경고*문자열(lpszErrorMsg)의 길이를*모르는 경우 *lpszErrorMsg를* NULL로 설정하고 **SQLInstallerError를**호출할 수 있습니다. **SQLInstallerError는** *cbErrorMsgMax에서*경고 문자열의 길이를 반환합니다. 오류 메시지의 버퍼가 너무 짧으면 **SQLInstallerError가** SQL_SUCCESS_WITH_INFO 반환하고 **SQLInstallerError**에 대한 올바른 *pfErrorCode* 값을 반환합니다.  
  
 오류 메시지에서 잘림이 발생했는지 여부를 확인하기 위해 응용 프로그램은 *cbErrorMsgMax* 인수의 값을 *pcbErrorMssg* 인수에 기록된 메시지 텍스트의 실제 길이와 비교할 수 있습니다. 잘림이 발생하는 경우 *lpszErrorMsg에* 대해 올바른 버퍼 길이를 할당해야 하며 **SQLInstallerError는** 해당 *iError* 레코드를 사용하여야 합니다.  
  
## <a name="comments"></a>주석  
 ODBC 설치 프로그램에 대한 이전 호출이 FALSE를 반환할 때 응용 프로그램에서 **SQLInstallerError를** 호출합니다. ODBC 설치 프로그램 및 드라이버 또는 번역기 설치 기능은 함수가 실패할 때만 0 개 이상의 오류를 게시합니다(FALSE를 반환합니다). 따라서 응용 프로그램은 ODBC 설치 프로그램 기능이 실패한 후에만 **SQLInstallerError를** 호출합니다.  
  
 ODBC 설치 프로그램 오류 큐는 새 설치 프로그램 함수가 호출될 때마다 플러시됩니다. 따라서 응용 프로그램은 마지막 설치 관리자 함수 호출 이외의 함수에 대한 오류를 검색할 수 없습니다.  
  
 함수 호출에 대해 여러 오류를 검색하려면 응용 프로그램에서 **SQLInstallerError를** 여러 번 호출합니다.  
  
 추가 정보가 없는 경우 **SQLInstallerError는** SQL_NO_DATA *반환하고, pfErrorCode* 인수는 정의되지 않고, *pcbErrorMsg* 인수는 0이고, *lpszErrorMssg* 인수는 단일 null 종료 문자를 포함합니다(cbErrorMsgMax 인수가 0이 아니라면). *cbErrorMsgMax*
