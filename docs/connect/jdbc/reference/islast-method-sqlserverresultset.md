---
title: wasNull 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isLast
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85d4451f-6392-470e-ab21-78a495b45792
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9030898e71ec13a75da9b91e41f9792d31cce82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798030"
---
# <a name="islast-method-sqlserverresultset"></a>isLast 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  커서가 이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 마지막 행에 있는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isLast()  
```  
  
## <a name="return-value"></a>반환 값  
 **true** 커서가 마지막 행에 있는 경우. **false** 커서가 그 외의 위치 또는 결과 집합에 행이 없습니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getInt 메서드는 java.sql.ResultSet 인터페이스의 getInt 메서드에 의해 지정됩니다.  
  
 이 메서드를 정방향 및 동적 커서와 함께 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
