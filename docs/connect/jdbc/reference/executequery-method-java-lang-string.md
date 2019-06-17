---
title: executeQuery 메서드 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeQuery (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 610205c2-6bcd-426c-ad6f-9682551efdec
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3f881493288c385cb490f9d04b22acce03e19f29
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802304"
---
# <a name="executequery-method-javalangstring"></a>executeQuery 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 SQL 문을 실행하고 단일 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.sql.ResultSet executeQuery(java.lang.String sql)  
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
  
 이 메서드는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스에 있는 [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 메서드를 재정의합니다.  
  
 SQLServerPreparedStatement 개체에 대한 SQL 문은 개체가 만들어질 때 지정되므로 이 메서드를 호출하면 예외가 발생합니다.  
  
 지정된 SQL 문에서 단일 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 이외의 개체를 생성하면 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)이 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [executeQuery 메서드 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
