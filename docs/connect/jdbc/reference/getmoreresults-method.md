---
title: getMoreResults 메서드() | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMoreResults ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: df89db50-0b2f-4094-820a-30be25ad72fe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dcbce9783641376ae142e94ab5e45dc47fe16fef
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67981735"
---
# <a name="getmoreresults-method-"></a>getMoreResults 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 다음 결과로 이동합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final boolean getMoreResults()  
```  
  
## <a name="return-value"></a>Return Value  
 반환된 결과가 결과 집합이면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getMoreResults 메서드는 java.sql.Statement 인터페이스의 getMoreResults 메서드에 의해 지정됩니다.  
  
 getMoreResults 메서드를 호출하면 [getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 메서드를 사용하여 가져온 현재 열려 있는 결과 집합 개체가 암시적으로 닫힙니다.  
  
## <a name="see-also"></a>참고 항목  
 [getMoreResults 메서드(SQLServerStatement)](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
