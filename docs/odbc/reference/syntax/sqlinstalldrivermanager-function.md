---
title: SQLInstallDriverManager 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 739af9f6d97dbd4595a3c18254ab53f2a9db10f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 함수
**규칙**  
 버전 소개: ODBC 1.0: Windows XP 서비스 팩 2, Windows Server 2003 서비스 팩 1 및 이상의 운영 체제에서 사용 되지 않습니다  
  
 **요약**  
 **SQLInstallDriverManager** ODBC 핵심 구성 요소 설치에 대 한 대상 디렉터리의 경로 반환 합니다. 실제로 호출 프로그램의 대상 디렉터리로 드라이버 관리자의 파일을 복사 해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>인수  
 *lpszPath*  
 [출력] 설치의 대상 디렉터리의 경로입니다.  
  
 *cbPathMax*  
 [입력] 길이 *lpszPath*합니다. 이상 이어야 합니다 _MAX_PATH 바이트입니다.  
  
 *pcbPathOut*  
 [출력] 총 바이트 수 (null 종료 바이트 제외)에서 반환 된 *lpszPath*합니다. 보다 크거나 반환에 사용할 수 있는 바이트 수가 *cbPathMax*, 경로에 *lpszPath* 잘립니다 *cbPathMax* 뺀 null 종료 문자입니다. *pcbPathOut* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLInstallDriverManager** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*lpszPath* 인수 출력 경로 포함할 수 없습니다. 버퍼의 잘린된 경로 포함합니다.<br /><br /> *cbPathMax* 인수 된 _MAX_PATH 보다 작습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|증가 하거나 구성 요소 사용 횟수를 감소 시킬 수 없습니다.|설치 관리자에서 ODBC 핵심 구성 요소 사용 횟수를 증가 하지 않습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>설명  
 **SQLInstallDriverManager** ODBC 핵심 구성 요소와 구성 요소 사용 증가 시스템 정보에 계산에 대 한 경로 반환 하기 위해 호출 됩니다. 버전의 드라이버 관리자가 이미 존재 하는 경우 드라이버에 대 한 구성 요소의 사용 횟수가 존재 하지 않는 새 구성 요소 사용 개수 값을 2로 설정 됩니다.  
  
 응용 프로그램 설치 프로그램은 물리적으로 핵심 구성 요소 파일을 복사 하 고 계산 파일 사용을 유지 관리. 핵심 구성 요소 파일을 이전에 설치 되지 않은 경우 응용 프로그램 설치 프로그램 파일 복사를 업데이트 하 고 파일 사용 횟수를 생성 해야. 파일이 이전에 설치 된 경우 설치 프로그램 파일 사용 횟수를 단순히 증가 합니다.  
  
 이전 버전의 드라이버 관리자 응용 프로그램 설치 프로그램에서 이전에 설치한, 하는 경우 핵심 구성 요소를 제거 하 고 다시 설치 된 핵심 구성 요소 사용 횟수는 유효 해야 합니다. **SQLRemoveDriverManager** 구성 요소 사용 횟수를 감소 시키기 위해 먼저 호출 해야 합니다. **SQLInstallDriverManager** 구성 요소 사용 횟수를 증가 시키는 다음 호출 해야 합니다. 응용 프로그램 설치 프로그램을 새 파일로 이전 핵심 구성 요소 파일을 바꿔야 합니다. 파일 사용 횟수 동일 하 게, 및 이전 버전 핵심 구성 요소 파일을 사용 하는 다른 응용 프로그램은 이제 사용 하 여 최신 버전 파일입니다.  
  
 ODBC 핵심 구성 요소, 드라이버 및 변환기가 새로 설치한 응용 프로그램 설치 프로그램 순서는 다음 함수 호출 해야: **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLConfigDriver** (으로 *문제점과* ODBC_INSTALL_DRIVER의)을 차례로 **SQLInstallTranslatorEx**합니다. 핵심 구성 요소, 드라이버 및 변환기의 제거, 응용 프로그램 설치 프로그램 순서는 다음 함수 호출 해야: **SQLRemoveTranslator**, **SQLRemoveDriver**, 한 다음 **SQLRemoveDriverManager**합니다. 이 시퀀스에서 이러한 함수를 호출 해야 합니다. 모든 구성 요소를 업그레이드 순서에서 모든 제거 함수를 호출 해야 하 고 시퀀스의 모든 설치 함수 다음 호출 해야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 드라이버를 제거 합니다.|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|드라이버 설치|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|설치 하는 변환기|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|드라이버를 제거합니다.|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|드라이버 관리자를 제거합니다.|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|변환기를 제거합니다.|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
