---
title: "execute 메서드 (java.lang.String) (SQLServerStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerStatement.execute (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 64ac78b8-d5b3-4134-9b72-d2b0c52168a2
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3860a208491aab40235fcc19bbbc8750875d526e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="execute-method-javalangstring-sqlserverstatement"></a>execute 메서드 (java.lang.String) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  여러 결과를 반환할 수 있는 지정된 SQL 문을 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean execute(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 A **문자열** SQL 문이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 첫 번째 결과가 결과 집합이 면 합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 execute 메서드는 java.sql.Statement 인터페이스의 execute 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [방법 &#40; 실행 SQLServerStatement &#41;](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
