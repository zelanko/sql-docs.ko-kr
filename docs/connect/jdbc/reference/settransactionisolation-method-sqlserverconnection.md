---
title: setTransactionIsolation 메서드 (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.setTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6a8fa4d3-5237-40f8-8a02-b40a3d7a1131
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd1a4fb0ef1c55c54a17dfe1825fd208ebd6035f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32846168"
---
# <a name="settransactionisolation-method-sqlserverconnection"></a>setTransactionIsolation 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 대 한 트랜잭션 격리 수준을 변경 하려고 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 지정한 개체입니다.  
  
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
  
## <a name="remarks"></a>주의  
 이 setTransactionIsolation 메서드는 java.sql.Connection 인터페이스의 setTransactionIsolation 메서드에 의해 지정 됩니다.  
  
 트랜잭션 중간에 이 메서드를 호출하면 트랜잭션이 커밋되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
