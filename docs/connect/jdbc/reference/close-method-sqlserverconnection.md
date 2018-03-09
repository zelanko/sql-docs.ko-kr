---
title: "close 메서드 (SQLServerConnection) | Microsoft Docs"
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
apiname: SQLServerConnection.close
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f0f26585-bdf7-4737-b434-8c7e115c8e94
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c8a83569b36191cb38fe70641650066ba3750780
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="close-method-sqlserverconnection"></a>close 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 해제 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체의 데이터베이스와 JDBC 리소스를 자동으로 해제 되기를 기다리지 않고 즉시 해제 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 Close이 메서드는 java.sql.Connection 인터페이스에 close 메서드에 의해 지정 됩니다.  
  
 트랜잭션 중간에 close 메서드를 호출 하면 트랜잭션이 롤백됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
