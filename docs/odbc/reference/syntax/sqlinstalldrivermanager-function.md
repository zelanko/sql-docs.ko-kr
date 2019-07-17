---
title: SQLInstallDriverManager 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverManager
helpviewer_keywords:
- SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f1e3ac7f0a76c607fa07d6eb92d069d99ef5e0a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076208"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 함수
**규칙**  
 도입 된 버전: ODBC 1.0: Windows XP 서비스 팩 2, Windows Server 2003 서비스 팩 1 이상 운영 체제에서 사용 되지 않음  
  
 **요약**  
 **SQLInstallDriverManager** ODBC 핵심 구성 요소 설치에 대 한 대상 디렉터리의 경로 반환 합니다. 실제로 호출 프로그램 대상 디렉터리에 드라이버 관리자의 파일을 복사 해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>인수  
 *lpszPath*  
 [출력] 설치 대상 디렉터리의 경로입니다.  
  
 *cbPathMax*  
 [입력] 길이가 *lpszPath*합니다. 이상 이어야 합니다 _max_path(256 바이트입니다.  
  
 *pcbPathOut*  
 [출력] 총 바이트 (null 종료 바이트 제외)에서 반환 된 *lpszPath*합니다. 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *cbPathMax*, 경로 *lpszPath* 잘립니다 *cbPathMax* null 종료 빼기 문자입니다. 합니다 *pcbPathOut* 인수로 null 포인터를 사용할 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLInstallDriverManager** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|합니다 *lpszPath* 인수가 출력 경로 포함 하기에 충분 합니다. 버퍼의 잘린된 경로 포함합니다.<br /><br /> 합니다 *cbPathMax* 인수가 _max_path(256 미만입니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|증가 또는 구성 요소 사용 횟수를 감소 시킬 수 없습니다.|설치 관리자는 ODBC 핵심 구성 요소 사용 횟수를 증가 하지 않습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 **SQLInstallDriverManager** 시스템 정보에 ODBC 핵심 구성 요소 및 구성 요소 사용 증가 수에 대 한 경로 반환 하기 위해 호출 됩니다. 드라이버 관리자의 버전이 이미 있는 경우 드라이버에 대 한 구성 요소 사용 수 없는 경우, 새 구성 요소 사용 개수 값을 2로 설정 됩니다.  
  
 응용 프로그램 설치 프로그램은 실제로 핵심 구성 요소 파일을 복사 하는 일을 담당 하 고 계산 파일 사용을 유지 관리 합니다. 핵심 구성 요소 파일을 이전에 설치 되지 않은 경우 응용 프로그램 설치 프로그램 파일을 복사를 업데이트 하 고 파일 사용 횟수를 생성 해야. 파일을 이전에 설치한 경우 설치 프로그램 파일 사용 횟수를 단순히 증가 합니다.  
  
 경우 이전 버전의 드라이버 관리자 응용 프로그램 설치 프로그램을 설치 했던 것 핵심 구성 요소를 제거 하 고 다시 설치 핵심 구성 요소 사용 횟수는 유효한 해야 합니다. **SQLRemoveDriverManager** 구성 요소 사용 횟수를 감소 시키기 위해 먼저 호출 해야 합니다. **SQLInstallDriverManager** 다음 구성 요소 사용 횟수를 증가 시킬 호출 해야 합니다. 응용 프로그램 설치 프로그램을 새 파일로 이전 핵심 구성 요소 파일을 대체 해야 합니다. 파일 사용 횟수를 동일 하 게 유지 됩니다 및 이전 버전 핵심 구성 요소 파일을 사용 하는 다른 응용 프로그램에서 이제 최신 버전 파일을 사용 합니다.  
  
 ODBC 핵심 구성 요소, 드라이버 및 translator의 새로운 치의 경우 응용 프로그램 설치 프로그램 순서로 다음 함수를 호출 해야 합니다. **SQLInstallDriverManager**, **SQLInstallDriverEx**를 **SQLConfigDriver** (사용 하 여를 *문제점과* ODBC_INSTALL_DRIVER의)을 차례로  **SQLInstallTranslatorEx**합니다. 응용 프로그램 설치 프로그램의 핵심 구성 요소, 드라이버 및 변환기의 제거를 시퀀스에서 다음 함수를 호출 해야 합니다. **SQLRemoveTranslator**, **SQLRemoveDriver**를 차례로 **SQLRemoveDriverManager**합니다. 이 시퀀스에서 이러한 함수를 호출 해야 합니다. 모든 구성 요소를 업그레이드에서 시퀀스의 모든 제거 함수를 호출 해야 하 고 시퀀스의 모든 설치 함수를 호출 해야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 드라이버를 제거 합니다.|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|드라이버 설치|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|변환기를 설치합니다.|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|드라이버 제거|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|드라이버 관리자를 제거합니다.|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|변환기를 제거합니다.|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
