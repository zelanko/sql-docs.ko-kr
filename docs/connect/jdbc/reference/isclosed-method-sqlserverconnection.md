---
description: isClosed 메서드(SQLServerConnection)
title: isClosed 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isClosed
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3560ab18-4350-4d02-9716-439f0c2f7142
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09d4a5e3c1d3634e52fd9b2d8244262c40fada06
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433595"
---
# <a name="isclosed-method-sqlserverconnection"></a>isClosed 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 닫혔는지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>Return Value  
 연결이 닫혀 있으면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 isClosed 메서드는java.sql.Connection 인터페이스의 isClosed 메서드에 의해 지정됩니다.  
  
 호출된 SQLServerConnection 개체의 상태를 확인합니다. 개체에서 [close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md) 메서드가 호출되었거나 치명적인 오류가 발생했으면 연결이 닫혀 있습니다. 이 메서드는 close 메서드가 호출된 후에 호출되는 경우에만 **true**를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
