---
title: SQLGetConfigMode 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConfigMode
helpviewer_keywords:
- SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc11bec24ede3352dd43f3645fb8c720b77fdabe
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285693"
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 함수
**규칙**  
 버전 출시: ODBC 3.0  
  
 **요약**  
 **SQLGetConfigMode는** 시스템 정보에 DSN 값을 나열하는 Odbc.ini 항목의 위치를 나타내는 구성 모드를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>인수  
 *pwConfigMode*  
 [출력] 구성 모드를 포함하는 버퍼에 대한 포인터입니다. ("댓글"참조)) * \*pwConfigMode의* 값은 다음과 같은 값일 수 있습니다.  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetConfigModeFALSE를** 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 DSN 값을 나열하는 Odbc.ini 항목이 시스템 정보의 위치를 결정하는 데 사용됩니다. * \*pwConfigMode가* ODBC_USER_DSN 경우 DSN은 사용자 DSN이며 함수는 HKEY_CURRENT_USER Odbc.ini 항목에서 읽습니다. ODBC_SYSTEM_DSN 경우 DSN은 시스템 DSN이며 함수는 HKEY_LOCAL_MACHINE Odbc.ini 항목에서 읽습니다. ODBC_BOTH_DSN 경우 HKEY_CURRENT_USER 시도되고 실패하면 HKEY_LOCAL_MACHINE 사용됩니다.  
  
 기본적으로 **SQLGetConfigMode는 ODBC_BOTH_DSN 반환합니다.** **SQLConfigDataSource를**호출하여 사용자 DSN 또는 시스템 DSN을 만들면 이 함수는 구성 모드를 ODBC_USER_DSN 또는 ODBC_SYSTEM_DSN 설정하여 DSN을 수정하는 동안 사용자와 시스템 DSN을 구분합니다. 반환하기 전에 **SQLConfigDataSource는** 구성 모드를 ODBC_BOTH_DSN 다시 설정합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|구성 모드 설정|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
