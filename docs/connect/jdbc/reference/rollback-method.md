---
description: rollback 메서드()
title: rollback 메서드() | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.rollback ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7adb6772-4047-4d8e-931d-b3d20eec44b5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca2a2847f9d917872ee3a0b56bad50b184f58ea2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432675"
---
# <a name="rollback-method-"></a>rollback 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 트랜잭션에서 변경한 모든 내용을 취소하고 이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 현재 보유하고 있는 데이터베이스 잠금을 해제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void rollback()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 rollBack 메서드는java.sql.Connection 인터페이스의 rollBack 메서드에 의해 지정됩니다.  
  
 이 메서드는 자동 커밋 모드가 해제된 경우에만 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [rollback 메서드&#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
