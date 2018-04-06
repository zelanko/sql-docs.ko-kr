---
title: SQLWritePrivateProfileString 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLWritePrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWritePrivateProfileString
helpviewer_keywords:
- SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 081d91ac2c257fbaa60b93de24dd134ea698bcd9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 함수
**규칙**  
 ODBC 2.0 도입 된 버전:  
  
 **요약**  
 **SQLWritePrivateProfileString** 값 이름 및 데이터는 Odbc.ini 하위 키의 시스템 정보를 씁니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>인수  
 *lpszSection*  
 [입력] 문자열을 복사할 섹션의 이름을 포함 하는 null로 끝나는 문자열을 가리킵니다. 섹션이 없는 경우 자동으로 만들어집니다. 섹션 이름은 대/소문자에 관계 없이; 모든 조합의 대문자 및 소문자 문자열 수 있습니다.  
  
 *lpszEntry*  
 [입력] 문자열과 연결 될 키의 이름을 포함 하는 null로 끝나는 문자열을 가리킵니다. 지정된 된 섹션에 키가 없는 경우 자동으로 만들어집니다. 이 인수가 NULL 이면 섹션에서 모든 항목을 포함 한 전체 섹션을 삭제 됩니다.  
  
 *lpszString*  
 [입력] 파일에 쓰여지도록 null로 끝나는 문자열을 가리킵니다. 이 인수가 NULL 이면 키가 가리키는 *lpszEntry* 인수 삭제 됩니다.  
  
 *lpszFilename*  
 [출력] 초기화 파일 이름을 지정 하는 null로 끝나는 문자열을 가리킵니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLWritePrivateProfileString** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청이 실패 했습니다.|요청 된 시스템 정보를 쓸 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 **SQLWritePrivateProfileString** Microsoft Windows/Windows 2000에서 Microsoft® Windows® 포트 드라이버 및 드라이버 설치 Dll로 간단한 방법으로 제공 됩니다. 에 대 한 호출이 **WritePrivateProfileString** Odbc.ini 파일에 프로필 문자열에 대 한 호출으로 대체 해야 쓰기에 **SQLWritePrivateProfileString**합니다. **SQLWritePrivateProfileString** Odbc.ini 하위 키의 시스템 정보를 지정 된 값 이름 및 데이터를 추가 하려면 Win32® api에서 함수를 호출 합니다.  
  
 구성 모드 DSN 값을 나열 하는 Odbc.ini 항목 시스템 정보에는 위치를 나타냅니다. DSN (상태 변수는 USERDSN_ONLY은)는 사용자 DSN 이면 함수 HKEY_CURRENT_USER의 Odbc.ini 엔트리를 씁니다. DSN 시스템 DSN (SYSTEMDSN_ONLY) 이면 함수에서 HKEY_LOCAL_MACHINE Odbc.ini 항목을 씁니다. BOTHDSN 상태 변수를 사용 하는 경우 HKEY_CURRENT_USER 시도 되 면 하 고 실패 한 경우 HKEY_LOCAL_MACHINE 사용 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|시스템 정보에서 값 가져오기|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
