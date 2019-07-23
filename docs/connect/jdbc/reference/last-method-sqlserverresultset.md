---
title: last 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.last
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ac9bef59-8c31-437b-a183-619cc778fe7a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bf176794b2fac5a241c14ee494d08ddd4aa98dbc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976894"
---
# <a name="last-method-sqlserverresultset"></a>last 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  커서를 이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 마지막 행으로 이동합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean last()  
```  
  
## <a name="return-value"></a>반환 값  
 새 현재 행이 올바르면 **true** 입니다. 처리할 행이 더 이상 없는 경우 **false** 입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 last 메서드는 java.sql.ResultSet 인터페이스의 last 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
