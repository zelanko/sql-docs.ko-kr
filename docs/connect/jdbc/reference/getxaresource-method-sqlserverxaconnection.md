---
title: getXAResource 메서드(SQLServerXAConnection) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: beee81cbc62a1257c9f9f0fbe8c93720fa54a523
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910141"
---
# <a name="getxaresource-method-sqlserverxaconnection"></a>getXAResource 메서드(SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  트랜잭션 관리자가 분산 트랜잭션에서 이 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체의 참여를 관리하는 데 사용할 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 개체를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>Return Value  
 XAResource 개체입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>설명  
 이 getXAResource 메서드는 javax.sql.XAConnection 인터페이스의 getXAResource 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAConnection 메서드](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [SQLServerXAConnection 메서드](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [SQLServerXAConnection 클래스](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
