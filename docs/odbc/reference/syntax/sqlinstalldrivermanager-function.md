---
title: SQLInstallDriver관리자 기능 | 마이크로 소프트 문서
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
ms.openlocfilehash: 0788de0493439a360c0446733b31606a02e12422
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302114"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 함수
**규칙**  
 버전 소개: ODBC 1.0: Windows XP 서비스 팩 2, Windows 서버 2003 서비스 팩 1 및 이후 운영 체제에서 더 이상 사용되지 않습니다.  
  
 **요약**  
 **SQLInstallDriverManager** ODBC 핵심 구성 요소의 설치에 대 한 대상 디렉터리의 경로를 반환 합니다. 호출 프로그램은 실제로 드라이버 관리자의 파일을 대상 디렉터리로 복사해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>인수  
 *lpszPath*  
 [출력] 설치 대상 디렉터리 경로입니다.  
  
 *cb패스맥스*  
 [입력] *lpszPath의*길이 . 이 바이트는 _MAX_PATH 바이트 이상이어야 합니다.  
  
 *pcb패스아웃*  
 [출력] *lpszPath에서*반환되는 총 바이트 수(널 종료 바이트 제외). 반환할 수 있는 바이트 수가 *cbPathMax보다*크거나 같으면 *lpszPath의* 경로는 null 종료 문자를 뺀 *cbPathMax로* 잘립니다. *pcbPathOut* 인수는 null 포인터일 수 있습니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLInstallDriverManager** FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못된 버퍼 길이|*lpszPath* 인수는 출력 경로를 포함할 만큼 충분히 크지 않았습니다. 버퍼에 잘린 경로가 포함되어 있습니다.<br /><br /> *cbPathMax* 인수는 _MAX_PATH 미만이었습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|구성 요소 사용량 수를 증가하거나 감소시킬 수 없습니다.|설치 프로그램이 ODBC 핵심 구성 요소 사용 횟수를 증가시키지 못했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLInstallDriverManager는** ODBC 핵심 구성 요소에 대한 경로를 반환하고 시스템 정보의 구성 요소 사용 수를 증가시키기 위해 호출됩니다. 드라이버 관리자 버전이 이미 있지만 드라이버의 구성 요소 사용 수가 없는 경우 새 구성 요소 사용 수 개 값이 2로 설정됩니다.  
  
 응용 프로그램 설치 프로그램은 핵심 구성 요소 파일을 물리적으로 복사하고 파일 사용 수를 유지 관리합니다. 핵심 구성 요소 파일이 이전에 설치되지 않은 경우 응용 프로그램 설치 프로그램에서 파일을 복사하고 파일 사용 수를 만들어야 합니다. 파일이 이전에 설치된 경우 설치 프로그램은 파일 사용 횟수를 증가시입니다.  
  
 이전 버전의 드라이버 관리자가 응용 프로그램 설치 프로그램에서 설치한 경우 핵심 구성 요소를 제거한 다음 다시 설치해야 핵심 구성 요소 사용 수가 유효합니다. **SQLRemoveDriverManager** 먼저 구성 요소 사용 수를 감소 시키기 위해 호출 해야 합니다. 그런 다음 **SQLInstallDriverManager를** 호출하여 구성 요소 사용 수를 증가시켜야 합니다. 응용 프로그램 설치 프로그램은 이전 핵심 구성 요소 파일을 새 파일로 바꿔야 합니다. 파일 사용 수는 동일하게 유지되며 이전 버전 핵심 구성 요소 파일을 사용한 다른 응용 프로그램은 이제 최신 버전 파일을 사용합니다.  
  
 ODBC 핵심 구성 요소, 드라이버 및 번역기를 새로 설치할 때 응용 프로그램 설치 프로그램은 ODBC_INSTALL_DRIVER **다음** **SQLInstallDriverEx**함수를 순서대로 **SQLConfigDriver** 호출해야 합니다. *fRequest* **SQLInstallTranslatorEx** 핵심 구성 요소, 드라이버 및 번역기를 제거할 때 응용 프로그램 설치 프로그램은 **다음**함수를 순서대로 **SQLRemoveDriver**호출해야 합니다. **SQLRemoveDriverManager** 이러한 함수는 이 시퀀스에서 호출해야 합니다. 모든 구성 요소를 업그레이드할 때 모든 제거 함수를 순서대로 호출한 다음 모든 설치 함수를 순서대로 호출해야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|드라이버 추가, 수정 또는 제거|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|드라이버 설치|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|번역기 설치|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|드라이버 제거|[SQLRemove드라이버](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|드라이버 관리자 제거|[SQLRemove드라이버관리자](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|번역기 제거|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
