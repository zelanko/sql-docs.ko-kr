---
title: setMaxRows 메서드 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f697921ebeb05416555495197812e818a2d1058e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="setmaxrows-method-sqlserverstatement"></a>setMaxRows 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  최대 행 수에 대 한 제한을 설정 하는 모든 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체는 지정된 된 숫자를 포함할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *max*  
  
 **int** 행 또는 0의 최대 수 있는지 여부를 나타내는 제한이 없습니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setMaxRows 메서드는 java.sql.Statement 인터페이스의 setMaxRows 메서드에 의해 지정 됩니다.  
  
 이 setMaxRows 메서드는 동적 스크롤 가능 커서에 대 한 영향을 주지 않습니다. 응용 프로그램에서는 SELECT TOP N SQL 구문을 사용하여 크기가 커질 수 있는 결과 집합에서 반환되는 행 수를 제한해야 합니다.  
  
 SetMaxRows 메서드를 호출 하는 경우는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 응용 프로그램의 쿼리를 실행할 때 SET ROWCOUNT SQL 문을 실행 합니다. 이 인해 모든 영향을 받는 행의 최대 수를 제한 하려면 JDBC 드라이버는 [!INCLUDE[tsql](../../../includes/tsql_md.md)] 해당 쿼리에서 반환 된 행 수 뿐만 아니라 해당 쿼리에서 실행 된 문의 합니다. 최상위 수준에 대해서만 설정 하는 응용 프로그램에서 필요로 하는 경우 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 setMaxRows 메서드 대신 쿼리에 SELECT TOP N SQL 구문을 사용 해야 합니다.  
  
 SET ROWCOUNT SQL 문에 대 한 자세한 내용은 참조는 "[SET ROWCOUNT (TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=139522)" 항목을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
