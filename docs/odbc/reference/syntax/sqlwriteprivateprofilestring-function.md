---
title: SQLWrite개인 프로필 스트링 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWritePrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWritePrivateProfileString
helpviewer_keywords:
- SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0de5ad074fb2b760420686feddff58b26887112
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286886"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 함수
**규칙**  
 버전 출시: ODBC 2.0  
  
 **요약**  
 **SQLWritePrivateProfileString은** 시스템 정보의 Odbc.ini 하위 키에 값 이름과 데이터를 씁니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>인수  
 *lpszSection*  
 [입력] 문자열이 복사될 섹션의 이름을 포함하는 null 종료된 문자열을 가리킵니다. 단면이 없으면 만들어집니다. 섹션의 이름은 대/소문자 독립적입니다. 문자열은 대문자와 소문자의 조합일 수 있습니다.  
  
 *lpsz항목*  
 [입력] 문자열과 연결할 키의 이름을 포함하는 null 종료 된 문자열을 가리킵니다. 지정된 섹션에 키가 없으면 키가 만들어집니다. 이 인수가 NULL이면 섹션 내의 모든 항목을 포함한 전체 섹션이 삭제됩니다.  
  
 *lpszString*  
 [입력] 파일에 쓸 null 종료 된 문자열을 가리킵니다. 이 인수가 NULL이면 *lpszEntry* 인수가 가리키는 키가 삭제됩니다.  
  
 *lpszFilename*  
 [출력] 초기화 파일의 이름을 지정하는 null 종료 문자열을 가리킵니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLWritePrivateProfileString** FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청 실패|요청된 시스템 정보를 기록할 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLWritePrivateProfileString은** 마이크로 소프트에서 드라이버 및 드라이버 설정 DLL을 포트하는 간단한 방법으로 제공됩니다® 윈도우® 마이크로 소프트 윈도우 NT® / 윈도우 2000. Odbc.ini 파일에 프로필 문자열을 작성하는 **WritePrivateProfileString** 호출은 **SQLWritePrivateProfileString**에 대한 호출로 대체되어야 합니다. **SQLWritePrivateProfileString** 은 Win32® API의 함수를 호출하여 시스템 정보의 Odbc.ini 하위 키에 지정된 값 이름과 데이터를 추가합니다.  
  
 구성 모드는 DSN 값을 나열하는 Odbc.ini 항목이 시스템 정보에 있는 위치를 나타냅니다. DSN이 사용자 DSN(상태 변수가 USERDSN_ONLY 경우) 함수는 HKEY_CURRENT_USER Odbc.ini 항목에 기록됩니다. DSN이 시스템 DSN(SYSTEMDSN_ONLY)인 경우 함수는 HKEY_LOCAL_MACHINE Odbc.ini 항목에 기록됩니다. 상태 변수가 BOTHDSN인 경우 HKEY_CURRENT_USER 시도되고 실패하면 HKEY_LOCAL_MACHINE 사용됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|시스템 정보에서 값 얻기|[SQLGet개인 프로필 스트링](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
