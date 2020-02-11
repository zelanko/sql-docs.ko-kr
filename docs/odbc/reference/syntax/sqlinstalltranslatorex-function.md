---
title: SQLInstallTranslatorEx 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43acc6708b5df71893c2c6b7658ca99bfb73f616
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019002"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 함수
**규칙**  
 소개 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLInstallTranslatorEx** 시스템 정보의 odbcinst.ini 섹션에 변환기에 대 한 정보를 추가 합니다 (HKEY_LOCAL_MACHINE \software\odbc\odbcinst. INI\ODBC 번역가 레지스트리 키).  
  
 ODBCCONF를 사용 하 여 **SQLInstallTranslatorEx** 의 기능에 액세스할 수도 있습니다 [. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 *lpszTranslator*  
 입력 여기에는 변환기를 설명 하는 키워드-값 쌍의 이중 null 종료 목록이 포함 되어야 합니다. 키워드-값 쌍 구문에 대 한 자세한 내용은 [Translator 사양 하위 키](../../../odbc/reference/install/translator-specification-subkeys.md)를 참조 하세요.  
  
 *LpszTranslator* 문자열에 **Translator** 및 **Setup** 키워드를 포함 해야 합니다. 변환 DLL은 **translator** 키워드와 함께 나열 되며, TRANSLATOR 설치 Dll은 **setup** 키워드와 함께 나열 됩니다. 각 쌍은 NULL 바이트로 종료 되며 전체 목록이 NULL 바이트로 종료 됩니다. 즉, 두 개의 NULL 바이트가 목록의 끝을 표시 합니다. *LpszTranslator* 형식은 다음과 같습니다.  
  
 \0Translator =*translator-filename*\ 0 [setup =*setup-dll-filename*\ 0] \ 0  
  
 *lpszPathIn*  
 입력 변환기를 설치할 전체 경로 이거나 null 포인터입니다. *LpszPath* 가 null 포인터인 경우 변환기가 시스템 디렉터리에 설치 됩니다.  
  
 *lpszPathOut*  
 출력 변환기를 설치 해야 하는 대상 디렉터리의 경로입니다. 변환기를 설치 하지 않은 경우 *lpszPathOut* 은 *lpszPathIn*와 동일 합니다. 이전에 설치 된 번역기가 있는 경우 *lpszPathOut* 은 이전 설치의 경로입니다.  
  
 *cbPathOutMax*  
 입력 LpszPathOut의 길이 *입니다.*  
  
 *pcbPathOut*  
 출력 *LpszPathOut*에서 반환할 수 있는 총 바이트 수입니다. 반환할 수 있는 바이트 수가 *Cbpathoutmax*보다 크거나 같으면 *lpszPathOut* 의 출력 경로가 *pcbpathoutmax* 에서 null 종료 문자를 뺀 값으로 잘립니다. *Pcbpathout* 인수는 null 포인터 일 수 있습니다.  
  
 *fRequest*  
 입력 요청 유형입니다. *Frequest* 는 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_INSTALL_INQUIRY: 번역기를 설치할 수 있는 위치를 조회 합니다.  
  
 ODBC_INSTALL_COMPLETE: 설치 요청을 완료 합니다.  
  
 *lpdwUsageCount*  
 출력 이 함수가 호출 된 후의 변환기 사용 횟수입니다.  
  
 응용 프로그램은 사용 횟수를 설정 하면 안 됩니다. ODBC는이 수를 유지 합니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLInstallTranslatorEx** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*LpszPathOut* 인수가 출력 경로를 포함할 만큼 크지 않습니다. 버퍼는 잘린 경로를 포함 합니다.<br /><br /> *Cbpathoutmax* 인수가 0이 고 *frequest* 인수가 ODBC_INSTALL_COMPLETE 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못 된 요청 유형|*Frequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|*LpszTranslator* 인수에 구문 오류가 포함 되어 있습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|*LpszPathIn* 인수에 잘못 된 경로가 포함 되어 있습니다.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못 된 매개 변수 시퀀스|*LpszTranslator* 인수에 키워드-값 쌍의 목록이 없습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|레지스트리의 구성 요소 사용 횟수를 증가 시키거나 감소 시킬 수 없습니다.|변환기의 사용 횟수를 증가 시 설치 관리자가 실패 했습니다.|  
  
## <a name="comments"></a>주석  
 **SQLInstallTranslatorEx** 은 번역기만 설치 하는 메커니즘을 제공 합니다. 이 함수는 실제로 파일을 복사 하지 않습니다. 호출 프로그램은 변환기 파일 복사를 담당 합니다.  
  
 **SQLInstallTranslatorEx** 는 설치 된 변환기에 대 한 구성 요소 사용 횟수를 1 씩 증가 시킵니다. 변환기의 버전이 이미 있지만 변환기의 구성 요소 사용 횟수가 없는 경우 새 구성 요소 사용 횟수 값은 2로 설정 됩니다.  
  
 응용 프로그램 설치 프로그램은 변환기 파일을 물리적으로 복사 하 고 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. 변환기 파일이 이전에 설치 되지 않은 경우 응용 프로그램 설치 프로그램에서 파일을 복사 하 고 파일 또는 파일 사용 횟수를 만들어야 합니다. 파일이 이전에 설치 된 경우에는 설치 프로그램에서 단순히 파일 사용 횟수를 증가 시킵니다.  
  
 이전 버전의 변환기가 이전에 응용 프로그램에 의해 설치 된 경우 변환기를 제거한 다음 다시 설치 하 여 변환기 구성 요소 사용 횟수가 올바른지 여부를 지정 해야 합니다. **SQLRemoveTranslator** 를 호출 하 여 구성 요소 사용 횟수를 감소 시킨 다음 **SQLInstallTranslatorEx** 를 호출 하 여 구성 요소 사용 횟수를 증가 시켜야 합니다. 응용 프로그램 설치 프로그램에서 이전 파일을 새 파일로 바꾸어야 합니다. 파일 사용 횟수는 동일 하 게 유지 되 고 이전 버전 파일을 사용 하는 다른 응용 프로그램은 이제 최신 버전을 사용 합니다.  
  
 **SQLInstallTranslatorEx** 의 *lpszPathOut* 에 있는 경로 길이는 2 단계 설치 프로세스를 허용 하므로 응용 프로그램은 ODBC_INSTALL_INQUIRY 모드의 *Frequest* 를 사용 하 여 **SQLInstallTranslatorEx** 를 호출 하 여 *cbpathoutmax* 를 결정할 수 있습니다. 그러면 *Pcbpathout* 버퍼에서 사용할 수 있는 총 바이트 수가 반환 됩니다. 그런 다음 ODBC_INSTALL_COMPLETE의 *Frequest* 로 설정 하 고 *Cbpathoutmax* 인수를 *pcbpathout* 버퍼의 값과 null 종료 문자를 더한 값으로 설정 하 여 **SQLInstallTranslatorEx** 를 호출할 수 있습니다.  
  
 **SQLInstallTranslatorEx**에 대해 2 단계 모델을 사용 하지 않도록 선택 하는 경우에는 stdlib.h에 정의 된 대로 대상 디렉터리의 경로에 대 한 저장소 크기를 정의 하는 *Cbpathoutmax*를에 정의 된 _MAX_PATH 값으로 설정 하 여 잘라내기가 발생 하지 않도록 해야 합니다.  
  
 *Frequest* 가 ODBC_INSTALL_COMPLETE 되 면 **SQLInstallTranslatorEx** 에서는 *LpszPathOut* 가 NULL (또는 *cbpathoutmax* 가 0 일 수 있음) 일 수 없습니다. *Frequest* 가 ODBC_INSTALL_COMPLETE 인 경우 반환할 수 있는 바이트 수가 *Cbpathoutmax*보다 크거나 같은 경우에는 잘림이 발생 하므로 FALSE가 반환 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|기본 번역 옵션 반환|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|번역기 선택|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|번역기 제거|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
