---
title: 구성 번역기 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigTranslator
helpviewer_keywords:
- ConfigTranslator [ODBC]
ms.assetid: 7c22f07e-36de-425b-aa67-e32a84afae92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb2f26f87854d74a217885010014633963472787
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306034"
---
# <a name="configtranslator-function"></a>ConfigTranslator 함수
**규칙**  
 버전 출시: ODBC 2.0  
  
 **요약**  
 **ConfigTranslator는** 번역기에 대한 기본 번역 옵션을 반환합니다. 그것은 번역기 DLL 또는 별도의 설정 DLL에있을 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>인수  
 *hwndParent*  
 [입력] 부모 창 핸들입니다. 핸들이 null이면 함수에 대화 상자가 표시되지 않습니다.  
  
 *pvoption*  
 [출력] 32비트 변환 옵션입니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **ConfigTranslator** FALSE를 반환 하는 경우 관련 된 * \*pfErrorCode* 값 **SQLPostInstallerError에** 대 한 호출에 의해 설치 관리자 오류 버퍼에 게시 되 고 **SQLInstallerError**를 호출 하 여 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못되었습니다.|*hwndParent* 인수가 유효하지 않거나 NULL입니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 번역기 관련 오류|정의된 ODBC 설치 관리자 오류가 없는 드라이버별 오류입니다. **SQLPostInstallerError** 함수에 대 한 호출에서 *SzError* 인수 드라이버 관련 오류 메시지를 포함 해야 합니다.|  
|ODBC_ERROR_INVALID_OPTION|잘못된 변환 옵션|*pvOption* 인수에 잘못된 값이 포함되어 있습니다.|  
  
## <a name="comments"></a>주석  
 번역기가 단일 번역 옵션만 지원하는 경우 **ConfigTranslator는** TRUE를 반환하고 *pvOption을* 32비트 옵션으로 설정합니다. 그렇지 않으면 사용할 기본 변환 옵션이 결정됩니다. **ConfigTranslator는** 사용자가 기본 번역 옵션을 선택하는 대화 상자를 표시할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|번역 옵션 얻기|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|번역기 선택|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|변환 옵션 설정|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
