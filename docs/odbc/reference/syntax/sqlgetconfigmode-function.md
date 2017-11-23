---
title: "SQLGetConfigMode 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetConfigMode
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetConfigMode
helpviewer_keywords: SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82f01e7b93cc5114193dcc550476dafc63cd09a3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 함수
**규칙**  
 ODBC 3.0 도입 된 버전:  
  
 **요약**  
 **SQLGetConfigMode** 시스템 정보에 DSN 값을 나열 하는 Odbc.ini 항목 인지를 나타내는 구성 모드를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>인수  
 *pwConfigMode*  
 [출력] 구성 모드를 포함 하는 버퍼에 대 한 포인터입니다. ("주석" 참조) 값 * \*pwConfigMode* 될 수 있습니다.  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetConfigMode** 관련 FALSE를 반환 * \*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에 * \*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>설명  
 이 함수는 위치를 확인 DSN 값을 나열 하는 Odbc.ini 항목 시스템 정보에 사용 됩니다. 경우 * \*pwConfigMode* ODBC_USER_DSN, DSN은 DSN이 사용자 이며 HKEY_CURRENT_USER에 Odbc.ini 항목에서 함수를 읽습니다. ODBC_SYSTEM_DSN 이면 DSN은 시스템 DSN 고 함수 Odbc.ini 항목 HKEY_LOCAL_MACHINE에서 읽습니다. ODBC_BOTH_DSN 이면 HKEY_CURRENT_USER 시도 되 면 하 고 실패 한 경우 HKEY_LOCAL_MACHINE 사용 됩니다.  
  
 기본적으로 **SQLGetConfigMode** ODBC_BOTH_DSN를 반환 합니다. 사용자 DSN 또는 시스템 DSN 만들어질 때 호출 하 여 **SQLConfigDataSource**, ODBC_USER_DSN 또는 ODBC_SYSTEM_DSN DSN을 수정 하는 동안 사용자 및 시스템 Dsn을 구분 하기 위해 구성 모드를 설정 하는 함수입니다. 를 반환 하기 전에 **SQLConfigDataSource** 구성 모드 ODBC_BOTH_DSN을 기본값으로 다시 설정 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|구성 모드를 설정합니다.|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
