---
title: ConfigTranslator 함수 | Microsoft Docs
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
- ConfigTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigTranslator
helpviewer_keywords:
- ConfigTranslator [ODBC]
ms.assetid: 7c22f07e-36de-425b-aa67-e32a84afae92
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5b38bc6340ec456ce180eb2a9cc266d5b8a19305
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916398"
---
# <a name="configtranslator-function"></a>ConfigTranslator 함수
**규칙**  
 ODBC 2.0 도입 된 버전:  
  
 **요약**  
 **ConfigTranslator** 는 변환기에 대 한 기본 변환 옵션을 반환 합니다. 변환기 DLL 또는 별도 설치 DLL에서 가능 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>인수  
 *hwndParent*  
 [입력] 부모 창 핸들입니다. 핸들 null 이면 함수는 모든 대화 상자 표시 되지 않습니다.  
  
 *pvOption*  
 [출력] 32 비트 번역 옵션입니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **ConfigTranslator** 관련 FALSE를 반환  *\*pfErrorCode* 를 호출 하 여 설치 관리자 오류 버퍼에 값이 게시 **SQLPostInstallerError**를 호출 하 여 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|*창은* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 변환기 관련 오류|정의 된 ODBC 설치 관리자 오류가 없는 드라이버 관련 오류가 발생 했습니다. *SzError* 에 대 한 호출의 인수는 **SQLPostInstallerError** 함수에는 드라이버 특정 오류 메시지가 포함 되어 있어야 합니다.|  
|ODBC_ERROR_INVALID_OPTION|잘못 된 번역 옵션|*pvOption* 인수에 잘못 된 값을 포함 합니다.|  
  
## <a name="comments"></a>설명  
 변환기는 단일 변환 옵션을 지 원하는 경우 **ConfigTranslator** TRUE를 반환 하 고 설정 *pvOption* 를 32 비트 옵션입니다. 그렇지 않은 경우 사용 하는 기본 변환 옵션을 결정 합니다. **ConfigTranslator** 는 사용자가 기본 변환 옵션을 선택 하는 대화 상자를 표시할 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|번역 옵션 가져오기|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|변환기를 선택합니다.|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|변환 옵션 설정|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
