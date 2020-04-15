---
title: SQLSetConfigMode 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c36da48fa1493f61131d23a07f7a820b67ebac82
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293283"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 함수
**규칙**  
 버전 출시: ODBC 3.0  
  
 **요약**  
 **SQLSetConfigMode는** 시스템 정보에 DSN 값을 나열하는 Odbc.ini 항목의 위치를 나타내는 구성 모드를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>인수  
 *wConfigMode*  
 [입력] 설치 프로그램 구성 모드("댓글" 참조). *wConfigMode의* 값은 다음과 같은 값일 수 있습니다.  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetConfigModeFALSE를** 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못된 매개 변수 시퀀스|*wConfigMode* 인수에는 ODBC_USER_DSN, ODBC_SYSTEM_DSN 또는 ODBC_BOTH_DSN 포함되지 않았습니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 DSN 값을 나열하는 Odbc.ini 항목이 시스템 정보에 있는 위치를 설정하는 데 사용됩니다. *wConfigMode가* ODBC_USER_DSN 경우 DSN은 사용자 DSN이며 함수는 HKEY_CURRENT_USER Odbc.ini 항목에서 읽습니다. ODBC_SYSTEM_DSN 경우 DSN은 시스템 DSN이며 함수는 HKEY_LOCAL_MACHINE Odbc.ini 항목에서 읽습니다. ODBC_BOTH_DSN 경우 HKEY_CURRENT_USER 시도되고 실패하면 HKEY_LOCAL_MACHINE 사용됩니다.  
  
 이 함수는 **SQLCreateDataSource** 및 **SQLDriverConnect**에 영향을 주지 않습니다. 구성 모드는 드라이버가 **SQLGetPrivateProfileString을** 호출하여 레지스트리에서 읽거나 **SQLWritePrivateProfileString**을 호출하여 레지스트리에 기록할 때 설정되어야 합니다. **SQLGetPrivateProfileString** 및 **SQLWritePrivateProfileString에** 대한 호출은 구성 모드를 사용하여 레지스트리의 어느 부분에서 작동할지 알 수 있습니다.  
  
> [!CAUTION]  
>  **SQLSetConfigMode는** 필요한 경우에만 호출해야 합니다. 모드가 잘못 설정된 경우 ODBC 설치 프로그램이 제대로 작동하지 않을 수 있습니다.  
  
 **SQLSetConfigMode는** 구성 모드를 직접 레지스트리수정합니다. 이는 **SQLConfigDataSource**를 호출하여 구성 모드를 수정하는 프로세스와는 별개입니다. **SQLConfigDataSource에** 대한 호출은 DSN을 수정할 때 사용자와 시스템 DSN을 구분하기 위해 구성 모드를 설정합니다. 반환하기 전에 **SQLConfigDataSource는** 구성 모드를 BOTHDSN으로 재설정합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본 만들기|[SQLCreate데이터 소스](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|연결 문자열 또는 대화 상자를 사용하여 데이터 원본에 연결|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|구성 모드 검색|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
