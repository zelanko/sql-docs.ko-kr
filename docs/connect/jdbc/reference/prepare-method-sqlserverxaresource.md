---
title: "prepare 메서드 (SQLServerXAResource) | Microsoft Docs"
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
apiname: SQLServerXAResource.prepare
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f800c966-3fae-41b3-963a-464988f80da3
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3abe6f5f7b415e0fbae0950929acd7ff3318bdbb
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="prepare-method-sqlserverxaresource"></a>prepare 메서드(SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 Xid 개체에서 지정 된 트랜잭션의 트랜잭션 커밋을 준비 하도록 리소스 관리자 요청 수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int prepare(javax.transaction.xa.Xid xid)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *xid*  
  
 Xid 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 **int** 값입니다.  
  
## <a name="exceptions"></a>예외  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>주의  
 이 준비 메서드는 javax.transaction.xa.XAResource 인터페이스의 준비 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXAResource 메서드](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
