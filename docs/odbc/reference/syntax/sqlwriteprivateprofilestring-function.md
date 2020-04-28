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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0de5ad074fb2b760420686feddff58b26887112
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286886"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 함수
**규칙**  
 소개 된 버전: ODBC 2.0  
  
 **요약**  
 **SQLWritePrivateProfileString** 는 값 이름과 데이터를 시스템 정보의 Odbc .ini 하위 키에 씁니다.  
  
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
 입력 문자열이 복사 될 섹션의 이름을 포함 하는 null로 끝나는 문자열을 가리킵니다. 섹션이 없으면 생성 됩니다. 섹션 이름은 대/소문자를 구분 하지 않습니다. 문자열은 대/소문자를 임의로 조합 하 여 사용할 수 있습니다.  
  
 *lpszEntry*  
 입력 문자열과 연결할 키의 이름을 포함 하는 null로 끝나는 문자열을 가리킵니다. 지정 된 섹션에 키가 없으면 해당 키가 생성 됩니다. 이 인수가 NULL 이면 섹션 내의 모든 항목을 포함 하 여 전체 섹션이 삭제 됩니다.  
  
 *lpszString*  
 입력 파일에 쓸 null로 끝나는 문자열을 가리킵니다. 이 인수가 NULL 이면 *lpszEntry* 인수에서 가리키는 키가 삭제 됩니다.  
  
 *lpszFilename*  
 출력 초기화 파일의 이름을 나타내는 null로 끝나는 문자열을 가리킵니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLWritePrivateProfileString** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청 실패|요청 된 시스템 정보를 쓸 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLWritePrivateProfileString** 는 Microsoft® windows®에서 MICROSOFT windows NT®/windows 2000으로 드라이버 및 드라이버 설치 dll을 이식 하는 간단한 방법으로 제공 됩니다. **WritePrivateProfileString** 파일에 프로필 문자열을 기록 하는 호출을 **SQLWritePrivateProfileString**에 대 한 호출로 바꾸어야 합니다. **SQLWritePrivateProfileString** 는 WIN32® API의 함수를 호출 하 여 지정 된 값 이름과 데이터를 시스템 정보의 Odbc .ini 하위 키에 추가 합니다.  
  
 구성 모드는 DSN 값을 나열 하는 Odbc .ini 항목이 시스템 정보에 있는지 여부를 나타냅니다. DSN이 사용자 DSN 인 경우 (상태 변수가 USERDSN_ONLY) 함수는 HKEY_CURRENT_USER의 Odbc .ini 항목에 씁니다. DSN이 시스템 DSN (SYSTEMDSN_ONLY) 인 경우 함수는 HKEY_LOCAL_MACHINE의 Odbc .ini 항목에 씁니다. 상태 변수가 BOTHDSN HKEY_CURRENT_USER 시도 하 고 실패 하면 HKEY_LOCAL_MACHINE 사용 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|시스템 정보에서 값 가져오기|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
