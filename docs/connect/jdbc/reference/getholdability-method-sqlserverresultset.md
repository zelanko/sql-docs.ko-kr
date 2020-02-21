---
title: getHoldability 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57bf0cfc206319bf6afcb09435e8787499266c0c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982918"
---
# <a name="getholdability-method-sqlserverresultset"></a>getHoldability 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 유지 기능을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>Return Value  
 다음 유지 기능 수준 중 하나가 들어 있는 **int** 값입니다.  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getHoldability 메서드는 java.sql.ResultSet 인터페이스의 getHoldability 메서드에 의해 지정됩니다.  
  
 결과 집합의 유지 기능을 설정하기 위해 애플리케이션에서는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 메서드를 사용할 수 있습니다. [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 메서드가 호출되고 문 개체와 해당 결과 집합 개체가 만들어졌으며 문이 실행된 후에는 애플리케이션에서 유지 기능을 다시 변경해야 할 수 있습니다.  
  
 서버 커서의 경우 SQL Server 2005 이상과 연결되어 있을 때 유지 기능을 설정하면 해당 연결에서 만들어질 새 결과 집합의 유지 기능만 영향을 받게 됩니다. 그러나 SQL Server 2000의 경우에는 유지 기능을 설정하면 기존 결과 집합과 해당 연결에서 만들어질 새 결과 집합의 유지 기능이 모두 영향을 받습니다.  
  
 유지 기능이 다시 설정되고 이전에 만들어진 결과 집합 개체에 대해 getHoldability 메서드가 호출될 경우 이 메서드에서 반환되는 값은 Statement.getResultSetHoldability, Connection.getHoldability 또는 DatabaseMetaData.getResultSetHoldability 메서드에서 반환되는 유지 기능 값과 다를 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
