---
title: SQLCleanupConnectionPoolID 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1dc2552c848b691346c57a0191f9c9200bad4523
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666171"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 함수
**규칙**  
 버전에 도입 되었습니다: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLCleanupConnectionPoolID** 풀 ID를 초과 하는 드라이버에 알립니다. 풀 ID는 해당 풀 ID와 연결 된 풀의 모든 연결 된 때마다 제한 시간 수의 제한 시간이 초과 되었습니다. 참조 [Microsoft Data Access Components의 풀링](http://msdn.microsoft.com/library/ms810829.aspx) 연결 제한 시간에 대 한 자세한 내용은 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>인수  
 *EnvironmentHandle*  
 [입력] 환경 핸들의 풀입니다.  
  
 *PoolID*  
 [입력] 시간이 초과 된 된 풀 ID에 연결 된 풀 합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자에서 반환 된 진단 정보를 처리 하지 것입니다 **SQLCleanupConnectionPoolID**합니다.  
  
 응용 프로그램 드라이버에 의해 반환 되는 오류 메시지를 받을 수 없습니다.  
  
## <a name="remarks"></a>Remarks  
 **SQLCleanupConnectionPoolID** 언제 든 지 호출할 수 있지만 드라이버 관리자는 다른 스레드에서 동시에 호출 하는 보장 **SQLGetPoolID** 하며 다른 스레드에서 동시에 호출  **SQLRateConnection** 하 고 **SQLPoolConnect** 풀 ID를 사용 하 여 할당 된 연결 정보 토큰을 사용 하 여 따라서 드라이버는이 함수는 스레드로부터 안전 하 고 있는지 확인 해야 합니다.  
  
 드라이버 풀 ID와 사용 하 여 연결 된 리소스를 정리할 수 있습니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발을 위한 sqlspi.h 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
