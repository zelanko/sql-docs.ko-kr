---
title: "addConnectionEventListener 메서드 (SQLServerPooledConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerPooledConnection.addConnectionEventListener
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 142830a8-8d4e-48ca-911d-85bf195ca4fe
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0054071b9fe6ddc814d0973de3af3adbaaa228e0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="addconnectioneventlistener-method-sqlserverpooledconnection"></a>addConnectionEventListener 메서드(SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 이벤트 수신기를 등록 하 여이 이벤트가 발생할 때 알림을 받이 됩니다 있도록 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void addConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *수신기*  
  
 ConnectionEventListener 개체입니다.  
  
## <a name="remarks"></a>주의  
 이 addConnectionEventListener 메서드는 javax.sql.PooledConnection 인터페이스의 addConnectionEventListener 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerPooledConnection 메서드](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection 멤버](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection 클래스](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
