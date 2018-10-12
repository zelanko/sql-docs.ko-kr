---
title: insertRow 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 611ba86c25f78cda15fcac53d8f31311d88e4840
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696873"
---
# <a name="insertrow-method-sqlserverresultset"></a>insertRow 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체와 해당 데이터베이스에 삽입 행의 내용을 추가합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 insertRow 메서드는 java.sql.ResultSet 인터페이스의 insertRow 메서드에 의해 지정됩니다.  
  
 이 메서드를 호출할 때 커서는 삽입 행에 있어야 합니다. 이 메서드를 호출한 후 커서는 삽입 행에 계속 있으며 결과 집합도 삽입 모드에 계속 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
