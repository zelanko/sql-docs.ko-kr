---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45e56a0a5ddb7cf8aece6813d421b7ebb1685408
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977709"
---
# <a name="isclosed-method-sqlserverconnection"></a>isClosed 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 닫혔는지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>반환 값  
 연결이 종료 되 면 **true** 이 고, 그렇지 않으면 **false** 입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 isClosed 메서드는java.sql.Connection 인터페이스의 isClosed 메서드에 의해 지정됩니다.  
  
 호출 된 SQLServerConnection 개체의 상태를 확인 합니다. 개체에서 [close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md) 메서드가 호출되었거나 치명적인 오류가 발생했으면 연결이 닫혀 있습니다. 이 메서드는 close 메서드가 호출된 후에 호출되는 경우에만 **true**를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
