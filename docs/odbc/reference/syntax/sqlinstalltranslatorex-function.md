---
title: SQLInstallTranslatorEx 함수 | Microsoft Docs
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
- SQLInstallTranslatorEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslatorEx
helpviewer_keywords:
- SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bf6eda5909aa7cec78a2c23e35126c90f566117
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 함수
**규칙**  
 ODBC 3.0 도입 된 버전:  
  
 **요약**  
 **SQLInstallTranslatorEx** 시스템 정보 (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST Odbcinst.ini 섹션에는 변환기에 대 한 정보를 추가 합니다. INI\ODBC 변환기가 레지스트리 키)입니다.  
  
 기능 **SQLInstallTranslatorEx** 로 액세스할 수도 [ODBCCONF 합니다. EXE](../../../odbc/odbcconf-exe.md)합니다.  
  
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
 [입력] 변환기를 설명 하는 키워드 / 값 쌍의 이중으로 null로 끝나는 목록을 포함 해야 합니다. 키워드-값 쌍 구문에 대 한 자세한 내용은 참조 [변환기 사양 하위 키](../../../odbc/reference/install/translator-specification-subkeys.md)합니다.  
  
 **변환기** 및 **설치** 키워드에 포함 되어야 합니다는 *lpszTranslator* 문자열입니다. DLL이 함께 나열 번역은 **변환기** 키워드 및 DLL이 함께 나열 변환기 설치는 **설치** 키워드입니다. 각 쌍에 NULL 바이트가으로 종료 되 고 전체 목록에 NULL 바이트가로 종료 됩니다. (즉, 두 개의 NULL 바이트의 끝을 표시 목록입니다.) 형식은 *lpszTranslator* 는 다음과 같습니다.  
  
 \0Translator=*변환기-DLL-filename*\0[Setup=*설치 프로그램-DLL-filename*\0]\0  
  
 *lpszPathIn*  
 [입력] 설치 하는 위치 또는 null 포인터의 전체 경로입니다. 경우 *lpszPath* 가 null 포인터는 변환기가 시스템 디렉터리에 설치 됩니다.  
  
 *lpszPathOut*  
 [출력] 변환기를 설치할 대상 디렉터리의 경로입니다. 변환기 설치 되어 있지 않은 경우 *lpszPathOut* 동일 *lpszPathIn*합니다. 변환기가 사전 설치 있으면 *lpszPathOut* 이전 설치의 경로입니다.  
  
 *cbPathOutMax*  
 [입력] 길이 *lpszPathOut 합니다.*  
  
 *pcbPathOut*  
 [출력] 반환 하려면 사용 가능한 바이트의 총 수 *lpszPathOut*합니다. 보다 크거나 반환에 사용할 수 있는 바이트 수가 *cbPathOutMax*, 출력 경로의 *lpszPathOut* 잘립니다 *pcbPathOutMax* 뺀는 null 종료 문자입니다. *pcbPathOut* 인수는 null 포인터 일 수 있습니다.  
  
 *문제점과*  
 [입력] 요청의 유형입니다. *문제점과* 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_INSTALL_INQUIRY: 조회는 변환기를 설치할 수 있습니다.  
  
 ODBC_INSTALL_COMPLETE: 설치 요청을 완료 합니다.  
  
 *lpdwUsageCount*  
 [출력] 이 함수를 호출한 후 변환기의 사용 횟수입니다.  
  
 응용 프로그램 사용 횟수를 설정 해야 합니다. ODBC는이 개수를 유지 합니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLInstallTranslatorEx** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*lpszPathOut* 인수 출력 경로 포함할 수 없습니다. 버퍼의 잘린된 경로 포함합니다.<br /><br /> *cbPathOutMax* 되었습니다. 0, 인수 및 *문제점과* ODBC_INSTALL_COMPLETE 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|*문제점과* 인수는 다음 중 하나 였습니다.<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|*lpszTranslator* 인수에 구문 오류가 포함 되어 있습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|*lpszPathIn* 인수는 잘못 된 경로 포함 합니다.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못 된 매개 변수 순서|*lpszTranslator* 인수 키워드-값 쌍의 목록이 없습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|증가 하거나 레지스트리의 구성 요소 사용 횟수를 감소 시킬 수 없습니다.|설치 관리자는 변환기 사용 횟수를 증가 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 **SQLInstallTranslatorEx** 변환기만 설치 하는 메커니즘을 제공 합니다. 이 함수 실제로 파일을 복사 하지 않습니다. 호출 프로그램은 변환기 파일을 복사 하는 일을 담당 합니다.  
  
 **SQLInstallTranslatorEx** 설치 된 변환기에 대 한 구성 요소 사용 횟수를 1 씩 증가 합니다. 변환기의 버전이 이미 변환기에 대 한 구성 요소의 사용 횟수가 존재 하지 않는 경우 새 구성 요소 사용 개수 값을 2로 설정 됩니다.  
  
 응용 프로그램 설치 프로그램은 변환기 파일을 복사 하는 물리적으로 및 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. 변환기 파일 이전에 설치 되지 않은 경우 응용 프로그램 설치 프로그램 파일 복사한 해야 사용 횟수 파일 또는 파일을 만듭니다. 파일이 이전에 설치 된 경우 설치 프로그램 파일 사용 횟수를 단순히 증가 합니다.  
  
 변환기의 이전 버전을 설치 했던 응용 프로그램에서 경우 변환기를 제거 하 고 다시 설치 된 변환기 구성 요소 사용 횟수는 유효 해야 합니다. **SQLRemoveTranslator** 구성 요소 사용 횟수를 감소 시키기 위해 호출 해야 하 고 다음 **SQLInstallTranslatorEx** 구성 요소 사용 수를 증가 호출 해야 합니다. 응용 프로그램 설치 프로그램을 새 파일로 이전 파일 또는 파일을 대체 해야 합니다. 파일 사용 횟수 동일 하 게, 및 이전 버전 파일을 사용 하는 다른 응용 프로그램은 이제 사용 하 여 최신 버전입니다.  
  
 에 경로의 길이가 *lpszPathOut* 에 **SQLInstallTranslatorEx** 응용 프로그램 기능을 결정할 수 있도록 2 단계 설치 프로세스에 대 한 허용 *cbPathOutMax* 해야 호출 하 여 수 **SQLInstallTranslatorEx** 와 *문제점과* ODBC_INSTALL_INQUIRY 모드입니다. 이에서 사용 가능한 바이트의 총 수를 반환 된 *pcbPathOut* 버퍼입니다. **SQLInstallTranslatorEx** 없이 호출할 수는 *문제점과* ODBC_INSTALL_COMPLETE의 및 *cbPathOutMax* 인수에 값으로 설정 된 *pcbPathOut* 버퍼와 null 종료 문자입니다.  
  
 2 단계에 대 한 모델을 사용 하지 않으려는 경우 **SQLInstallTranslatorEx**를 설정 해야 *cbPathOutMax*,으로 값 _MAX_PATH에 대상 디렉터리의 경로 대 한 저장소의 크기를 정의 하는 잘림을 방지 하기 위해 Stdlib.h에 정의 합니다.  
  
 때 *문제점과* ODBC_INSTALL_COMPLETE은 **SQLInstallTranslatorEx** 하지 못하도록 *lpszPathOut* NULL로 (또는 *cbPathOutMax* 0으로). 경우 *문제점과* ODBC_INSTALL_COMPLETE 이면 FALSE가 반환 반환에 사용할 수 있는 바이트 수가 보다 크거나 *cbPathOutMax*, 결과 함께 잘림이 발생 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|기본 변환 옵션을 반환합니다.|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|변환기를 선택합니다.|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|변환기를 제거합니다.|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
