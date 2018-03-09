---
title: "getRowIdLifetime 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
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
ms.assetid: 317c0b44-fe3f-4142-9cab-e40e4c4fe070
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c547ec7b433f0cbccc66e79db4906879f7012225
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getrowidlifetime-method-sqlserverdatabasemetadata"></a>getRowIdLifetime 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQL RowId 데이터 형식이 지원되는지 여부를 나타내는 상태를 반환합니다. 이 데이터 형식이 지원되는 경우 이 메서드는 RowId 개체가 유효한 상태로 있는 수명을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.RowIdLifetime getRowIdLifetime()  
```  
  
## <a name="return-value"></a>반환 값  
 RowIdLifetime 개체입니다.  
  
> [!NOTE]  
>  JDBC 드라이버 버전 2.0 릴리스에서이 메서드는 java.sql.RowIdLifetime.ROWID_UNSUPPORTED 값을 반환합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getRowIdLifetime 메서드는 java.sql.DatabaseMetaData 인터페이스의 getRowIdLifetime 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
