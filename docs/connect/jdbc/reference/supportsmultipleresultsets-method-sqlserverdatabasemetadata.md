---
title: "supportsMultipleResultSets 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
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
apiname: SQLServerDatabaseMetaData.supportsMultipleResultSets
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: cb4d0b91-db1d-4a6f-a87c-8ea125215afc
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 03d6c35d77f3d0b4be38fa8161b144b660e6c2f7
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="supportsmultipleresultsets-method-sqlserverdatabasemetadata"></a>supportsMultipleResultSets 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 가져오는 여러 지원 하는지 여부를 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 에서 한 번 호출 하는 개체는 [실행](../../../connect/jdbc/reference/execute-method.md) 의 메서드는 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)클래스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean supportsMultipleResultSets()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 지원 되는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 supportsMultipleResultSets 메서드는 java.sql.DatabaseMetaData 인터페이스의 supportsMultipleResultSets 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
