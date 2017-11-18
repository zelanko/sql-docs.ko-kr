---
title: "setTransactionIsolation 메서드 (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.setTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6a8fa4d3-5237-40f8-8a02-b40a3d7a1131
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b91e33388706cabe7436259193f9b2c0bb446b25
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="settransactionisolation-method-sqlserverconnection"></a>setTransactionIsolation 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 대 한 트랜잭션 격리 수준을 변경 하려고 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 지정한 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setTransactionIsolation(int level)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *수준*  
  
 **int** 다음 격리 수준 중 하나를 포함 하는 값:  
  
 TRANSACTION_READ_UNCOMMITTED  
  
 TRANSACTION_READ_COMMITTED  
  
 TRANSACTION_REPEATABLE_READ  
  
 TRANSACTION_SERIALIZABLE  
  
 TRANSACTION_SNAPSHOT = 0x1000  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setTransactionIsolation 메서드는 java.sql.Connection 인터페이스의 setTransactionIsolation 메서드에 의해 지정 됩니다.  
  
 트랜잭션 중간에 이 메서드를 호출하면 트랜잭션이 커밋되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

