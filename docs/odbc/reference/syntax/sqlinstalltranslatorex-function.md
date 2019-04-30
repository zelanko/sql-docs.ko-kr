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
manager: craigg
ms.openlocfilehash: 276b8627588bcd3472c12564db1e8c6e6af1ef2b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242321"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 함수
**규칙**  
 도입 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLInstallTranslatorEx** 변환기에 대 한 정보 시스템 정보 (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST Odbcinst.ini 섹션 추가. INI\ODBC 변환기 레지스트리 키)입니다.  
  
 기능의 **SQLInstallTranslatorEx** 사용 하 여 액세스할 수도 있습니다 [ODBCCONF 합니다. EXE](../../../odbc/odbcconf-exe.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 이 변환기를 설명 하는 키워드 / 값 쌍의 이중으로 null로 끝나는 목록이 있어야 합니다. 키워드-값 쌍 구문에 대 한 자세한 내용은 참조 하세요. [변환기 사양 서브 키](../../../odbc/reference/install/translator-specification-subkeys.md)합니다.  
  
 **Translator** 하 고 **설치** 키워드에 포함 되어야 합니다는 *lpszTranslator* 문자열입니다. 변환 DLL와 함께 나열 됩니다는 **Translator** 키워드 및 변환기 설치 DLL이 함께 나열 합니다 **설치** 키워드. 각 쌍을 NULL 바이트를 사용 하 여 종료 됩니다 하 고 전체 목록을 NULL 바이트를 사용 하 여 종료 됩니다. (즉, 두 개의 NULL 바이트의 끝을 표시 목록입니다.) 형식은 *lpszTranslator* 는 다음과 같습니다.  
  
 \0Translator=*translator-DLL-filename*\0[Setup=*setup-DLL-filename*\0]\0  
  
 *lpszPathIn*  
 [입력] 설치할 변환기 인 또는 null 포인터의 전체 경로입니다. 하는 경우 *lpszPath* 가 null 포인터인 경우 번역은 시스템 디렉터리에 설치 됩니다.  
  
 *lpszPathOut*  
 [출력] 변환기를 설치할 대상 디렉터리의 경로입니다. 변환기 설치 되어 있지 않은 경우 *lpszPathOut* 와 같습니다 *lpszPathIn*합니다. Translator의 이전 설치가 있는 경우 *lpszPathOut* 이전 설치의 경로입니다.  
  
 *cbPathOutMax*  
 [입력] 길이가 *lpszPathOut 합니다.*  
  
 *pcbPathOut*  
 [출력] 반환할 사용 가능한 바이트의 총 *lpszPathOut*합니다. 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *cbPathOutMax*, 출력 경로 *lpszPathOut* 잘립니다 *pcbPathOutMax* 빼기는 null 종료 문자입니다. 합니다 *pcbPathOut* 인수로 null 포인터를 사용할 수 있습니다.  
  
 *fRequest*  
 [입력] 요청 유형입니다. *문제점과* 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_INSTALL_INQUIRY: 변환기를 설치할 수 있는지 문의 합니다.  
  
 ODBC_INSTALL_COMPLETE: 설치 요청을 완료 합니다.  
  
 *lpdwUsageCount*  
 [출력] 이 함수를 호출한 후 변환기의 사용 횟수입니다.  
  
 응용 프로그램 사용 횟수를 설정 하지 않아야 합니다. ODBC는이 개수를 유지 합니다.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLInstallTranslatorEx** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|합니다 *lpszPathOut* 인수가 출력 경로 포함 하기에 충분 합니다. 버퍼의 잘린된 경로 포함합니다.<br /><br /> 합니다 *cbPathOutMax* 인수가 0, 및 *문제점과* 인수가 ODBC_INSTALL_COMPLETE 합니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|합니다 *문제점과* 인수 중 하나 였습니다.<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|합니다 *lpszTranslator* 인수 구문 오류를 포함 합니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|합니다 *lpszPathIn* 인수에 잘못 된 경로 포함 합니다.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못 된 매개 변수 순서|합니다 *lpszTranslator* 인수 키워드-값 쌍의 목록이 없습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|증가 하거나 레지스트리 구성 요소 사용 횟수를 감소 시킬 수 없습니다.|설치 관리자는 변환기의 사용 횟수를 증가 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLInstallTranslatorEx** 변환기만 설치 하는 메커니즘을 제공 합니다. 이 함수는 모든 파일을 실제로 복사 하지 않습니다. 호출 프로그램이 translator 파일을 복사 하는 일을 담당 합니다.  
  
 **SQLInstallTranslatorEx** 설치 변환기에 대 한 구성 요소 사용 횟수를 1 씩 증가 합니다. 변환기의 버전이 이미 있는 경우 변환기에 대 한 구성 요소 사용 수 없는 경우, 새 구성 요소 사용 개수 값을 2로 설정 됩니다.  
  
 응용 프로그램 설치 프로그램은 translator 파일을 복사 하는 물리적으로 및 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. Translator 파일을 이전에 설치 되지 않은 경우 응용 프로그램 설치 프로그램 파일 또는 파일 복사를 업데이트 하 고 사용 횟수가 파일 또는 파일을 생성 해야. 파일에 이전에 설치 된 경우 설치 프로그램 파일 사용 횟수를 단순히 증가 합니다.  
  
 변환기의 이전 버전을 응용 프로그램에서 설치 했던 것 경우 변환기를 제거 하 고 다시 설치 변환기 구성 요소 사용 횟수는 유효한 해야 합니다. **SQLRemoveTranslator** 구성 요소 사용 횟수를 감소 시키기 위해 호출 해야 차례로 **SQLInstallTranslatorEx** 구성 요소 사용 횟수를 증가 시킬를 호출 해야 합니다. 응용 프로그램 설치 프로그램을 새 파일로 이전 파일 또는 파일을 대체 해야 합니다. 파일 사용 횟수를 동일 하 게 유지 됩니다 및 이전 버전 파일을 사용 하는 다른 응용 프로그램에서 이제 최신 버전을 사용 합니다.  
  
 경로의 길이 *lpszPathOut* 에 **SQLInstallTranslatorEx** 응용 프로그램 항목을 확인할 수 있도록 2 단계 설치 프로세스에 대 한 허용 *cbPathOutMax* 해야 호출 하 여 수 **SQLInstallTranslatorEx** 사용 하 여는 *문제점과* ODBC_INSTALL_INQUIRY 모드입니다. 사용 가능한 바이트의 총 수를 반환은이 *pcbPathOut* 버퍼입니다. **SQLInstallTranslatorEx** 사용 하 여 호출할 수 있습니다는 *문제점과* ODBC_INSTALL_COMPLETE의 및 *cbPathOutMax* 인수를 값으로 설정 된 *pcbPathOut* 버퍼와 null 종료 문자입니다.  
  
 에 대 한 2 단계 모델을 사용 하도록 하지 않으려는 경우 **SQLInstallTranslatorEx**를 설정 해야 *cbPathOutMax*,으로 대상 디렉터리로 값 _max_path(256의 경로 대 한 저장소의 크기를 정의 하는 잘림을 방지 하기 위해 Stdlib.h에 정의 합니다.  
  
 때 *문제점과* ODBC_INSTALL_COMPLETE, 됩니다 **SQLInstallTranslatorEx** 없도록 *lpszPathOut* NULL로 (또는 *cbPathOutMax* 0으로). 하는 경우 *문제점과* ODBC_INSTALL_COMPLETE를 반환할 수 있는 바이트 수가 보다 크거나 같은 경우 FALSE 반환 됩니다 *cbPathOutMax*, 결과 사용 하 여 잘림이 발생 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|기본 변환 옵션을 반환합니다.|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|변환기를 선택합니다.|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|변환기를 제거합니다.|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
