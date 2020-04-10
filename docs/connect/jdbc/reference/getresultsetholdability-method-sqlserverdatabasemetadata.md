---
title: getResultSetHoldability 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData,getResultSetHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f0bd6283-83ab-4a0a-b825-ec4cdccf03e1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 137f2388f940bfbf17038af3288dea6c8b944e26
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921852"
---
# <a name="getresultsetholdability-method-sqlserverdatabasemetadata"></a>getResultSetHoldability 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에 대한 결과 집합의 기본 유지 기능을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getResultSetHoldability()  
```  
  
## <a name="return-value"></a>Return Value  
 기본 유지 기능을 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getResultSetHoldability 메서드는 java.sql.DatabaseMetaData 인터페이스의 getResultSetHoldability 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 데이터베이스와 함께 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용할 경우 이 메서드는 1을 반환합니다. 이 값은 ResultSet.HOLD_CURSORS_OVER_COMMIT 상수와 같습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
