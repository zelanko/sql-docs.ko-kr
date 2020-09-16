---
description: getMaxColumnsInTable 메서드(SQLServerDatabaseMetaData)
title: getMaxColumnsInTable 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInTable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dbcad2e1-7508-49ff-9f6d-db11200d87b6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 27938919042b645d6fad7936e2ab7f952865f895
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435595"
---
# <a name="getmaxcolumnsintable-method-sqlserverdatabasemetadata"></a>getMaxColumnsInTable 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스가 테이블에 허용하는 최대 열 수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getMaxColumnsInTable()  
```  
  
## <a name="return-value"></a>Return Value  
 허용되는 최대 열 수를 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getMaxColumnsInTable 메서드는 java.sql.DatabaseMetaData 인터페이스의 getMaxColumnsInTable 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
