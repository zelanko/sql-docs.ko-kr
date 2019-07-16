---
title: SQLGetTranslator 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f769d3c5b2dcfe5d2aa8a431695cb18a52893b91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030656"
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 함수
**규칙**  
 도입 된 버전: ODBC 2.0  
  
 **요약**  
 **SQLGetTranslator** 사용자 변환기를 선택할 수 있는 대화 상자를 표시 합니다.  
  
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
 [입력/출력] 시스템 정보에서 변환기의 이름입니다.  
  
 *cbNameMax*  
 [입력] 최대 길이 *lpszName* 버퍼입니다.  
  
 *pcbNameOut*  
 [입력/출력] 총 바이트 (null 종료 바이트 제외)에서 반환 된 지났거나 *lpszName*합니다. 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *cbNameMax*, translator 이름을 *lpszName* 잘립니다 *cbNameMax* 빼기는 null 종료 문자입니다. 합니다 *pcbNameOut* 인수로 null 포인터를 사용할 수 있습니다.  
  
 *lpszPath*  
 [출력] 변환 DLL의 전체 경로입니다.  
  
 *cbPathMax*  
 [입력] 최대 길이 *lpszPath* 버퍼입니다.  
  
 *pcbPathOut*  
 [출력] 총 바이트 (null 종료 바이트 제외)에서 반환 된 *lpszPath*합니다. 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *cbPathMax*, 번역 DLL 경로 *lpszPath* 잘립니다 *cbPathMax* 빼기는 null 종료 문자입니다. 합니다 *pcbPathOut* 인수로 null 포인터를 사용할 수 있습니다.  
  
 *pvOption*  
 [출력] 32 비트 변환 옵션입니다.  
  
## <a name="returns"></a>반환 값  
 함수가 실패 한 경우 또는 사용자가 대화 상자를 취소 하는 경우 성공적이 고 FALSE 인 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetTranslator** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|합니다 *cbNameMax* 하거나 *cbPathMax* 인수가 0 보다 작거나 합니다.|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|합니다 *hwndParent* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_INVALID_NAME|잘못 된 드라이버 또는 변환기 이름|합니다 *lpszName* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 translator 설치 라이브러리를 로드할 수 없습니다.|변환기 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_INVALID_OPTION|잘못 된 트랜잭션 옵션|합니다 *pvOption* 인수에 잘못 된 값을 포함 합니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 하는 경우 *hwndParent* 가 null 이거나 *lpszName*를 *lpszPath*, 또는 *pvOption* 가 null 포인터인 경우 **SQLGetTranslator** FALSE를 반환 합니다. 이 고, 그렇지 다음 대화 상자에서 설치 된 변환기 목록을 표시합니다.  
  
 ![변환기 대화 상자를 선택](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 하는 경우 *lpszName* 유효한 translator 이름을 포함을 선택 합니다. 이 고, 그렇지 \<아니요 Translator >을 선택 합니다.  
  
 사용자가 선택 하는 경우 \<No Translator >, 내용의 *lpszName*를 *lpszPath*, 및 *pvOption* 는 그대로 유지 합니다. **SQLGetTranslator** 설정 *pcbNameOut* 하 고 *pcbPathOut* 0과 TRUE 반환 합니다.  
  
 사용자는 translator 싶다면 **SQLGetTranslator** 호출 **ConfigTranslator** 변환기 설치 DLL에서에서. 하는 경우 **ConfigTranslator** FALSE를 반환 **SQLGetTranslator** 해당 대화 상자로 돌아갑니다. 하는 경우 **ConfigTranslator** TRUE를 반환 **SQLGetTranslator** 선택한 translator 이름, 경로 및 변환 옵션을 함께 TRUE를 반환 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|변환기를 구성합니다.|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|변환 특성을 가져오기|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|변환 특성을 설정합니다.|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
