---
title: 환경 전환 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebfb5475d24d5fc70c4cb46a666b2573066565a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283303"
---
# <a name="environment-transitions"></a>환경 전환
ODBC 환경에는 다음과 같은 세 가지 상태가 있습니다.  
  
|시스템 상태|설명|  
|-----------|-----------------|  
|E0|할당되지 않은 환경|  
|E1|할당된 환경, 할당되지 않은 연결|  
|E2|할당된 환경, 할당된 연결|  
  
 다음 표는 각 ODBC 함수가 환경 상태에 미치는 영향을 보여 줍니다.  
  
## <a name="sqlallochandle"></a>SQLAlloc핸들  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|(IH) [2]|E2[5]<br />(HY010) [6]|--[4]|  
|(IH) [3]|(IH)|--[4]|  
  
 [1] 이 행은 *핸들타입이* SQL_HANDLE_ENV 때의 전환을 보여 주었습니다.  
  
 [2] 이 행은 *핸들타입이* SQL_HANDLE_DBC 때의 전환을 보여 주었습니다.  
  
 [3] 이 행은 *HandleType이* SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC 때의 전환을 보여.  
  
 [4] *OutputHandlePtr을* 사용하여 **SQLAllocHandle을** 호출하면 해당 핸들을 덮어쓰는 올바른 핸들을 가리킵니다. 응용 프로그램 프로그래밍 오류일 수 있습니다.  
  
 [5] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정되었습니다.  
  
 [6] SQL_ATTR_ODBC_VERSION 환경 특성이 환경에 설정되지 않았습니다.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSource 및 SQL드라이버  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--[1]<br />(HY010) [2]|  
  
 [1] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정되었습니다.  
  
 [2] SQL_ATTR_ODBC_VERSION 환경 특성이 환경에 설정되지 않았습니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--[3]<br />(HY010) [4]|--[3]<br />(HY010) [4]|  
|(IH) [2]|(IH)|--|  
  
 [1] 이 행은 *핸들타입이* SQL_HANDLE_ENV 때의 전환을 보여 주었습니다.  
  
 [2] 이 행은 *핸들타입이* SQL_HANDLE_DBC 때의 전환을 보여 주었습니다.  
  
 [3] SQL_ATTR_ODBC_VERSION 환경 특성이 환경에 설정되었습니다.  
  
 [4] SQL_ATTR_ODBC_VERSION 환경 특성이 환경에 설정되지 않았습니다.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|E0|(HY010)|  
|(IH) [2]|(IH)|--[4]<br />E1[5]|  
|(IH) [3]|(IH)|--|  
  
 [1] 이 행은 *핸들타입이* SQL_HANDLE_ENV 때의 전환을 보여 주었습니다.  
  
 [2] 이 행은 *핸들타입이* SQL_HANDLE_DBC 때의 전환을 보여 주었습니다.  
  
 [3] 이 행은 *HandleType이* SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC 때의 전환을 보여.  
  
 [4] 다른 할당 된 연결 핸들이 있었다.  
  
 [5] *핸들에* 지정된 연결 핸들이 할당된 유일한 연결 핸들입니다.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiag필드 및 SQLGetDiagRec  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--|--|  
|(IH) [2]|(IH)|--|  
  
 [1] 이 행은 *핸들타입이* SQL_HANDLE_ENV 때의 전환을 보여 주었습니다.  
  
 [2] 이 행은 *HandleType이* SQL_HANDLE_DBC, SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC 때의 전환을 보여 주었습니다.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--|  
  
 [1] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정되었습니다.  
  
 [2] SQL_ATTR_ODBC_VERSION 환경 특성이 환경에 설정되지 않았습니다.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|(HY011)|  
  
 [1] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정되었습니다.  
  
 [2] *특성* 인수가 SQL_ATTR_ODBC_VERSION 않았으며 SQL_ATTR_ODBC_VERSION 환경 특성이 환경에 설정되지 않았습니다.  
  
## <a name="all-other-odbc-functions"></a>기타 모든 ODBC 함수  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
