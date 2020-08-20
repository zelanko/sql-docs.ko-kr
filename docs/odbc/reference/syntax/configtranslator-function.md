---
description: ConfigTranslator 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b99628b801199c7e2d7fd033e1b0728f1538932
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461275"
---
# <a name="configtranslator-function"></a>ConfigTranslator 함수
**규칙**  
 소개 된 버전: ODBC 2.0  
  
 **요약**  
 **Configtranslator** 는 번역기에 대 한 기본 번역 옵션을 반환 합니다. 이 파일은 번역기 DLL 또는 별도의 설치 DLL에 있을 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>인수  
 *hwndParent*  
 입력 부모 창 핸들입니다. 핸들이 null 이면 함수는 대화 상자를 표시 하지 않습니다.  
  
 *pvOption*  
 출력 32 비트 번역 옵션입니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **Configtranslator** FALSE를 반환 하면 연결 된 * \* pfErrorCode* 값이 **SQLPostInstallerError** 에 대 한 호출에 의해 설치 관리자 오류 버퍼에 게시 되 고 **SQLInstallerError**를 호출 하 여 가져올 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \* pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못 되었습니다.|*HwndParent* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 번역기 관련 오류|ODBC 설치 관리자 오류가 정의 되지 않은 드라이버 관련 오류입니다. **SQLPostInstallerError** 함수 호출의 *szerror* 인수는 드라이버별 오류 메시지를 포함 해야 합니다.|  
|ODBC_ERROR_INVALID_OPTION|잘못 된 변환 옵션|*PvOption* 인수에 잘못 된 값이 있습니다.|  
  
## <a name="comments"></a>주석  
 변환기에서 단일 번역 옵션만 지 원하는 경우 **Configtranslator** 는 TRUE를 반환 하 고 *pvOption* 를 32 비트 옵션으로 설정 합니다. 그렇지 않으면 사용할 기본 변환 옵션을 결정 합니다. **Configtranslator** 는 사용자가 기본 번역 옵션을 선택할 수 있는 대화 상자를 표시할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|번역 옵션 가져오기|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|번역기 선택|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|변환 옵션 설정|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
