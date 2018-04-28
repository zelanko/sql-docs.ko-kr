---
title: getDatabaseMajorVersion 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getDatabaseMajorVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 30860c07-e84b-428a-922a-ba63c070cd9c
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d01e8a07004ff6ed143f54118b8c62ded4c8c07
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getdatabasemajorversion-method-sqlserverdatabasemetadata"></a>getDatabaseMajorVersion 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  기본 데이터베이스의 주 버전 번호를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getDatabaseMajorVersion()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 데이터베이스 주 버전을 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getDatabaseMajorVersion 메서드는 java.sql.DatabaseMetaData 인터페이스의 getDatabaseMajorVersion 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
