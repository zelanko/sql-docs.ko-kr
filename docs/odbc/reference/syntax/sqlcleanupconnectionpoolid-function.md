---
title: SQLCleanup커넥션풀ID 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a74a92cc05ecd41e99ff87642c7fe3ee527e0c98
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301323"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 함수
**규칙**  
 버전 출시: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLCleanupConnectionPoolID는** 드라이버에 풀 ID가 시간 만료되었다고 알립니다. 풀 ID는 해당 풀 ID와 연결된 풀의 모든 연결이 시간 만일 때마다 시간 아웃할 수 있습니다. 연결 시간 시간에 대한 자세한 내용은 [Microsoft 데이터 액세스 구성 요소의 풀링을](https://msdn.microsoft.com/library/ms810829.aspx) 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>인수  
 *환경 핸들*  
 [입력] 풀의 환경 핸들입니다.  
  
 *풀 ID*  
 [입력] 시간 만료된 풀 ID에 연결된 풀입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자는 **SQLCleanupConnectionPoolID**에서 반환 된 진단 정보를 처리 하지 않습니다.  
  
 응용 프로그램에서 드라이버에서 반환한 오류 메시지를 받을 수 없습니다.  
  
## <a name="remarks"></a>설명  
 **SQLCleanupConnectionPoolID는** 언제든지 호출할 수 있지만 드라이버 관리자는 다른 스레드가 **동시에 SQLGetPoolID를** 호출하지 않으며 다른 스레드가 해당 풀 ID로 할당된 연결 정보 토큰을 사용하던 **SQLRateConnection** 및 **SQLPoolConnect를** 동시에 호출하지 않음을 보장합니다. 따라서 드라이버는 이 함수가 스레드에서 안전한지 확인해야 합니다.  
  
 드라이버는 풀 ID와 연결된 리소스를 정리할 수 있습니다.  
  
 응용 프로그램은 이 함수를 직접 호출해서는 안 됩니다. 드라이버 인식 연결 풀링을 지원하는 ODBC 드라이버는 이 기능을 구현해야 합니다.  
  
 ODBC 드라이버 개발을 위해 sqlspi.h를 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
