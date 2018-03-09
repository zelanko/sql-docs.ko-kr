---
title: "executeQuery 메서드 (java.lang.String) | Microsoft Docs"
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
apiname: SQLServerPreparedStatement.executeQuery (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 610205c2-6bcd-426c-ad6f-9682551efdec
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d848338f8f4599e07c7c71b0b723150499ec6054
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="executequery-method-javalangstring"></a>executeQuery 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 SQL 문을 실행 하 고는 단일 반환 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.sql.ResultSet executeQuery(java.lang.String sql)  
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
  
 이 메서드를 재정의 [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 에서 발견 되는 메서드는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스입니다.  
  
 이 메서드를 호출 개체가 만들어질 때 SQLServerPreparedStatement 개체에 대 한 SQL 문이 지정 된 후 예외가 발생 합니다.  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 이외의 노드에 단일 지정된 된 SQL 문을 생성 되는 경우 throw 되 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [executeQuery 메서드 &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
