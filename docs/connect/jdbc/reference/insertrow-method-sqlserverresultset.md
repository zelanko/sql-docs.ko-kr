---
title: insertRow 메서드 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 106743625ef17e733836ec9430f2f171af2b0d72
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="insertrow-method-sqlserverresultset"></a>insertRow 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 삽입 행의 내용을 추가 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 및 데이터베이스에 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 insertRow 메서드는 java.sql.ResultSet 인터페이스의 insertRow 메서드에 의해 지정 됩니다.  
  
 이 메서드를 호출할 때 커서는 삽입 행에 있어야 합니다. 이 메서드를 호출한 후 커서는 삽입 행에 계속 있으며 결과 집합도 삽입 모드에 계속 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
