---
title: "executeQuery 메서드 (SQLServerStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.executeQuery
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 599cf463-e19f-4baa-bacb-513cad7c6cd8
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 806cde82a3e1556ef4df93eb4916ae14ae19c8c9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="executequery-method-sqlserverstatement"></a>executeQuery 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 SQL 문을 실행 하 고는 단일 반환 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet executeQuery(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 A **문자열** SQL 문이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 
          SQLServerResultSet 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 executeQuery 메서드는 java.sql.Statement 인터페이스의 executeQuery 메서드에 의해 지정 됩니다.  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 이외의 노드에 단일 지정된 된 SQL 문을 생성 되는 경우 throw 되 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
 1 보다 큰 또는 둘 이상의 결과 집합을 사용 하 여 생성 하 여 업데이트 횟수로 인해 저장된 프로시저를 실행 하는 경우는 [실행](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 저장된 프로시저를 실행 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

