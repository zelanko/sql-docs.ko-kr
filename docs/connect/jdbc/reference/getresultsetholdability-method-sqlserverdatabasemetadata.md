---
description: getResultSetHoldability 메서드(SQLServerDatabaseMetaData)
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
ms.openlocfilehash: d302a290ce0dcc88d6d27c2b3e01570cf596633e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434845"
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
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스와 함께 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]를 사용할 경우 이 메서드는 1을 반환합니다. 이 값은 ResultSet.HOLD_CURSORS_OVER_COMMIT 상수와 같습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
