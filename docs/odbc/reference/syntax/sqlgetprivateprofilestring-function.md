---
title: SQLGetPrivateProfileString 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17ac06d65d519be86ec077e6c6d39896c7f5ad46
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537334"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 함수
**규칙**  
 도입 된 버전: ODBC 2.0  
  
 **요약**  
 **SQLGetPrivateProfileString** 의 이름 값 또는 시스템 정보 값에 해당 하는 데이터의 목록을 가져옵니다.  
  
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
 [입력] 키 이름이 포함 된 섹션을 지정 하는 null로 끝나는 문자열을 가리킵니다. 이 인수가 NULL 이면 함수는 제공 된 버퍼에 모든 섹션 이름을 파일에 복사 합니다.  
  
 *lpszEntry*  
 [입력] 연결된 문자열을 검색 하려면 키 이름을 포함 하는 null로 끝나는 문자열을 가리킵니다. 모든 키 이름으로 지정 된 섹션에서이 인수가 NULL 이면를 *lpszSection* 인수는 지정 된 버퍼에 복사 합니다 *RetBuffer* 인수.  
  
 *lpszDefault*  
 [입력] 초기화 파일의 키를 찾을 수 없는 경우 지정된 된 키에 대 한 기본값을 지정 하는 null로 끝나는 문자열을 가리킵니다. 이 인수는 NULL 일 수 없습니다.  
  
 *RetBuffer*  
 [출력] 검색된 문자열을 수신 하는 버퍼를 가리킵니다.  
  
 *cbRetBuffer*  
 [입력] 문자를 가리키는 버퍼의 크기를 지정 합니다 *RetBuffer* 인수입니다.  
  
 *lpszFilename*  
 [입력] 초기화 파일의 이름을 지정 하는 null로 끝나는 문자열을 가리킵니다. 이 인수에 전체 파일 경로 찾을 수 없는 경우에 기본 디렉터리가 검색 됩니다.  
  
## <a name="returns"></a>반환 값  
 **SQLGetPrivateProfileString** 읽은 문자 수를 나타내는 정수 값을 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 호출 하 여 **SQLGetPrivateProfileString** 실패 하면 연결 된  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetPrivateProfileString** Microsoft Windows/Windows 2000에서 Microsoft® Windows® 포트 드라이버 및 드라이버 설치 Dll로 간단 하 게 제공 됩니다. 에 대 한 호출 **GetPrivateProfileString** Odbc.ini 파일에서 프로필 문자열로 바꿔야 하는 검색에 대 한 호출 **SQLGetPrivateProfileString**합니다. **SQLGetPrivateProfileString** 값 또는 시스템 정보 Odbc.ini 하위 키의 값에 해당 하는 데이터의 요청된 이름을 검색 하기 위해 Win32® api에서 함수를 호출 합니다.  
  
 구성 모드 (에서 설정 된 **SQLSetConfigMode**) 시스템 정보에 DSN 값을 나열 하는 Odbc.ini 항목 위치를 나타냅니다. DSN 구성 모드를 이어서 USERDSN_ONLY 사용자 DSN 이면 함수는 Odbc.ini 항목 HKEY_CURRENT_USER에서 읽습니다. DSN 시스템 DSN (SYSTEMDSN_ONLY) 인 경우 함수는 Odbc.ini 항목 HKEY_LOCAL_MACHINE에서 읽습니다. 구성 모드 BOTHDSN 이면 HKEY_CURRENT_USER 시도 되 면 및 HKEY_LOCAL_MACHINE는 실패 한 경우.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|시스템 정보 값을 쓰는|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
