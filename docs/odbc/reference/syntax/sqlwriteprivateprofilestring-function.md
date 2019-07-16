---
title: SQLWritePrivateProfileString 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4b847576e503fbbbb511d2dda8f60675c298681c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039386"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 함수
**규칙**  
 도입 된 버전: ODBC 2.0  
  
 **요약**  
 **SQLWritePrivateProfileString** 시스템 정보 Odbc.ini 하위 키 값 이름 및 데이터를 씁니다.  
  
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
 [입력] 문자열을 복사할 섹션의 이름이 포함 된 null로 끝나는 문자열을 가리킵니다. 섹션 존재 하지 않는 경우 만들어집니다. 섹션의 이름은 대/소문자에 관계 없이; 모든 조합을 대문자 및 소문자 문자열 수 있습니다.  
  
 *lpszEntry*  
 [입력] 연결 문자열을 사용 하 여 키의 이름이 포함 된 null로 끝나는 문자열을 가리킵니다. 지정된 된 섹션에 키 없으면 자동으로 만들어집니다. 이 인수가 NULL 이면 전체 섹션을 섹션에서 모든 항목을 포함 하 여 삭제 됩니다.  
  
 *lpszString*  
 [입력] 파일을 쓸 수 있도록 null로 끝나는 문자열을 가리킵니다. 이 인수가 NULL 이면 키가 가리키는 합니다 *lpszEntry* 인수 삭제 됩니다.  
  
 *lpszFilename*  
 [출력] 초기화 파일의 이름을 지정 하는 null로 끝나는 문자열을 가리킵니다.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLWritePrivateProfileString** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청이 실패 했습니다.|요청 된 시스템 정보를 작성할 수 있습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 **SQLWritePrivateProfileString** Microsoft Windows/Windows 2000에서 Microsoft® Windows® 포트 드라이버 및 드라이버 설치 Dll로 간단 하 게 제공 됩니다. 에 대 한 호출 **WritePrivateProfileString** Odbc.ini 파일에 프로필 문자열에 대 한 호출으로 바꿔야 하는 쓰기 **SQLWritePrivateProfileString**합니다. **SQLWritePrivateProfileString** 시스템 정보 Odbc.ini 하위 키에 지정 된 값 이름과 데이터를 추가 하려면 Win32® api에서 함수를 호출 합니다.  
  
 구성 모드 DSN 값을 나열 하는 Odbc.ini 항목은 시스템 정보에서 위치를 나타냅니다. DSN이 사용자 DSN (상태 변수가 USERDSN_ONLY) 인 경우 함수는 HKEY_CURRENT_USER에서 Odbc.ini 항목을 씁니다. DSN 시스템 DSN (SYSTEMDSN_ONLY) 인 경우 함수에서 HKEY_LOCAL_MACHINE Odbc.ini 항목을 씁니다. HKEY_CURRENT_USER 시도할 경우 상태 변수가 BOTHDSN 및 HKEY_LOCAL_MACHINE는 실패 한 경우.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|시스템 정보에서 값 가져오기|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
