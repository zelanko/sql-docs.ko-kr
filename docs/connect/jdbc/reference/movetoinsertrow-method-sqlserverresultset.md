---
title: "moveToInsertRow 메서드 (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.moveToInsertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3c54bfe-d5b7-4f6e-ae6c-3e8954e5b1c9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 396367249ad1b786064d6fc5685e505590bbc4af
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="movetoinsertrow-method-sqlserverresultset"></a>moveToInsertRow 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  커서를 삽입 행으로 이동합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void moveToInsertRow()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 moveToInsertRow 메서드는 java.sql.ResultSet 인터페이스의 moveToInsertRow 메서드에 의해 지정 됩니다.  
  
 현재 커서 위치는 커서가 삽입 행에 있는 동안 저장됩니다. 삽입 행은 업데이트할 수 있는 결과 집합과 연결된 특수한 행으로, 기본적으로는 결과 집합에 행을 추가하기 전에 updater 메서드를 호출하여 새 행을 생성할 수 있는 버퍼입니다.  
  
 Updater, getter 및 [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) 커서가 삽입 행에 있는 경우에 메서드를 호출할 수 있습니다. 지정 된 값이이 메서드를 호출할 때마다 및 insertRow를 호출 하기 전에 결과 집합의 모든 열 이어야 합니다. 또한 열 값에 대해 getter 메서드를 호출하려면 먼저 updater 메서드를 호출해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

