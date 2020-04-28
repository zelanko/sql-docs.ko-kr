---
title: SQLGetConfigMode 함수 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285693"
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 함수
**규칙**  
 소개 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLGetConfigMode** 는 DSN 값을 나열 하는 Odbc .ini 항목이 시스템 정보에 있는지를 나타내는 구성 모드를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>인수  
 *pwConfigMode*  
 출력 구성 모드를 포함 하는 버퍼에 대 한 포인터입니다. "설명"을 참조 하십시오. * \*PwConfigMode* 의 값은 다음과 같을 수 있습니다.  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetConfigMode** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 DSN 값을 나열 하는 Odbc .ini 항목이 시스템 정보에 있는지 여부를 확인 하는 데 사용 됩니다. * \*PwConfigMode* 가 ODBC_USER_DSN 경우 dsn은 사용자 dsn이 고 함수는 HKEY_CURRENT_USER의 ODBC .ini 항목에서 읽습니다. ODBC_SYSTEM_DSN 되는 경우 DSN은 시스템 DSN 이며 함수는 HKEY_LOCAL_MACHINE의 Odbc .ini 항목에서 읽습니다. ODBC_BOTH_DSN 되는 경우 HKEY_CURRENT_USER 시도 하 고 실패 하면 HKEY_LOCAL_MACHINE 사용 됩니다.  
  
 기본적으로 **SQLGetConfigMode** 는 ODBC_BOTH_DSN를 반환 합니다. **SQLConfigDataSource**호출을 통해 사용자 Dsn 또는 시스템 dsn을 만든 경우이 함수는 DSN을 수정 하는 동안 사용자 및 시스템 dsn을 구분 하기 위해 구성 모드를 ODBC_USER_DSN 또는 ODBC_SYSTEM_DSN로 설정 합니다. 을 반환 하기 전에 **SQLConfigDataSource** 는 구성 모드를 ODBC_BOTH_DSN으로 다시 설정 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|구성 모드 설정|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
