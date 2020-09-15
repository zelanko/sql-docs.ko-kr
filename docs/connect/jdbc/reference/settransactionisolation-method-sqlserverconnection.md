---
description: setTransactionIsolation 메서드(SQLServerConnection)
title: setTransactionIsolation 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6a8fa4d3-5237-40f8-8a02-b40a3d7a1131
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 552920c275dee8b1dede1b229b593ce8b7547428
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355006"
---
# <a name="settransactionisolation-method-sqlserverconnection"></a>setTransactionIsolation 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 트랜잭션 격리 수준을 지정된 수준으로 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setTransactionIsolation(int level)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *level*  
  
 다음 격리 수준 중 하나가 포함된 **int** 값입니다.  
  
 TRANSACTION_READ_UNCOMMITTED  
  
 TRANSACTION_READ_COMMITTED  
  
 TRANSACTION_REPEATABLE_READ  
  
 TRANSACTION_SERIALIZABLE  
  
 TRANSACTION_SNAPSHOT = 0x1000  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setTransactionIsolation 메서드는 java.sql.Connection 인터페이스의 setTransactionIsolation 메서드에 의해 지정됩니다.  
  
 트랜잭션 중간에 이 메서드를 호출하면 트랜잭션이 커밋되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
