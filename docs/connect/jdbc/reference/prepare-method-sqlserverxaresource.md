---
description: prepare 메서드(SQLServerXAResource)
title: prepare 메서드(SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.prepare
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f800c966-3fae-41b3-963a-464988f80da3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5df7e43a944180be9cf73bda5b65343022fd51c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432985"
---
# <a name="prepare-method-sqlserverxaresource"></a>prepare 메서드(SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 Xid 개체가 지정하는 트랜잭션의 트랜잭션 커밋을 준비하도록 리소스 관리자에 요청합니다.  
  
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
  
## <a name="remarks"></a>설명  
 이 prepare 메서드는 javax.transaction.xa.XAResource 인터페이스의 prepare 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAResource 메서드](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
