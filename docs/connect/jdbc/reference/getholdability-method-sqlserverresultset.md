---
title: "getHoldability 메서드 (SQLServerResultSet) | Microsoft Docs"
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
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d413613719a5ea0adc8e323cfd8aaea205219d2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getholdability-method-sqlserverresultset"></a>getHoldability 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 유지 기능을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 다음 유지 기능 수준 중 하나를 포함 하는 값:  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getHoldability 메서드는 java.sql.ResultSet 인터페이스의 getHoldability 메서드에 의해 지정 됩니다.  
  
 결과 집합 유지 기능을 설정 하려면 응용 프로그램이 사용할 수는 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다. 이후에 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 메서드를 호출 하 고 문 개체와 해당 결과 집합 개체가 만들어집니다 및 문이 실행 되, 응용 프로그램의 유지 기능을 다시 변경 해야 할 수 있습니다.  
  
 서버 커서의 경우 SQL Server 2005 이상과 연결되어 있을 때 유지 기능을 설정하면 해당 연결에서 만들어질 새 결과 집합의 유지 기능만 영향을 받게 됩니다. 그러나 SQL Server 2000의 경우에는 유지 기능을 설정하면 기존 결과 집합과 해당 연결에서 만들어질 새 결과 집합의 유지 기능이 모두 영향을 받습니다.  
  
 개체에 이전에 만들어진된 결과 집합 유지 기능이 다시 설정 되 고 getHoldability 메서드가 호출 되 면,이 메서드에 의해 반환 되는 값은 다음 방법으로 반환 되는 유지 기능 값 보다 다를 수 있습니다: Statement.getResultSetHoldability Connection.getHoldability, 또는 DatabaseMetaData.getResultSetHoldability 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
