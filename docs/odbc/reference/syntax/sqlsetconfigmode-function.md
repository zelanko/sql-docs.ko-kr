---
title: SQLSetConfigMode 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a10ec8f8fa6ef2b0e310680f58252f98628ff045
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62656061"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 함수
**규칙**  
 도입 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLSetConfigMode** DSN 값을 나열 하는 Odbc.ini 항목은 시스템 정보에서 위치를 지정 하는 구성 모드를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>인수  
 *wConfigMode*  
 [입력] 설치 관리자 구성 모드 ("주석" 참조). 값 *wConfigMode* 될 수 있습니다.  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetConfigMode** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못 된 매개 변수 순서|합니다 *wConfigMode* ODBC_USER_DSN, ODBC_SYSTEM_DSN, 또는 ODBC_BOTH_DSN 인수 포함 되지 않았습니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 시스템 정보에 DSN 값을 나열 하는 Odbc.ini 항목 인 설정에 사용 됩니다. 하는 경우 *wConfigMode* ODBC_USER_DSN, DSN 사용자 DSN 이며 함수는 Odbc.ini 항목 HKEY_CURRENT_USER에서 읽습니다. ODBC_SYSTEM_DSN 인 경우 DSN은 시스템 DSN 및 함수는 Odbc.ini 항목 HKEY_LOCAL_MACHINE에서 읽습니다. HKEY_CURRENT_USER 시도할 ODBC_BOTH_DSN 이면 하 고 실패 한 경우 HKEY_LOCAL_MACHINE 사용 됩니다.  
  
 이 함수에 영향을 주지 않습니다 **SQLCreateDataSource** 하 고 **SQLDriverConnect**합니다. 구성 모드에 드라이버를 호출 하 여 레지스트리에서 읽을 때 설정할 **SQLGetPrivateProfileString** 하거나 호출 하 여 레지스트리에 씁니다 **SQLWritePrivateProfileString**합니다. 에 대 한 호출 **SQLGetPrivateProfileString** 하 고 **SQLWritePrivateProfileString** 구성 모드를 사용 하 여 어느 부분에서 작동 하도록 레지스트리를 알아야 합니다.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** ODBC 설치 관리자를 제대로 작동 하지 못할 수 있습니다 때 필요한; 모드를 설정한 부적절 하 게 하는 경우에 호출 해야 합니다.  
  
 **SQLSetConfigMode** 구성 모드의 직접 레지스트리를 수정 하면 됩니다. 호출 하 여 구성 모드를 수정 하는 프로세스와는 별도로 이것이 **SQLConfigDataSource**합니다. 에 대 한 호출 **SQLConfigDataSource** DSN을 수정 하는 경우 사용자 및 시스템 Dsn을 구분 하기 위해 구성 모드를 설정 합니다. 를 반환 하기 전에 **SQLConfigDataSource** BOTHDSN 구성 모드를 다시 설정 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|데이터 원본 만들기|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|구성 모드를 검색합니다.|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
