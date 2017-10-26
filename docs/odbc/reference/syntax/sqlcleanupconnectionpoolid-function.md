---
title: "SQLCleanupConnectionPoolID 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 49d204d7d77ae39c6a7eb3c9d408f6d72bafcc91
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 함수
**규칙**  
 도입 된 버전: ODBC 3.81 표준 준수: ODBC  
  
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
 [입력] 풀의 환경 핸들을 지정 합니다.  
  
 *PoolID*  
 [입력] 제한 시간이 초과 하는 풀 ID에 연결 된 풀입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자에서 반환 된 진단 정보를 처리 하지 것입니다 **SQLCleanupConnectionPoolID**합니다.  
  
 응용 프로그램이 드라이버에서 반환 된 오류 메시지를 받을 수 없습니다.  
  
## <a name="remarks"></a>주의  
 **SQLCleanupConnectionPoolID** 언제 든 지 호출 될 수 있지만 드라이버 관리자는 다른 스레드에서 호출 동시에 있다는 보장 **SQLGetPoolID** 하며 동시에 다른 스레드에서 호출 ** SQLRateConnection** 및 **SQLPoolConnect** 풀 ID를 가진 지정 된 연결 정보 토큰으로 따라서 드라이버는이 함수는 스레드로부터 안전 하 고 있는지 확인 해야 합니다.  
  
 드라이버 풀 ID와 연결 된 리소스를 정리할 수 있습니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지원 되는 ODBC 드라이버가이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발에 대 한 sqlspi.h를 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버를 개발합니다.](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

