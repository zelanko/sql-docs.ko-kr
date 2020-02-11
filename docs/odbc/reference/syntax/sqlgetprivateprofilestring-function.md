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
ms.openlocfilehash: 6d58fe69e487b4f61384f9bd146b17c6d9ada9ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061469"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 함수
**규칙**  
 소개 된 버전: ODBC 2.0  
  
 **요약**  
 **SQLGetPrivateProfileString** 시스템 정보 값에 해당 하는 값 또는 데이터의 이름 목록을 가져옵니다.  
  
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
 입력 키 이름이 포함 된 섹션을 지정 하는 null로 끝나는 문자열을 가리킵니다. 이 인수가 NULL 이면 함수는 파일의 모든 섹션 이름을 제공 된 버퍼에 복사 합니다.  
  
 *lpszEntry*  
 입력 연결 된 문자열을 검색할 키 이름을 포함 하는 null로 끝나는 문자열을 가리킵니다. 이 인수가 NULL 이면 *lpszSection* 인수에 지정 된 섹션의 모든 키 이름이 *보존 버퍼* 인수에 지정 된 버퍼에 복사 됩니다.  
  
 *lpszDefault*  
 입력 초기화 파일에서 키를 찾을 수 없는 경우 지정 된 키의 기본값을 지정 하는 null로 끝나는 문자열을 가리킵니다. 이 인수는 NULL 일 수 없습니다.  
  
 *보존 버퍼*  
 출력 검색 된 문자열을 받는 버퍼를 가리킵니다.  
  
 *Cb보존 버퍼*  
 입력 *보존 버퍼* 인수가 가리키는 버퍼의 크기 (문자 수)를 지정 합니다.  
  
 *lpszFilename*  
 입력 초기화 파일의 이름을 나타내는 null로 끝나는 문자열을 가리킵니다. 이 인수에 파일의 전체 경로가 포함 되어 있지 않으면 기본 디렉터리가 검색 됩니다.  
  
## <a name="returns"></a>반환  
 **SQLGetPrivateProfileString** 는 읽은 문자 수를 나타내는 정수 값을 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetPrivateProfileString** 에 대 한 호출이 실패 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetPrivateProfileString** 는 Microsoft® windows®에서 MICROSOFT windows NT®/windows 2000으로 드라이버 및 드라이버 설치 dll을 이식 하는 간단한 방법으로 제공 됩니다. Odbc .ini 파일에서 프로필 문자열을 검색 하는 **GetPrivateProfileString** 에 대 한 호출은 **SQLGetPrivateProfileString**에 대 한 호출로 대체 되어야 합니다. **SQLGetPrivateProfileString** 는 WIN32® API의 함수를 호출 하 여 시스템 정보의 Odbc .ini 하위 키 값에 해당 하는 값 또는 데이터의 요청 된 이름을 검색 합니다.  
  
 구성 모드 ( **SQLSetConfigMode**에 의해 설정 됨)는 DSN 값을 나열 하는 Odbc .ini 항목이 시스템 정보에 있는지를 나타냅니다. DSN이 사용자 DSN (구성 모드 USERDSN_ONLY) 인 경우 함수는 HKEY_CURRENT_USER의 Odbc .ini 항목에서 읽습니다. DSN이 시스템 DSN (SYSTEMDSN_ONLY) 인 경우 함수는 HKEY_LOCAL_MACHINE의 Odbc .ini 항목에서 읽습니다. 구성 모드가 BOTHDSN 인 경우 HKEY_CURRENT_USER 시도 하 고 실패 하면 HKEY_LOCAL_MACHINE 사용 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|시스템 정보에 값을 씁니다.|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
