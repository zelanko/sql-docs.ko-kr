---
title: "refreshRow 메서드 (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 89452f34778b07f9e34b074beaf2b1e92f7be135
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="refreshrow-method-sqlserverresultset"></a>refreshRow 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터베이스의 최신 값으로 현재 행을 새로 고칩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void refreshRow()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 refreshRow 메서드는 java.sql.ResultSet 인터페이스의 refreshRow 메서드에 의해 지정 됩니다.  
  
 커서가 삽입 행에 있는 경우에는 이 메서드를 호출할 수 없습니다.  
  
 응용 프로그램에서는 이 메서드를 통해 데이터베이스에서 행을 다시 인출하도록 JDBC 드라이버에 명시적으로 지정할 수 있습니다. 응용 프로그램은이 메서드를 호출 해야 할 수 있습니다 때는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 캐싱 또는 데이터베이스에서 행의 최신 값을 사전 인출 합니다. 인출 크기가 1보다 크면 JDBC 드라이버에서는 실제로 여러 개의 행을 동시에 새로 고칠 수 있습니다.  
  
 모든 값은 트랜잭션 격리 수준과 커서 민감도에 따라 다시 인출됩니다. 이 메서드 호출 하기 전에 updater 메서드를 호출한 후 호출 되 면는 [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 메서드를 행에 대해 업데이트가 손실 됩니다. 이 메서드를 자주 호출하면 성능이 저하될 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

