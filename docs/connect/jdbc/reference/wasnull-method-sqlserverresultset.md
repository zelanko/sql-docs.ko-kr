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
- SQLServerResultSet.wasNull
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d37f80ef-d72c-4429-ada3-1d685bdab6d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e1647f67f8967b1c5802061f829bcc8504fe557
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919443"
---
# <a name="wasnull-method-sqlserverresultset"></a>wasNull 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  마지막으로 읽은 값이 null 값이었는지 여부를 확인합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean wasNull()  
```  
  
## <a name="return-value"></a>Return Value  
 마지막으로 읽은 값이 null이었으면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 wasNull 메서드는 java.sql.ResultSet 인터페이스의 wasNull 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
