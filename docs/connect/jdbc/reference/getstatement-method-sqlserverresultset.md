---
title: getStatement 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getStatement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7dea981b-b4fd-4f8d-954f-e686124627e2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f6a96d7bde4301c5789da402ebb58ab2a38295be
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926289"
---
# <a name="getstatement-method-sqlserverresultset"></a>getStatement 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 생성한 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Statement getStatement()  
```  
  
## <a name="return-value"></a>Return Value  
 SQLServerStatement 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getStatement 메서드는 java.sql.ResultSet 인터페이스의 getStatement 메서드에 의해 지정됩니다.  
  
 결과 집합이 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 메서드 등의 다른 방식으로 생성된 경우 이 메서드는 null을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
