---
title: setHoldability 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 552eebd0-4c38-43f0-961f-35244f99109b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe53c38e1b3f1633be27f4c82a9c2edfe9820495
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68213662"
---
# <a name="setholdability-method-sqlserverconnection"></a>setHoldability 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 개체를 사용하여 만든 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 유지 기능을 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setHoldability(int nNewHold)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *nNewHold*  
  
 다음 유지 기능 수준 중 하나가 들어 있는 **int** 값입니다.  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setHoldability 메서드는 java.sql.Connection 인터페이스의 setHoldability 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
