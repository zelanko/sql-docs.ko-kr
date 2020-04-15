---
title: SQLGet개인 프로필 스트링 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetPrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetPrivateProfileString
helpviewer_keywords:
- SQLGetPrivateProfileString function [ODBC]
ms.assetid: b72ca065-4d67-48df-baac-e18379a8320a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c12fc8d08535960cbb239c14e017b2ad5faa6c0e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303295"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 함수
**규칙**  
 버전 출시: ODBC 2.0  
  
 **요약**  
 **SQLGetPrivateProfileString은** 시스템 정보의 값에 해당하는 값 또는 데이터의 이름 목록을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>인수  
 *lpszSection*  
 [입력] 키 이름을 포함하는 섹션을 지정하는 null 종료 된 문자열을 가리킵니다. 이 인수가 NULL이면 함수는 파일의 모든 섹션 이름을 제공된 버퍼에 복사합니다.  
  
 *lpsz항목*  
 [입력] 연결된 문자열을 검색할 키 이름을 포함하는 null 종료된 문자열을 가리킵니다. 이 인수가 NULL이면 *lpszSection* 인수에 의해 지정된 섹션의 모든 키 이름이 *RetBuffer* 인수에서 지정한 버퍼에 복사됩니다.  
  
 *lpsz기본값*  
 [입력] 초기화 파일에서 키를 찾을 수 없는 경우 지정된 키에 대한 기본값을 지정하는 null 종료 된 문자열을 가리킵니다. 이 인수는 NULL일 수 없습니다.  
  
 *리트버퍼*  
 [출력] 검색된 문자열을 받는 버퍼를 가리킵니다.  
  
 *cbRet버퍼*  
 [입력] *RetBuffer* 인수에 의해 가리키는 버퍼의 크기(문자)를 지정합니다.  
  
 *lpszFilename*  
 [입력] 초기화 파일의 이름을 지정하는 null 종료 문자열을 가리킵니다. 이 인수에 파일에 대한 전체 경로가 포함되어 있지 않으면 기본 디렉터리가 검색됩니다.  
  
## <a name="returns"></a>반환  
 **SQLGetPrivateProfileString** 읽은 문자 수를 나타내는 정수 값을 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetPrivateProfileString에** 대한 호출이 실패하면 **SQLInstaller Error**를 호출하여 연결된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetPrivateProfileString은** 마이크로 소프트의 마이크로 소프트® 윈도우® 마이크로 소프트 윈도우 NT® / 윈도우 2000에서 드라이버 및 드라이버 설정 DLL을 포트하는 간단한 방법으로 제공됩니다. Odbc.ini 파일에서 프로필 문자열을 검색하는 **GetPrivateProfileString** 에 대한 호출은 **SQLGetPrivateProfileString**에 대한 호출로 대체되어야 합니다. **SQLGetPrivateProfileString** Win32® API의 함수를 호출하여 시스템 정보의 Odbc.ini 하위 키값에 해당하는 값 또는 데이터의 요청된 이름을 검색합니다.  
  
 구성 **모드(SQLSetConfigMode에서**설정한 대로)는 DSN 값을 나열하는 Odbc.ini 항목이 시스템 정보에 있는 위치를 나타냅니다. DSN이 사용자 DSN(구성 모드가 USERDSN_ONLY 경우)이면 함수는 HKEY_CURRENT_USER Odbc.ini 항목에서 읽습니다. DSN이 시스템 DSN(SYSTEMDSN_ONLY)인 경우 함수는 HKEY_LOCAL_MACHINE Odbc.ini 항목에서 읽습니다. 구성 모드가 BOTHDSN인 경우 HKEY_CURRENT_USER 시도되고 실패하면 HKEY_LOCAL_MACHINE 사용됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|시스템 정보에 값 쓰기|[SQLWrite개인 프로필 스트링](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
