---
title: "SQLServerXAConnection 멤버 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b61dabd-369b-460c-8450-9fe424f76541
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0303bdf87283f2a7fba87b58991239f5d92a10d7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverxaconnection-members"></a>SQLServerXAConnection 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에서에 의해 노출 되는 멤버가 나와 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 클래스입니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
 없음  
  
## <a name="inherited-fields"></a>상속된 필드  
 없음  
  
## <a name="methods"></a>메서드  
  
|이름|Description|  
|----------|-----------------|  
|[addConnectionEventListener](../../../connect/jdbc/reference/addconnectioneventlistener-method-sqlserverpooledconnection.md)|(에서 상속 되며, [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md))이 연결 개체에서 이벤트가 발생할 때 알림을 받이 됩니다 있도록 지정된 된 이벤트 수신기를 등록 합니다.|  
|[닫기](../../../connect/jdbc/reference/close-method-sqlserverpooledconnection.md)|(에서 상속 되며, [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md))이 연결 개체가 나타내는 실제 연결을 닫습니다.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverpooledconnection.md)|(에서 상속 되며, [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md))이 연결 개체가 나타내는 실제 연결에 대 한 개체 핸들을 만듭니다.|  
|[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)|검색 한 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 이의 참여를 관리 하는 트랜잭션 관리자는 사용 하 여 개체 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 분산 트랜잭션에서 개체입니다.|  
|[removeConnectionEventListener](../../../connect/jdbc/reference/removeconnectioneventlistener-method-sqlserverpooledconnection.md)|(에서 상속 되며, [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 지정된 된 이벤트 수신기를 제거 합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|javax.sql.PooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXAConnection 클래스](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  

