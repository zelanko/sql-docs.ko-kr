---
title: "getPooledConnection 메서드 () | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerConnectionPoolDataSource.getPooledConnection ()
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: aad6c325-3398-462c-aa6e-201dc89fa5ef
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4a35e2b75f0de79a010483b1a7240c2721eb5f5a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getpooledconnection-method-"></a>getPooledConnection 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  풀링된 연결로 사용할 수 있는 실제 데이터베이스 연결을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public javax.sql.PooledConnection getPooledConnection()  
```  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>주의  
 이 getPooledConnection 메서드는 javax.sql.ConnectionPoolDataSource 인터페이스의 getPooledConnection 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)   
 [SQLServerConnectionPoolDataSource 메서드](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource 멤버](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource 클래스](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
