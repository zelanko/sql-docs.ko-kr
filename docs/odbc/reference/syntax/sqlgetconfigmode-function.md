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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d9065d48e8b4af686e1ff64272fbe902e066cb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537281"
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 함수
**규칙**  
 도입 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLGetConfigMode** DSN 값을 나열 하는 Odbc.ini 항목은 시스템 정보에서 위치를 지정 하는 구성 모드를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>인수  
 *pwConfigMode*  
 [출력] 구성 모드를 포함 하는 버퍼에 대 한 포인터입니다. ("주석입니다." 참조) 값  *\*pwConfigMode* 될 수 있습니다.  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetConfigMode** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 시스템 정보에 DSN 값을 나열 하는 Odbc.ini 항목 위치를 확인에 사용 됩니다. 하는 경우  *\*pwConfigMode* ODBC_USER_DSN, DSN 사용자 DSN 이며 함수는 Odbc.ini 항목 HKEY_CURRENT_USER에서 읽습니다. ODBC_SYSTEM_DSN 인 경우 DSN은 시스템 DSN 및 함수는 Odbc.ini 항목 HKEY_LOCAL_MACHINE에서 읽습니다. HKEY_CURRENT_USER 시도할 ODBC_BOTH_DSN 인 경우 및 HKEY_LOCAL_MACHINE 실패 하는 경우 사용 됩니다.  
  
 기본적으로 **SQLGetConfigMode** ODBC_BOTH_DSN를 반환 합니다. 사용자 DSN 또는 시스템 DSN을 만들면를 호출한 **SQLConfigDataSource**, ODBC_USER_DSN 또는 ODBC_SYSTEM_DSN DSN을 수정 하는 동안 사용자 및 시스템 Dsn을 구분 하기 위해 구성 모드를 설정 하는 함수입니다. 를 반환 하기 전에 **SQLConfigDataSource** ODBC_BOTH_DSN 구성 모드를 다시 설정 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|구성 모드 설정|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
