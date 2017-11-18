---
title: "setHoldability 메서드 (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.setHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 552eebd0-4c38-43f0-961f-35244f99109b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cfc1f5eb9b3c6368cfe0dd659146bcfa7353bf89
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setholdability-method-sqlserverconnection"></a>setHoldability 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  유지 기능을 변경 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 이 사용 하 여 만든 개체 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 를 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setHoldability(int nNewHold)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *nNewHold*  
  
 **int** 다음 유지 기능 수준 중 하나를 포함 하는 값:  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setHoldability 메서드는 java.sql.Connection 인터페이스의 setHoldability 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

