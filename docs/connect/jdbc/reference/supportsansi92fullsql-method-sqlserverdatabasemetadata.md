---
title: supportsANSI92FullSQL 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsANSI92FullSQL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8877dc8c-26cd-4374-8ae8-ff7d20621130
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fcad4dae62be2e2185848acc2ea5aa3562e60ce1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969839"
---
# <a name="supportsansi92fullsql-method-sqlserverdatabasemetadata"></a>supportsANSI92FullSQL 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 ANSI92 전체 SQL 문법을 지원하는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean supportsANSI92FullSQL()  
```  
  
## <a name="return-value"></a>Return Value  
 지원되는 경우 **true**입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 supportsANSI92FullSQL 메서드는 java.sql.DatabaseMetaData 인터페이스의 supportsANSI92FullSQL 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
