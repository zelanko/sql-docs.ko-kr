---
title: "usesLocalFilePerTable 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
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
apiname: SQLServerDatabaseMetaData.usesLocalFilePerTable
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 1fafb076-2bb7-4845-9c02-788479f00ca2
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 506d7a6edf3c4ab113a3796fde5ad87acbf930a4
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="useslocalfilepertable-method-sqlserverdatabasemetadata"></a>usesLocalFilePerTable 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 각 테이블에 대해 개별 파일을 사용하는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean usesLocalFilePerTable()  
```  
  
## <a name="return-value"></a>반환 값  
 **true** 각 테이블에 대 한 파일을 사용 합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 usesLocalFilePerTable 메서드는 java.sql.DatabaseMetaData 인터페이스의 usesLocalFilePerTable 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
