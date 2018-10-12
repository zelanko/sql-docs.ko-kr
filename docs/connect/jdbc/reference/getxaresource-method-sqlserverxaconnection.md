---
title: getXAResource 메서드 (SQLServerXAConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAConnection.getXAResource
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d2828f-fd20-44b0-b796-dc70f77c5b03
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d48ba821cee687eca112c405e5f0363244bc7842
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47700141"
---
# <a name="getxaresource-method-sqlserverxaconnection"></a>getXAResource 메서드(SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  트랜잭션 관리자가 분산 트랜잭션에서 이 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 개체의 참여를 관리하는 데 사용할 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>반환 값  
 XAResource 개체입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 이 getXAResource 메서드는 javax.sql.XAConnection 인터페이스의 getXAResource 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAConnection 메서드](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [SQLServerXAConnection 메서드](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [SQLServerXAConnection 클래스](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
