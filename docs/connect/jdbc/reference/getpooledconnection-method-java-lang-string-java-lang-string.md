---
title: getPooledConnection 메서드 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnectionPoolDataSource.getPooledConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f2e6391d-9aaf-4b09-ae1c-a27c1ada6301
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 424ac4951ce4fd6f63644a154d7fd572dd5657be
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32839018"
---
# <a name="getpooledconnection-method-javalangstring-javalangstring"></a>getPooledConnection 메서드(java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 사용자 이름 및 암호에 따라 풀링된 연결로 사용할 수 있는 실제 데이터베이스 연결을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public javax.sql.PooledConnection getPooledConnection(java.lang.String user,  
                                                      java.lang.String password)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *user*  
  
 A **문자열** 사용자 이름이 들어 있는입니다.  
  
 *passwword*  
  
 A **문자열** 암호가 포함 된 합니다.  
  
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
  
  
