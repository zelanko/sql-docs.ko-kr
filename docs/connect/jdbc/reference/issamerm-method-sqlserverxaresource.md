---
description: isSameRM 메서드(SQLServerXAResource)
title: isSameRM 메서드(SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.isSameRM
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa24c46-b7cf-470a-afa1-52301847a448
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b35a775c8a8ed02dbbb634868e38b1d6c1579a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433415"
---
# <a name="issamerm-method-sqlserverxaresource"></a>isSameRM 메서드(SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  대상 개체가 나타내는 리소스 관리자 인스턴스가 지정된 XAResource 개체가 나타내는 리소스 관리자 인스턴스와 동일한지 확인합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isSameRM(javax.transaction.xa.XAResource xares)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *xares*  
  
 XAResource 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 인스턴스가 동일하면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>설명  
 이 commit 메서드는 javax.transaction.xa.XAResource 인터페이스의 commit 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAResource 메서드](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
