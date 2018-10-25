---
title: getHoldability 메서드 (SQLServerResultSet) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9cf27049e45c8e52c8a63a419327f377dd1f558f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841401"
---
# <a name="getholdability-method-sqlserverresultset"></a>getHoldability 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 유지 기능을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>반환 값  
 다음 유지 기능 수준 중 하나가 들어 있는 **int** 값입니다.  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getHoldability 메서드는 java.sql.ResultSet 인터페이스의 getHoldability 메서드에 의해 지정 됩니다.  
  
 결과 집합의 유지 기능을 설정하기 위해 응용 프로그램에서는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 메서드를 사용할 수 있습니다. [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 메서드가 호출되고 문 개체와 해당 결과 집합 개체가 만들어졌으며 문이 실행된 후에는 응용 프로그램에서 유지 기능을 다시 변경해야 할 수 있습니다.  
  
 서버 커서의 경우 SQL Server 2005 이상과 연결되어 있을 때 유지 기능을 설정하면 해당 연결에서 만들어질 새 결과 집합의 유지 기능만 영향을 받게 됩니다. 그러나 SQL Server 2000의 경우에는 유지 기능을 설정하면 기존 결과 집합과 해당 연결에서 만들어질 새 결과 집합의 유지 기능이 모두 영향을 받습니다.  
  
 유지 기능을 다시 설정 되 고 getHoldability 메서드가 호출 되 면 이전에 만들어진된 결과 집합 개체에이 메서드에서 반환 되는 값 다음 메서드에서 반환 되는 유지 기능 값 보다 다를 수 있습니다: Statement.getResultSetHoldability Connection.getHoldability, 또는 DatabaseMetaData.getResultSetHoldability 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
