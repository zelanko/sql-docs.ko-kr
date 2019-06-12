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
- SQLServerResultSet.getRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a266e3bc-05c2-44e2-9346-125ae6780216
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 034378c7e5f8624fa945bcf696ee521606963063
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66762580"
---
# <a name="getrow-method-sqlserverresultset"></a>getRow 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행 번호를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getRow()  
```  
  
## <a name="return-value"></a>반환 값  
 현재 행 번호를 나타내는 **int**이거나, 행이 없는 경우 0입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getRow 메서드는 java.sql.ResultSet 인터페이스의 getRow 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
