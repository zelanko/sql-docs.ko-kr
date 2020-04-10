---
title: supportsLikeEscapeClause 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsLikeEscapeClause
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cfb43430-88bf-4386-847a-10ea1e5ce7db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f2c062f1bf2235441be182d29af6bd3e83717fc1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80912959"
---
# <a name="supportslikeescapeclause-method-sqlserverdatabasemetadata"></a>supportsLikeEscapeClause 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 LIKE 이스케이프 절을 지정할 수 있는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean supportsLikeEscapeClause()  
```  
  
## <a name="return-value"></a>Return Value  
 지원되는 경우 **true**입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 supportsLikeEscapeClause 메서드는 java.sql.DatabaseMetaData 인터페이스의 supportsLikeEscapeClause 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
