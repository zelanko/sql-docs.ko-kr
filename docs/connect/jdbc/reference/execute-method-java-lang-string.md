---
title: execute 메서드(java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.execute (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a871917e-d286-46c3-96cf-2e8e8b22111c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09adea323a5a2930e9c636a1b2e1b00567dbd9ce
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954955"
---
# <a name="execute-method-javalangstring"></a>execute 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  여러 결과를 반환할 수 있는 지정된 SQL 문을 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final boolean execute(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 SQL 문이 포함된 **문자열**입니다.  
  
## <a name="return-value"></a>Return Value  
 문이 결과 집합을 반환하는 경우 **true**입니다. 업데이트 수를 반환하거나 결과를 반환하지 않는 경우 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 execute 메서드는 java.sql.Statement 인터페이스의 execute 메서드에 의해 지정됩니다.  
  
 이 메서드는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스에 있는 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 재정의합니다.  
  
 SQLServerPreparedStatement 개체에 대한 SQL 문은 개체가 만들어질 때 지정되므로 이 메서드를 호출하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [execute 메서드&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
