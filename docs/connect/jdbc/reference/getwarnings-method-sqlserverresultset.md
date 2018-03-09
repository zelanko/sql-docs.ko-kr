---
title: "getWarnings 메서드 (SQLServerResultSet) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerResultSet.getWarnings
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: eb4339b0-383b-4337-a935-e8ec3f0d4123
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3df9fc832fdcdb1e5e2eb6c9393f397b8308e002
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getwarnings-method-sqlserverresultset"></a>getWarnings 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 호출에서 보고 된 첫 번째 경고 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
> [!NOTE]  
>  이 메서드는 현재 지원 되지 않습니다는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]합니다. 이 메서드를 호출하면 항상 null 값이 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.SQLWarning getWarnings()  
```  
  
## <a name="return-value"></a>반환 값  
 SQLWarning 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getWarnings 메서드는 java.sql.ResultSet 인터페이스의 getWarnings 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
