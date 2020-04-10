---
title: rollback 메서드(SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.rollback
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 93d9d7e6-54b6-4d86-8f8c-386c6057e85e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d129913a4946d5887a100bd4a295c344a951c2f0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80903795"
---
# <a name="rollback-method-sqlserverxaresource"></a>rollback 메서드(SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  리소스 관리자에 트랜잭션 분기 대신 수행된 작업을 롤백하도록 요청합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void rollback(javax.transaction.xa.Xid xid)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *xid*  
  
 Xid 개체입니다.  
  
## <a name="exceptions"></a>예외  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>설명  
 이 rollback 메서드는 javax.transaction.xa.XAResource 인터페이스의 rollback 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAResource 메서드](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
