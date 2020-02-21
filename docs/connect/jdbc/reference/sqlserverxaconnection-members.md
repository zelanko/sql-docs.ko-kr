---
title: SQLServerXAConnection 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b61dabd-369b-460c-8450-9fe424f76541
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85d106ad25c1823f873ade24800e44987d78a2f7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67970258"
---
# <a name="sqlserverxaconnection-members"></a>SQLServerXAConnection 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에는 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 클래스에 의해 노출되는 멤버가 나와 있습니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
 없음  
  
## <a name="inherited-fields"></a>상속된 필드  
 없음  
  
## <a name="methods"></a>메서드  
  
|속성|Description|  
|----------|-----------------|  
|[addConnectionEventListener](../../../connect/jdbc/reference/addconnectioneventlistener-method-sqlserverpooledconnection.md)|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)에서 상속되며, 지정된 이벤트 수신기를 등록하여 이 Connection 개체에서 이벤트가 발생할 때 해당 수신기가 알림을 받도록 합니다.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpooledconnection.md)|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)에서 상속되며, 이 Connection 개체가 나타내는 실제 연결을 닫습니다.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverpooledconnection.md)|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)에서 상속되며, 이 Connection 개체가 나타내는 실제 연결에 대한 개체 핸들을 만듭니다.|  
|[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)|트랜잭션 관리자가 분산 트랜잭션에서 이 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 개체의 참여를 관리하는 데 사용할 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체를 검색합니다.|  
|[removeConnectionEventListener](../../../connect/jdbc/reference/removeconnectioneventlistener-method-sqlserverpooledconnection.md)|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)에서 상속되며, 지정된 이벤트 수신기를 제거합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|javax.sql.PooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAConnection 클래스](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
