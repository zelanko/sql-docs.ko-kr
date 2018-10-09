---
title: getRow 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- MSQLServerResultSet.updateRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cfced0ca-a281-40dc-8d2f-370d5f0bf12b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d0a88a70cc6ed4b6bf1df83eb00806714324b0e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783021"
---
# <a name="updaterow-method-sqlserverresultset"></a>updateRow 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  기본 데이터베이스를 이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에 있는 새 내용으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateRow()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateRow 메서드는 java.sql.ResultSet 인터페이스의 updateRow 메서드에 의해 지정 됩니다.  
  
 커서가 삽입 행에 있는 경우에는 이 메서드를 호출할 수 없습니다.  
  
 열 값이 변경되지 않은 경우에 이 메서드를 호출하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
