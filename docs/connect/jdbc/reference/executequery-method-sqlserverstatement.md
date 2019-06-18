---
title: executeQuery 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeQuery
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 599cf463-e19f-4baa-bacb-513cad7c6cd8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8755695a805684338378efa4427c24c333c3da08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796934"
---
# <a name="executequery-method-sqlserverstatement"></a>executeQuery 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 SQL 문을 실행하고 단일 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet executeQuery(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 SQL 문이 포함된 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 SQLServerResultSet 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 executeQuery 메서드는 java.sql.Statement 인터페이스의 executeQuery 메서드에 의해 지정됩니다.  
  
 지정된 SQL 문에서 단일 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 이외의 개체를 생성하면 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)이 발생합니다.  
  
 업데이트 횟수가 1보다 크거나 둘 이상의 결과 집합을 생성하는 저장 프로시저 결과를 실행하는 경우 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 사용하여 저장 프로시저를 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
