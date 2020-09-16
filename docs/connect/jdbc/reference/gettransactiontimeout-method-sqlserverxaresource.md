---
description: getTransactionTimeout 메서드(SQLServerXAResource)
title: getTransactionTimeout 메서드(SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.getTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed0a37e9-1132-4d3f-b88f-8be674e852b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a8b8605ab9c9acf4872a93ed305da7cb01fef85c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434005"
---
# <a name="gettransactiontimeout-method-sqlserverxaresource"></a>getTransactionTimeout 메서드(SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체에 대해 설정된 현재 트랜잭션 시간 제한 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getTransactionTimeout()  
```  
  
## <a name="exceptions"></a>예외  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>설명  
 이 getTransactionTimeout 메서드는 javax.transaction.xa.XAResource 인터페이스의 getTransactionTimeout 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAResource 메서드](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
