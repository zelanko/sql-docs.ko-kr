---
title: getMaxRows 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d4ca4ff73b30796084ae8cb7dd51a1438d3642e9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66792486"
---
# <a name="getmaxrows-method-sqlserverstatement"></a>getMaxRows 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 포함될 수 있는 최대 행 수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>반환 값  
 최대 행 수를 나타내는 **int**이며, 제한이 없는 경우에는 0입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getMaxRows 메서드는 java.sql.Statement 인터페이스의 getMaxRows 메서드에 의해 지정 됩니다.  
  
 동적 스크롤 가능 커서의 경우 이 getMaxRows 메서드는 항상 0을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
