---
title: getJDBCMajorVersion 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getJDBCMajorVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 67b2bb4b-9714-4ba5-8739-50c632830451
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ac0527ac51c1a5c4a44e7fb7fbc26c5449ff6c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getjdbcmajorversion-method-sqlserverdatabasemetadata"></a>getJDBCMajorVersion 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 드라이버의 주 JDBC 버전 번호를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getJDBCMajorVersion()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 주 JDBC 버전을 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getJDBCMajorVersion 메서드는 java.sql.DatabaseMetaData 인터페이스의 getJDBCMajorVersion 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
