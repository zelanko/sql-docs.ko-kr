---
title: ConfigTranslator 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f38a9c6814c65593ab452e646a8b1f184e2095de
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47676581"
---
# <a name="configtranslator-function"></a>ConfigTranslator 함수
**규칙**  
 ODBC 2.0 버전에 도입 되었습니다.  
  
 **요약**  
 **ConfigTranslator** 변환기에 대 한 기본 변환 옵션을 반환 합니다. Translator DLL 또는 별도 설치 프로그램 DLL 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>인수  
 *hwndParent*  
 [입력] 부모 창 핸들입니다. 핸들을 null 이면 함수는 모든 대화 상자 표시 되지 않습니다.  
  
 *pvOption*  
 [출력] 32 비트 변환 옵션입니다.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **ConfigTranslator** 연결 된 FALSE를 반환  *\*pfErrorCode* 값을 호출 하 여 설치 관리자 오류 버퍼에 게시 될 **SQLPostInstallerError**및 호출 하 여 가져올 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|합니다 *hwndParent* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 translator 관련 오류|정의 된 ODBC 설치 관리자 오류가 없는 드라이버 관련 오류가 발생 했습니다. 합니다 *SzError* 호출에서 인수를 **SQLPostInstallerError** 함수 드라이버 관련 오류 메시지를 포함 해야 합니다.|  
|ODBC_ERROR_INVALID_OPTION|잘못 된 변환 옵션|합니다 *pvOption* 인수에 잘못 된 값을 포함 합니다.|  
  
## <a name="comments"></a>주석  
 변환기에만 단일 변환 옵션을 지 원하는 경우 **ConfigTranslator** TRUE를 반환 하 고 설정 *pvOption* 32 비트 옵션입니다. 그렇지 않은 경우 기본 변환 옵션을 사용 하 여 결정 합니다. **ConfigTranslator** 있는 사용자는 기본 변환 옵션을 선택 하는 대화 상자를 표시할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|번역 옵션 가져오기|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|변환기를 선택합니다.|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|변환 옵션 설정|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
