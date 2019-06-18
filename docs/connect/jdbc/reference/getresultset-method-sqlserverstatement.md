---
title: getResultSet 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResultSet
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 929a14e2-8e98-4c32-89aa-86733c717ec1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 573a89f95dbebdf9a014f6b38e1aed94dabcb496
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66762705"
---
# <a name="getresultset-method-sqlserverstatement"></a>getResultSet 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 결과를 검색하여 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.sql.ResultSet getResultSet()  
```  
  
## <a name="return-value"></a>반환 값  
 ResultSet 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getResultSet 메서드는 java.sql.Statement 인터페이스의 getResultSet 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
