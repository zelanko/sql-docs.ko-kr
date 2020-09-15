---
description: setMaxRows 메서드(SQLServerStatement)
title: setMaxRows 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 544eb34b40bc81afbed34809f3348c5649c3d0be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431765"
---
# <a name="setmaxrows-method-sqlserverstatement"></a>setMaxRows 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 포함될 수 있는 최대 행 수에 대한 제한을 지정된 수로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *max*  
  
 최대 행 수를 나타내는 **int**이며, 제한이 없는 경우에는 0입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setMaxRows 메서드는 java.sql.Statement 인터페이스의 setMaxRows 메서드에 의해 지정됩니다.  
  
 이 setMaxRows 메서드는 동적 스크롤 가능 커서에는 아무런 영향을 주지 않습니다. 애플리케이션에서는 SELECT TOP N SQL 구문을 사용하여 크기가 커질 수 있는 결과 집합에서 반환되는 행 수를 제한해야 합니다.  
  
 setMaxRows 메서드가 호출되면 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 애플리케이션의 쿼리를 실행할 때 SET ROWCOUNT SQL 문을 실행합니다. 이로 인해 JDBC 드라이버에서는 해당 쿼리에서 반환되는 행 수뿐만 아니라 해당 쿼리에서 실행되는 모든 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문의 영향을 받는 최대 행 수도 제한하게 됩니다. 애플리케이션에서 최상위 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 대한 제한만 설정해야 하는 경우에는 setMaxRows 메서드 대신 쿼리에 SELECT TOP N SQL 구문을 사용해야 합니다.  
  
 SET ROWCOUNT SQL 문에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “[SET ROWCOUNT(Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=139522)” 항목을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
