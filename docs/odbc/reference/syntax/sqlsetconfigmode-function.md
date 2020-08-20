---
description: SQLSetConfigMode 함수
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5aab5274403a654362c5732d8ec3f6eccae3be96
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499586"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 함수
**규칙**  
 소개 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLSetConfigMode** 는 DSN 값을 나열 하는 Odbc.ini 항목이 시스템 정보에 있는지를 나타내는 구성 모드를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>인수  
 *wConfigMode*  
 입력 설치 관리자 구성 모드입니다 ("설명" 참조). *Wconfigmode* 의 값은 다음과 같을 수 있습니다.  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetConfigMode** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \* pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \* pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못 된 매개 변수 시퀀스|*Wconfigmode* 인수에 ODBC_USER_DSN, ODBC_SYSTEM_DSN 또는 ODBC_BOTH_DSN 포함 되어 있지 않습니다.|  
  
## <a name="comments"></a>주석  
 이 함수는 DSN 값을 나열 하는 Odbc.ini 항목이 시스템 정보에 있는 위치를 설정 하는 데 사용 됩니다. *Wconfigmode* 가 ODBC_USER_DSN 경우 Dsn은 사용자 dsn 이며 함수는 HKEY_CURRENT_USER의 Odbc.ini 항목에서 읽습니다. ODBC_SYSTEM_DSN 되는 경우 DSN은 시스템 DSN 이며 함수는 HKEY_LOCAL_MACHINE의 Odbc.ini 항목에서 읽습니다. ODBC_BOTH_DSN 되는 경우 HKEY_CURRENT_USER 시도 하 고 실패 하면 HKEY_LOCAL_MACHINE 사용 됩니다.  
  
 이 함수는 **Sqlcreatedatasource** 및 **SQLDriverConnect**에 영향을 주지 않습니다. 드라이버에서 **SQLGetPrivateProfileString** 를 호출 하 여 레지스트리에서 읽을 때 구성 모드를 설정 하거나 **SQLWritePrivateProfileString**를 호출 하 여 레지스트리에 쓰도록 설정 해야 합니다. **SQLGetPrivateProfileString** 및 **SQLWritePrivateProfileString** 에 대 한 호출은 구성 모드를 사용 하 여 작동 하는 레지스트리 부분을 파악 합니다.  
  
> [!CAUTION]  
>  필요한 경우에만 **SQLSetConfigMode** 를 호출 해야 합니다. 모드가 잘못 설정 된 경우 ODBC 설치 관리자가 제대로 작동 하지 않을 수 있습니다.  
  
 **SQLSetConfigMode** 는 구성 모드에 대 한 직접 레지스트리 수정 작업을 수행 합니다. 이는 **SQLConfigDataSource**를 호출 하 여 구성 모드를 수정 하는 프로세스와는 차이가 있습니다. **SQLConfigDataSource** 에 대 한 호출은 DSN을 수정할 때 사용자 및 시스템 dsn을 구분 하도록 구성 모드를 설정 합니다. 을 반환 하기 전에 **SQLConfigDataSource** 는 구성 모드를 BOTHDSN로 다시 설정 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 원본 만들기|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|연결 문자열 또는 대화 상자를 사용 하 여 데이터 원본에 연결|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|구성 모드 검색|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
