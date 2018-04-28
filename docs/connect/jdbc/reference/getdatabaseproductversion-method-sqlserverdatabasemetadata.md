---
title: getDatabaseProductVersion 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getDatabaseProductVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19c0c15d-223f-45bd-a215-2867dfefecb0
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 565a7976b6d12fdef115a1e546498b8e27457353
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getdatabaseproductversion-method-sqlserverdatabasemetadata"></a>getDatabaseProductVersion 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스 제품의 버전 번호를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getDatabaseProductVersion()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 데이터베이스 제품 버전 번호가 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getDatabaseProductVersion 메서드는 java.sql.DatabaseMetaData 인터페이스의 getDatabaseProductVersion 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
