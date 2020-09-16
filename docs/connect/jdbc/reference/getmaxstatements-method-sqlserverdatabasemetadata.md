---
description: getMaxStatements 메서드(SQLServerDatabaseMetaData)
title: getMaxStatements 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxStatements
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 71d58431-b671-49c5-939a-f581d1fef7cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 65b697414aadc3ded169cd70f19f8f923886c699
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435495"
---
# <a name="getmaxstatements-method-sqlserverdatabasemetadata"></a>getMaxStatements 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에 대해 동시에 열릴 수 있는 최대 활성 문 수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getMaxStatements()  
```  
  
## <a name="return-value"></a>Return Value  
 허용되는 최대 활성 문 수를 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getMaxStatements 메서드는 java.sql.DatabaseMetaData 인터페이스의 getMaxStatements 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
