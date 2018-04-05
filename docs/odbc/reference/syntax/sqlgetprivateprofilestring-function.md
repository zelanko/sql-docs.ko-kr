---
title: SQLGetPrivateProfileString 함수 | Microsoft Docs
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
- SQLGetPrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetPrivateProfileString
helpviewer_keywords:
- SQLGetPrivateProfileString function [ODBC]
ms.assetid: b72ca065-4d67-48df-baac-e18379a8320a
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7829cbff471b431b5c4975e8066356479631596
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 함수
**규칙**  
 ODBC 2.0 도입 된 버전:  
  
 **요약**  
 **SQLGetPrivateProfileString** 의 이름 값 또는 시스템 정보 값에 해당 하는 데이터의 목록을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 키 이름이 포함 된 섹션을 지정 하는 null로 끝나는 문자열을 가리킵니다. 이 인수가 NULL 이면 함수는 제공 된 버퍼가에 모든 섹션 이름이 파일에 복사 합니다.  
  
 *lpszEntry*  
 [입력] 검색할 수 있는 연결된 문자열은 키 이름이 포함 된 null로 끝나는 문자열을 가리킵니다. 이 인수가 NULL 이면 모든 키 이름으로 지정 된 섹션에는 *lpszSection* 인수 하 여 지정 된 버퍼에 복사 됩니다는 *RetBuffer* 인수입니다.  
  
 *lpszDefault*  
 [입력] 초기화 파일의 키를 찾을 수 없는 경우 지정된 된 키에 대 한 기본값을 지정 하는 null로 끝나는 문자열을 가리킵니다. 이 인수는 NULL 일 수 없습니다.  
  
 *RetBuffer*  
 [출력] 검색 된 문자열을 수신 하는 버퍼를 가리킵니다.  
  
 *cbRetBuffer*  
 [입력] 크기를 가리키는 버퍼의 문자 단위로 지정 된 *RetBuffer* 인수입니다.  
  
 *lpszFilename*  
 [입력] 초기화 파일 이름을 지정 하는 null로 끝나는 문자열을 가리킵니다. 이 인수에는 전체 파일 경로를 찾을 수 없는 경우 기본 디렉터리가 검색 됩니다.  
  
## <a name="returns"></a>반환 값  
 **SQLGetPrivateProfileString** 읽은 문자 수를 나타내는 정수 값을 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 호출할 때 **SQLGetPrivateProfileString** 실패 하면 연결 된  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetPrivateProfileString** Microsoft Windows/Windows 2000에서 Microsoft® Windows® 포트 드라이버 및 드라이버 설치 Dll로 간단한 방법으로 제공 됩니다. 에 대 한 호출이 **GetPrivateProfileString** Odbc.ini 파일에서 프로 파일 문자열을 바꿀 해당 검색에 대 한 호출이 **SQLGetPrivateProfileString**합니다. **SQLGetPrivateProfileString** 값 또는 시스템 정보 Odbc.ini 하위 키의 값에 해당 하는 데이터의 요청 된 이름을 검색 하기 위해 Win32® api에서 함수를 호출 합니다.  
  
 구성 모드 (의해 설정 **SQLSetConfigMode**) DSN 값을 나열 하는 Odbc.ini 항목 시스템 정보에 위치를 나타냅니다. DSN (구성 모드는 USERDSN_ONLY은)는 사용자 DSN 이면의 Odbc.ini 항목 HKEY_CURRENT_USER에 함수를 읽습니다. DSN 시스템 DSN (SYSTEMDSN_ONLY) 이면 HKEY_LOCAL_MACHINE에 Odbc.ini 항목에서 함수를 읽습니다. 구성 모드 BOTHDSN 이면 HKEY_CURRENT_USER 시도 되 면 및 HKEY_LOCAL_MACHINE 사용 되는 실패 한 경우.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|시스템 정보에는 값을 쓰기|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
