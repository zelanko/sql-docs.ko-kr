---
description: SQLGetTranslator 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d30268c846af4e95298d00edcd13def97c20c77d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421227"
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 함수
**규칙**  
 소개 된 버전: ODBC 2.0  
  
 **요약**  
 **SQLGetTranslator** 사용자가 번역기를 선택할 수 있는 대화 상자를 표시 합니다.  
  
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
 입력 부모 창 핸들입니다.  
  
 *lpszName*  
 [입/출력] 시스템 정보에서 변환기의 이름입니다.  
  
 *cbNameMax*  
 입력 *LpszName* 버퍼의 최대 길이입니다.  
  
 *pcbNameOut*  
 [입/출력] *LpszName*에 전달 되거나 반환 된 총 바이트 수입니다 (null 종결 바이트 제외). 반환 하는 데 사용할 수 있는 바이트 수가 *cbNameMax*보다 크거나 같으면 *lpszName* 의 변환기 이름이 *cbNameMax* 에서 null 종료 문자를 뺀 값으로 잘립니다. *Pcbnameout* 인수는 null 포인터 일 수 있습니다.  
  
 *lpszPath*  
 출력 변환 DLL의 전체 경로입니다.  
  
 *cbPathMax*  
 입력 *LpszPath* 버퍼의 최대 길이입니다.  
  
 *pcbPathOut*  
 출력 *LpszPath*에 반환 된 총 바이트 수입니다 (null 종결 바이트 제외). 반환할 수 있는 바이트 수가 *Cbpathmax*보다 크거나 같으면 *LPSZPATH* 의 변환 DLL 경로가 *cbpathmax* 에서 null 종료 문자를 뺀 값으로 잘립니다. *Pcbpathout* 인수는 null 포인터 일 수 있습니다.  
  
 *pvOption*  
 [출력] 32-비트 번역 옵션입니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고, 실패 하면 FALSE를 반환 하 고, 사용자가 대화 상자를 취소 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetTranslator** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \* pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \* pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*CbNameMax* 또는 *cbpathmax* 인수가 0 보다 작거나 같습니다.|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못 되었습니다.|*HwndParent* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_INVALID_NAME|드라이버 또는 번역기 이름이 잘못 되었습니다.|*LpszName* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 번역기 설치 라이브러리를 로드할 수 없습니다.|변환기 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_INVALID_OPTION|트랜잭션 옵션이 잘못 되었습니다.|*PvOption* 인수에 잘못 된 값이 있습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 *HwndParent* 가 Null 이거나 *lpszName*, *lpszPath*또는 *PVOPTION* 가 null 포인터인 경우 **SQLGetTranslator** 는 FALSE를 반환 합니다. 그렇지 않으면 다음 대화 상자에서 설치 된 번역기의 목록이 표시 됩니다.  
  
 ![변환기 선택 대화 상자](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 *LpszName* 에 올바른 번역기 이름이 포함 된 경우이를 선택 합니다. 그렇지 않으면 \<No Translator> 이 선택 됩니다.  
  
 사용자가를 선택 하는 경우 \<No Translator> *lpszName*, *lpszPath*및 *pvOption* 의 내용은 작업 하지 않습니다. **SQLGetTranslator** 는 *pcbnameout* 및 *pcbnameout* 을 0으로 설정 하 고 TRUE를 반환 합니다.  
  
 사용자가 번역기를 선택 하는 경우 **SQLGetTranslator** 은 변환기의 설치 DLL에서 **configtranslator** 를 호출 합니다. **Configtranslator** 가 FALSE를 반환 하는 경우 **SQLGetTranslator** 는 해당 대화 상자로 돌아갑니다. **Configtranslator** 가 true를 반환 하는 경우 **SQLGetTranslator** 는 선택한 번역기 이름, 경로 및 번역 옵션과 함께 true를 반환 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|번역기 구성|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|번역 특성 가져오기|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|번역 특성 설정|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
