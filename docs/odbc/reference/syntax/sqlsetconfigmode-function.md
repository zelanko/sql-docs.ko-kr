---
title: "SQLSetConfigMode 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLSetConfigMode
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetConfigMode
helpviewer_keywords: SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b9305a4b9cbbf8ce7316d1c3eccf71115e5f0fe
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 함수
**규칙**  
 ODBC 3.0 도입 된 버전:  
  
 **요약**  
 **SQLSetConfigMode** 시스템 정보에 DSN 값을 나열 하는 Odbc.ini 항목 인지를 나타내는 구성 모드를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>인수  
 *wConfigMode*  
 [입력] 설치 관리자 구성 모드 ("주석" 참조). 값 *wConfigMode* 될 수 있습니다.  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetConfigMode** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못 된 매개 변수 순서|*wConfigMode* ODBC_USER_DSN, ODBC_SYSTEM_DSN, 또는 ODBC_BOTH_DSN 인수를 포함 하지 않았습니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 DSN 값을 나열 하는 Odbc.ini 항목 시스템 정보에 있는 설정에 사용 됩니다. 경우 *wConfigMode* ODBC_USER_DSN, DSN은 DSN이 사용자 이며 HKEY_CURRENT_USER에 Odbc.ini 항목에서 함수를 읽습니다. ODBC_SYSTEM_DSN 이면 DSN은 시스템 DSN 고 함수 Odbc.ini 항목 HKEY_LOCAL_MACHINE에서 읽습니다. ODBC_BOTH_DSN 이면 HKEY_CURRENT_USER 시도 되 면 하 고 실패 한 경우 HKEY_LOCAL_MACHINE 사용 됩니다.  
  
 이 함수에 영향을 주지 않는 **SQLCreateDataSource** 및 **SQLDriverConnect**합니다. 구성 모드에는 드라이버를 호출 하 여 레지스트리에서 읽을 때 서비스에서 설정할 **SQLGetPrivateProfileString** 호출 하 여 레지스트리에 씁니다 또는 **SQLWritePrivateProfileString**합니다. 에 대 한 호출이 **SQLGetPrivateProfileString** 및 **SQLWritePrivateProfileString** 구성 모드를 사용 하 여에서 작동 하도록 레지스트리의 어느 부분에 알아야 합니다.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** ODBC 설치 제대로 작동 하지 않을 수 있습니다는 모드가 설정 잘못 되어 있으면 필요한 경우에 호출 해야 합니다.  
  
 **SQLSetConfigMode** 을 선택 하면 구성 모드의 레지스트리를 직접 수정 합니다. 이 구성 모드를 호출 하 여 수정 프로세스와는 별도로 **SQLConfigDataSource**합니다. 에 대 한 호출 **SQLConfigDataSource** DSN을 수정할 때 사용자 및 시스템 Dsn을 구별 하는 구성 모드를 설정 합니다. 를 반환 하기 전에 **SQLConfigDataSource** 구성 모드 BOTHDSN을 기본값으로 다시 설정 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|데이터 원본 만들기|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|구성 모드를 검색합니다.|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
