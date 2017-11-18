---
title: "getAutoCommit 메서드 (SQLServerConnection) | Microsoft Docs"
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
- SQLServerConnection.getAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: af1f67f4-f568-4e58-abcc-5c809a89b547
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e2c8ee804ede53953f531fe945da39c7c0667cae
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getautocommit-method-sqlserverconnection"></a>getAutoCommit 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 대 한 현재 자동 커밋 모드를 검색 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getAutoCommit()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 자동 커밋 모드가 사용 될 경우 **false** 없는 경우.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getAutoCommit 메서드는 java.sql.Connection 인터페이스의 getAutoCommit 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

