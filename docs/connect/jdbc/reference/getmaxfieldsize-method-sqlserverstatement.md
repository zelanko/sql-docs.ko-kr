---
title: "getMaxFieldSize 메서드 (SQLServerStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.getMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed7bbcb8-660b-4e9b-8241-e216c42826f9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46b9cb942a8adf671e0755da571283fa60b4fe87
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getmaxfieldsize-method-sqlserverstatement"></a>getMaxFieldSize 메서드 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  바이트의 문자 및 이진 열 값에 대 한 반환 될 수 있는 최대 수를 검색 한 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 이 생성 되는 개체 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int getMaxFieldSize()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 제한이 없는 경우 0 열이 포함할 수 있는 바이트의 최대 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getMaxFieldSize 메서드는 java.sql.Statement 인터페이스의 getMaxFieldSize 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 메서드](../../../connect/jdbc/reference/sqlserverstatement-methods.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
