---
title: "getXAResource 메서드 (SQLServerXAConnection) | Microsoft Docs"
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
- SQLServerXAConnection.getXAResource
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d2828f-fd20-44b0-b796-dc70f77c5b03
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 78999ece74ad80f7d4ce107484d225cc1ab6f4f6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getxaresource-method-sqlserverxaconnection"></a>getXAResource 메서드(SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  검색 한 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 관리 하기 위해 트랜잭션 관리자는 사용 하 여 개체 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 개체의 분산된 트랜잭션에 참여 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>반환 값  
 XAResource 개체입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>주의  
 이 getXAResource 메서드는 javax.sql.XAConnection 인터페이스의 getXAResource 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXAConnection 메서드](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [SQLServerXAConnection 멤버](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [SQLServerXAConnection 클래스](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  

