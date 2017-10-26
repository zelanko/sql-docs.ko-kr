---
title: "getMaxSchemaNameLength 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getMaxSchemaNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fece19e9-3bf8-4299-9188-ac3df5ce9c19
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7d7da43c56ec676d199647af1a0a72cbda126ada
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getmaxschemanamelength-method-sqlserverdatabasemetadata"></a>getMaxSchemaNameLength 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스가 스키마 이름에 허용하는 최대 문자 수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getMaxSchemaNameLength()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 허용 되는 문자의 최대 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getMaxSchemaNameLength 메서드는 java.sql.DatabaseMetaData 인터페이스의 getMaxSchemaNameLength 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

