---
title: SQLInstallTranslatorEx 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslatorEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslatorEx
helpviewer_keywords:
- SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cf52c26bf9e4a26f13a27a0e763fbaa30bd18ec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302094"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 함수
**규칙**  
 버전 출시: ODBC 3.0  
  
 **요약**  
 **SQLInstallTranslatorEx는** 시스템 정보의 Odbcinst.ini 섹션에 번역기에 대한 정보를 추가합니다(HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\ODBC 번역기 레지스트리 키).  
  
 **SQLInstallTranslatorEx의** 기능은 ODBCCONF로 액세스 할 수 [있습니다. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLInstallTranslatorEx(  
     LPCSTR    lpszTranslator,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *lpsz번역기*  
 [입력] 여기에는 번역기를 설명하는 키워드 값 쌍의 이중 null 종료 목록이 포함되어야 합니다. 키워드-값 쌍 구문에 대한 자세한 내용은 [번역기 사양 하위 키를](../../../odbc/reference/install/translator-specification-subkeys.md)참조하십시오.  
  
 **변환기** 및 **설치 설정** 키워드는 *lpszTranslator* 문자열에 포함되어야 합니다. 번역 DLL은 **번역기** 키워드와 함께 나열되고 번역기 설정 DLL은 **설치 키워드와** 함께 나열됩니다. 각 쌍은 NULL 바이트로 종료되고 전체 목록은 NULL 바이트로 종료됩니다. 즉, 두 개의 NULL 바이트가 목록의 끝을 표시합니다. *lpszTranslator의* 형식은 다음과 같습니다.  
  
 \0Translator=*번역기-DLL 파일 이름*\0[설치=*설치-DLL 파일 이름*\0]\0  
  
 *lpszPathIn*  
 [입력] 변환기를 설치할 위치 또는 null 포인터의 전체 경로입니다. *lpszPath가* null 포인터인 경우 변환기가 시스템 디렉터리에 설치됩니다.  
  
 *lpsz패스아웃*  
 [출력] 변환기를 설치해야 하는 대상 디렉터리 경로입니다. 번역기가 설치되지 않은 경우 *lpszPathOut은* *lpszPathIn과*동일합니다. 번역기의 이전 설치가 있는 경우 *lpszPathOut은* 이전 설치의 경로입니다.  
  
 *cb패스아웃맥스*  
 [입력] *lpszPathOut의 길이입니다.*  
  
 *pcb패스아웃*  
 [출력] *lpszPathOut에서*반환할 수 있는 총 바이트 수입니다. 반환할 수 있는 바이트 수가 *cbPathOutMax보다*크거나 같으면 *lpszPathOut의* 출력 경로가 *pcbPathOutMax에서* null 종료 문자를 뺀 값으로 잘립니다. *pcbPathOut* 인수는 null 포인터일 수 있습니다.  
  
 *f요청*  
 [입력] 요청 유형입니다. *fRequest는* 다음 값 중 하나를 포함해야 합니다.  
  
 ODBC_INSTALL_INQUIRY: 번역기를 설치할 수 있는 위치에 대해 문의하십시오.  
  
 ODBC_INSTALL_COMPLETE: 설치 요청을 완료합니다.  
  
 *lpdw사용계산*  
 [출력] 이 함수가 호출된 후 변환기의 사용 횟수입니다.  
  
 응용 프로그램은 사용 수를 설정해서는 안 됩니다. ODBC는 이 수를 유지합니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLInstallTranslatorEx가** FALSE를 반환하는 경우 **SQLInstallerError**를 호출하여 연결된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못된 버퍼 길이|*lpszPathOut* 인수는 출력 경로를 포함할 만큼 충분히 크지 않았습니다. 버퍼에 잘린 경로가 포함되어 있습니다.<br /><br /> *cbPathOutMax* 인수는 0이고 *fRequest* 인수는 ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못된 요청 유형|*fRequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못된 키워드-값 쌍|*lpszTranslator* 인수에는 구문 오류가 포함되어 있습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못된 설치 경로|*lpszPathIn* 인수에 잘못된 경로가 포함되어 있습니다.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못된 매개 변수 시퀀스|*lpszTranslator* 인수에는 키워드 값 쌍 목록이 포함되어 있지 않았습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|레지스트리의 구성 요소 사용 수를 증가하거나 감소시킬 수 없습니다.|설치 프로그램이 변환기의 사용 횟수를 증가시키지 못했습니다.|  
  
## <a name="comments"></a>주석  
 **SQLInstallTranslatorEx는** 번역기만 설치하는 메커니즘을 제공합니다. 이 함수는 실제로 파일을 복사하지 않습니다. 호출 프로그램은 번역기 파일을 복사할 책임이 있습니다.  
  
 **SQLInstallTranslatorEx는** 설치된 번역기에 대한 구성 요소 사용 수를 1로 증가시다. 번역기 버전이 이미 있지만 번역기에 대한 구성 요소 사용 수가 없는 경우 새 구성 요소 사용 횟수 값이 2로 설정됩니다.  
  
 응용 프로그램 설치 프로그램은 변환기 파일을 물리적으로 복사하고 파일 사용 수를 유지 관리합니다. 번역기 파일이 이전에 설치되지 않은 경우 응용 프로그램 설치 프로그램은 파일이나 파일을 복사하고 파일 또는 파일 사용 수를 만들어야 합니다. 파일이 이전에 설치된 경우 설치 프로그램은 파일 사용 횟수를 증가시면 됩니다.  
  
 이전 버전의 번역기가 응용 프로그램에서 이전에 설치한 경우 번역기를 제거한 다음 다시 설치해야 번역기 구성 요소 사용 수가 유효합니다. **SQLRemoveTranslator는** 구성 요소 사용 수를 감소시키기 위해 호출되어야하며 **SQLInstallTranslatorEx는** 구성 요소 사용 수를 증가시키기 위해 호출해야합니다. 응용 프로그램 설치 프로그램은 이전 파일이나 파일을 새 파일로 바꿔야 합니다. 파일 사용 수는 동일하게 유지되며 이전 버전 파일을 사용한 다른 응용 프로그램은 이제 최신 버전을 사용합니다.  
  
 **SQLInstallTranslatorEx에서** *lpszPathOut의* 경로 길이는 2단계 설치 프로세스를 허용하므로 응용 프로그램은 ODBC_INSTALL_INQUIRY 모드의 *fRequest를* 사용하여 **SQLInstallTranslatorEx를** 호출하여 *어떤 cbPathOutMax를* 호출해야 하는지 결정할 수 있습니다. 이렇게 하면 *pcbPathOut* 버퍼에서 사용할 수 있는 총 바이트 수가 반환됩니다. 그런 다음 **SQLInstallTranslatorEx는** ODBC_INSTALL_COMPLETE *fRequest와* *pcbPathOut* 버퍼의 값으로 설정된 *cbPathOutMax* 인수와 null 종료 문자로 호출할 수 있습니다.  
  
 **SQLInstallTranslatorEx에**대한 2단계 모델을 사용하지 않도록 선택한 경우 잘림을 방지하기 위해 대상 디렉터리 경로에 대한 저장소 크기를 stdlib.h에 정의된 값 _MAX_PATH *cbPathOutMax로*설정해야 합니다.  
  
 *fRequest가* ODBC_INSTALL_COMPLETE **경우 SQLInstallTranslatorEx는** *lpszPathOut을* NULL(또는 *cbPathOutMax가* 0)으로 허용하지 않습니다. *fRequest가* ODBC_INSTALL_COMPLETE 경우 반환할 수 있는 바이트 수가 *cbPathOutMax보다*크거나 같을 때 FALSE가 반환되고 그 결과 잘림이 발생합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|기본 번역 옵션 반환|[콘피그 번역기](../../../odbc/reference/syntax/configtranslator-function.md)|  
|번역자 선택|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|번역기 제거|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
