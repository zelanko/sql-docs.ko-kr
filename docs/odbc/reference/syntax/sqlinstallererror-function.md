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
ms.openlocfilehash: ab9461d87a3df2efc98c38e4c72cee4c247fee7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138033"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 함수
**규칙**  
 소개 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLInstallerError** 는 ODBC 설치 관리자 기능에 대 한 오류 또는 상태 정보를 반환 합니다.  
  
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
 입력 오류 레코드 번호입니다. 유효한 숫자는 1에서 8 까지입니다.  
  
 *pfErrorCode*  
 출력 설치 관리자 오류 코드입니다. 자세한 내용은 "설명"을 참조 하십시오.  
  
 *lpszErrorMsg*  
 출력 오류 메시지 텍스트의 저장소에 대 한 포인터입니다.  
  
 *cbErrorMsgMax*  
 입력 *Szerrormsg* 버퍼의 최대 길이입니다. 이 값은 null 종료 문자를 뺀 SQL_MAX_MESSAGE_LENGTH 보다 작거나 같아야 합니다.  
  
 *cbErrorMsgMax*  
 입력 *Szerrormsg* 버퍼의 최대 길이입니다. 이 값은 null 종료 문자를 뺀 SQL_MAX_MESSAGE_LENGTH 보다 작거나 같아야 합니다.  
  
 *pcbErrorMsg*  
 출력 *LpszErrorMsg*에서 반환 하는 데 사용할 수 있는 총 바이트 수 (null 종결 문자 제외)에 대 한 포인터입니다. 반환할 수 있는 바이트 수가 *Cberrormsgmax*보다 크거나 같으면 *lpszErrorMsg* 의 오류 메시지 텍스트가 *cberrormsgmax* 에서 null 종료 문자 바이트를 뺀 값으로 잘립니다. *Pcberrormsg* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA 또는 SQL_ERROR입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLInstallerError** 는 자체에 대 한 오류 값을 게시 하지 않습니다. **SQLInstallerError** 는 오류 정보를 검색할 수 없는 경우에 SQL_NO_DATA를 반환 합니다 .이 경우 *pfErrorCode* 가 정의 되지 않습니다. **SQLInstallerError** 가 일반적으로 SQL_ERROR 반환 하는 어떤 이유로 든 오류 값에 액세스할 수 없는 경우 **SQLInstallerError** 는 SQL_ERROR를 반환 하지만 오류 값은 게시 하지 않습니다. 경고 문자열 (*lpszErrorMsg*)의 길이를 모르는 경우 *lpszErrorMsg* 를 NULL로 설정 하 고 **SQLInstallerError**를 호출할 수 있습니다. 그런 다음 **SQLInstallerError** 는 *Cberrormsgmax*에서 경고 문자열의 길이를 반환 합니다. 오류 메시지에 대 한 버퍼가 너무 짧으면 **SQLInstallerError** 는 SQL_SUCCESS_WITH_INFO을 반환 하 고 **SQLInstallerError**에 대 한 올바른 *pfErrorCode* 값을 반환 합니다.  
  
 오류 메시지에서 잘림이 발생 했는지 여부를 확인 하기 위해 응용 프로그램에서는 *Cberrormsgmax* 인수의 값을 *Pcberrormsg* 인수에 쓰여진 메시지 텍스트의 실제 길이와 비교할 수 있습니다. 잘림이 발생 하는 경우 *lpszErrorMsg* 에 올바른 버퍼 길이를 할당 하 고 해당 *ierror* 레코드를 사용 하 여 **SQLInstallerError** 를 다시 호출 해야 합니다.  
  
## <a name="comments"></a>주석  
 ODBC 설치 관리자 함수에 대 한 이전 호출에서 FALSE를 반환 하는 경우 응용 프로그램은 **SQLInstallerError** 를 호출 합니다. ODBC 설치 관리자 및 드라이버 또는 변환기 설치 함수는 함수가 실패 한 경우에만 0 개 이상의 오류 (FALSE를 반환 함)를 게시 합니다. 따라서 응용 프로그램은 ODBC 설치 관리자 기능이 실패 한 후에만 **SQLInstallerError** 를 호출 합니다.  
  
 ODBC 설치 관리자 오류 큐는 새 설치 관리자 함수를 호출할 때마다 플러시됩니다. 따라서 응용 프로그램은 마지막 설치 관리자 함수 호출 이외의 함수에 대 한 오류를 검색할 수 없습니다.  
  
 함수 호출에 대 한 여러 오류를 검색 하기 위해 응용 프로그램은 **SQLInstallerError** 를 여러 번 호출 합니다.  
  
 추가 정보가 없는 경우 **SQLInstallerError** 는 SQL_NO_DATA을 반환 하 고 *pfErrorCode* 인수는 Undefined 이며 *pcberrormsg* 인수는 0이 고 *lpszErrorMsg* 인수는 단일 Null 종료 문자를 포함 합니다 ( *cberrormsgmax* 인수가 0과 같지 않은 경우).
