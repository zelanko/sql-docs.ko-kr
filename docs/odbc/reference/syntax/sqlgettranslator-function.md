---
title: SQLGetTranslator 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTranslator
helpviewer_keywords:
- SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcd5aeebab8539b8b94db56ff30892f4a7dbbac1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303274"
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 함수
**규칙**  
 버전 출시: ODBC 2.0  
  
 **요약**  
 **SQLGetTranslator는** 사용자가 번역기를 선택할 수 있는 대화 상자를 표시합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLGetTranslator(  
     HWND      hwndParent,  
     LPSTR     lpszName,  
     WORD      cbNameMax,  
     WORD *    pcbNameOut,  
     LPSTR     lpszPath,  
     WORD      cbPathMax,  
     WORD *    pcbPathOut,  
     DWORD *   pvOption);  
```  
  
## <a name="arguments"></a>인수  
 *hwndParent*  
 [입력] 부모 창 핸들입니다.  
  
 *lpszName*  
 [입력/출력] 시스템 정보에서 번역기의 이름입니다.  
  
 *cb네임맥스*  
 [입력] *lpszName* 버퍼의 최대 길이입니다.  
  
 *pcbNameOut*  
 [입력/출력] *lpszName에서*전달되거나 반환된 총 바이트 수(널 종료 바이트 제외). 반환할 수 있는 바이트 수가 *cbNameMax보다*크거나 같으면 *lpszName의* 번역기 이름이 *cbNameMax에서* null 종료 문자를 뺀 값으로 잘립니다. *pcbNameOut* 인수는 null 포인터일 수 있습니다.  
  
 *lpszPath*  
 [출력] 번역 DLL의 전체 경로입니다.  
  
 *cb패스맥스*  
 [입력] *lpszPath* 버퍼의 최대 길이입니다.  
  
 *pcb패스아웃*  
 [출력] *lpszPath에서*반환되는 총 바이트 수(널 종료 바이트 제외). 반환할 수 있는 바이트 수가 *cbPathMax보다*크거나 같으면 *lpszPath의* 번역 DLL 경로가 *cbPathMax에서* null 종료 문자를 뺀 값으로 잘립니다. *pcbPathOut* 인수는 null 포인터일 수 있습니다.  
  
 *pvoption*  
 [출력] 32비트 변환 옵션.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE, 실패하거나 사용자가 대화 상자를 취소하는 경우 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetTranslator** FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못된 버퍼 길이|*cbNameMax* 또는 *cbPathMax* 인수는 0보다 적거나 동일했습니다.|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못되었습니다.|*hwndParent* 인수가 유효하지 않거나 NULL입니다.|  
|ODBC_ERROR_INVALID_NAME|잘못된 드라이버 또는 번역기 이름|*lpszName* 인수가 잘못되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 번역기 설정 라이브러리를 로드할 수 없습니다.|변환기 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_INVALID_OPTION|잘못된 트랜잭션 옵션|*pvOption* 인수에 잘못된 값이 포함되어 있습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 *hwndParent가* null이거나 *lpszName,* *lpszPath*또는 *pvOption이* null 포인터인 경우 **SQLGetTranslator는** FALSE를 반환합니다. 그렇지 않으면 다음 대화 상자에 설치된 번역기 목록이 표시됩니다.  
  
 ![변환기 선택 대화 상자](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 *lpszName* 유효한 번역기 이름이 포함 된 경우 선택 됩니다. 그렇지 \<않으면 번역기> 선택되지 않습니다.  
  
 사용자가> \<번역사 없음을 선택하면 *lpszName, lpszPath*및 *pvOption의* 내용은 터치되지 않습니다. *lpszPath* **SQLGetTranslator는** *pcbNameOut* 및 *pcbPathOut을* 0으로 설정하고 TRUE를 반환합니다.  
  
 사용자가 번역기를 선택하면 **SQLGetTranslator가** 번역기의 설정 DLL에서 **ConfigTranslator를** 호출합니다. **ConfigTranslator가** FALSE를 반환하면 **SQLGetTranslator가** 대화 상자로 돌아갑니다. **ConfigTranslatorTRUE를** 반환하는 경우 **SQLGetTranslator는** 선택한 번역기 이름, 경로 및 번역 옵션과 함께 TRUE를 반환합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|번역기 구성|[콘피그 번역기](../../../odbc/reference/syntax/configtranslator-function.md)|  
|번역 특성 얻기|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|번역 특성 설정|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
