---
title: getPooledConnection 메서드(java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnectionPoolDataSource.getPooledConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f2e6391d-9aaf-4b09-ae1c-a27c1ada6301
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d6c21fa5df3545b641ccb935c53f6d7a689f580
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702951"
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
  
 사용자 이름을 포함하는 **문자열**입니다.  
  
 *passwword*  
  
 암호가 포함된 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 이 getPooledConnection 메서드는 javax.sql.ConnectionPoolDataSource 인터페이스의 getPooledConnection 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)   
 [SQLServerConnectionPoolDataSource 메서드](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource 멤버](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource 클래스](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
