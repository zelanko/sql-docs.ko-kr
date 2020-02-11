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
ms.openlocfilehash: ee8f9b9879a3533e8196bbc89f8ae0b0a132293a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036092"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 함수
**규칙**  
 소개 된 버전: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLCleanupConnectionPoolID** 는 풀 ID의 시간이 초과 되었음을 드라이버에 알립니다. 풀 id와 연결 된 풀의 모든 연결이 시간 초과 될 때마다 풀 ID가 시간 초과 될 수 있습니다. 연결 제한 시간에 대 한 자세한 내용은 [Microsoft 데이터 액세스 구성 요소의 풀링](https://msdn.microsoft.com/library/ms810829.aspx) 을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>인수  
 *EnvironmentHandle*  
 입력 풀의 환경 핸들입니다.  
  
 *PoolID*  
 입력 시간 초과 된 풀 ID에 연결 된 풀입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자는 **SQLCleanupConnectionPoolID**에서 반환 된 진단 정보를 처리 하지 않습니다.  
  
 응용 프로그램이 드라이버에서 반환 된 오류 메시지를 수신할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 **SQLCleanupConnectionPoolID** 는 언제 든 지 호출할 수 있지만, 드라이버 관리자는 다른 스레드가 동시에 **SQLGetPoolID** 를 호출 하지 않고 다른 스레드가 동시에 **SQLRateConnection** 및 **sqlpoolconnect** 를 호출 하는 것을 보장 합니다 .이는 해당 풀 ID로 할당 된 연결 정보 토큰을 사용 합니다. 따라서 드라이버는이 함수가 스레드로부터 안전 하 게 보호 되는지 확인 해야 합니다.  
  
 드라이버는 풀 ID와 연결 된 리소스를 정리할 수 있습니다.  
  
 응용 프로그램은이 함수를 직접 호출 하면 안 됩니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발용으로 sqlspi .h를 포함 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
