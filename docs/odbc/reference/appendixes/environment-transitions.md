---
title: 환경 전환 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b1de2f2147357f9e2ed4f71657b9298c4a13684
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910430"
---
# <a name="environment-transitions"></a>환경 전환
ODBC 환경에는 다음 세 가지 상태에 있습니다.  
  
|State|설명|  
|-----------|-----------------|  
|E0|할당 되지 않은 환경|  
|E1|연결 할당 되지 않은 할당 된 환경|  
|E2|환경에 연결 할당 된 할당|  
  
 다음 표에 각 ODBC 함수 환경 상태에 미치는 영향을 보여 줍니다.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|(IH)[2]|E2[5]<br />(HY010) [6]|--[4]|  
|(IH)[3]|(IH)|--[4]|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_DBC 되었습니다.  
  
 [3]이이 행 표시 전환 때 *HandleType* 호출 되었거나 SQL_HANDLE_DESC 합니다.  
  
 [4] 호출 **SQLAllocHandle** 사용 하 여 *OutputHandlePtr* 유효한 핸들을 가리키는 해당 핸들을 덮어씁니다. 이 응용 프로그램 프로그래밍 오류를 수 있습니다.  
  
 [5]를 SQL_ATTR_ODBC_VERSION 환경 특성 환경에 설정 했습니다.  
  
 [6] SQL_ATTR_ODBC_VERSION 환경 특성 환경에 설정 없습니다.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 및 SQLDrivers  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--[1]<br />(HY010)[2]|  
  
 [1] SQL_ATTR_ODBC_VERSION 환경 특성 환경에 설정 된 합니다.  
  
 [2]에서 SQL_ATTR_ODBC_VERSION 환경 특성 환경에 설정 없습니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--[3]<br />(HY010)[4]|--[3]<br />(HY010)[4]|  
|(IH)[2]|(IH)|--|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_DBC 되었습니다.  
  
 [환경에 설정 된 SQL_ATTR_ODBC_VERSION 환경 특성 3.  
  
 [SQL_ATTR_ODBC_VERSION 환경 특성 4]에서 환경에 설정 없습니다.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|E0|(HY010)|  
|(IH)[2]|(IH)|--[4]<br />E1[5]|  
|(IH)[3]|(IH)|--|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_DBC 되었습니다.  
  
 [3]이이 행 표시 전환 때 *HandleType* 호출 되었거나 SQL_HANDLE_DESC 합니다.  
  
 [4] 다른 할당 된 연결 핸들 했습니다.  
  
 [5]에 지정 된 연결 핸들 *처리* 만 할당 된 연결 처리 되었습니다.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagRec 및 SQLGetDiagField  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--|--|  
|(IH)[2]|(IH)|--|  
  
 [1]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_ENV 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_DBC, 호출 하 여, 또는 SQL_HANDLE_DESC 합니다.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--|  
  
 [1] SQL_ATTR_ODBC_VERSION 환경 특성 환경에 설정 된 합니다.  
  
 [2]에서 SQL_ATTR_ODBC_VERSION 환경 특성 환경에 설정 없습니다.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|(HY011)|  
  
 [1] SQL_ATTR_ODBC_VERSION 환경 특성 환경에 설정 된 합니다.  
  
 [2]은 *특성* 인수를 SQL_ATTR_ODBC_VERSION 없었으며 SQL_ATTR_ODBC_VERSION 환경 특성 환경에 설정 없습니다.  
  
## <a name="all-other-odbc-functions"></a>다른 모든 ODBC 함수  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
