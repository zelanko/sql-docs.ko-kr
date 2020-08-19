---
description: SQLInstallDriverManager 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b39e2c9304fd47394617d48f22ac91284af1b45d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421177"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 함수
**규칙**  
 소개 된 버전: ODBC 1.0: Windows XP 서비스 팩 2, Windows Server 2003 서비스 팩 1 이상 운영 체제에서 사용 되지 않음  
  
 **요약**  
 **Sqlinstalldrivermanager** 는 ODBC 핵심 구성 요소를 설치할 대상 디렉터리의 경로를 반환 합니다. 호출 프로그램은 실제로 드라이버 관리자의 파일을 대상 디렉터리에 복사 해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>인수  
 *lpszPath*  
 출력 설치 대상 디렉터리의 경로입니다.  
  
 *cbPathMax*  
 입력 *LpszPath*의 길이입니다. 이는 _MAX_PATH 바이트 이상 이어야 합니다.  
  
 *pcbPathOut*  
 출력 *LpszPath*에 반환 된 총 바이트 수입니다 (null 종결 바이트 제외). 반환할 수 있는 바이트 수가 *Cbpathmax*보다 크거나 같으면 *LpszPath* 의 경로가 *cbpathmax* 에서 null 종료 문자를 뺀 값으로 잘립니다. *Pcbpathout* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlinstalldrivermanager** 가 FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 연결 된 * \* pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \* pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*LpszPath* 인수가 출력 경로를 포함할 만큼 크지 않습니다. 버퍼는 잘린 경로를 포함 합니다.<br /><br /> *Cbpathmax* 인수가 _MAX_PATH 보다 작은 경우|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|구성 요소 사용 횟수를 증가 시키거나 감소 시킬 수 없습니다.|설치 관리자가 ODBC 핵심 구성 요소 사용 횟수를 증가 하지 못했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **Sqlinstalldrivermanager** 는 ODBC core 구성 요소에 대 한 경로를 반환 하 고 시스템 정보의 구성 요소 사용 수를 증가 시키기 위해 호출 됩니다. 드라이버 관리자의 버전이 이미 있지만 드라이버의 구성 요소 사용 횟수가 존재 하지 않는 경우 새 구성 요소 사용 횟수 값은 2로 설정 됩니다.  
  
 응용 프로그램 설치 프로그램은 핵심 구성 요소 파일을 물리적으로 복사 하 고 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. 핵심 구성 요소 파일을 이전에 설치 하지 않은 경우 응용 프로그램 설치 프로그램에서 파일을 복사 하 고 파일 사용 횟수를 만들어야 합니다. 파일이 이전에 설치 된 경우에는 설치 프로그램에서 단순히 파일 사용 횟수를 증가 시킵니다.  
  
 이전 버전의 드라이버 관리자를 응용 프로그램 설치 프로그램에서 이전에 설치한 경우 핵심 구성 요소를 제거한 다음 다시 설치 하 여 핵심 구성 요소 사용 횟수가 올바른지 여부를 지정 해야 합니다. 구성 요소 사용 횟수를 감소 시키려면 **SQLRemoveDriverManager** 를 먼저 호출 해야 합니다. 그런 다음 구성 요소 사용 횟수를 증가 시키기 위해 **Sqlinstalldrivermanager** 를 호출 해야 합니다. 응용 프로그램 설치 프로그램은 이전 핵심 구성 요소 파일을 새 파일로 바꾸어야 합니다. 파일 사용 횟수는 동일 하 게 유지 되 고 이전 버전의 핵심 구성 요소 파일을 사용 하는 다른 응용 프로그램은 이제 최신 버전 파일을 사용 합니다.  
  
 ODBC 핵심 구성 요소, 드라이버 및 번역기를 새로 설치 하는 경우 응용 프로그램 설치 프로그램에서 다음 함수를 순서 대로 호출 해야 합니다. **Sqlinstalldrivermanager**, **sqlinstalldrivermanager**, **SQLConfigDriver** (ODBC_INSTALL_DRIVER의 *frequest* ), **SQLInstallTranslatorEx**. 핵심 구성 요소, 드라이버 및 번역기를 제거 하는 경우 응용 프로그램 설치 프로그램은 **SQLRemoveTranslator**, **SQLRemoveDriver**및 **SQLRemoveDriverManager**함수를 차례로 호출 해야 합니다. 이러한 함수는이 시퀀스에서 호출 해야 합니다. 모든 구성 요소를 업그레이드 하는 경우 모든 제거 기능을 순서 대로 호출 해야 합니다. 그런 다음 모든 설치 기능을 순서 대로 호출 해야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|드라이버 추가, 수정 또는 제거|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|드라이버 설치|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|번역기 설치|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|드라이버 제거|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|드라이버 관리자를 제거 하는 중|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|번역기 제거|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
