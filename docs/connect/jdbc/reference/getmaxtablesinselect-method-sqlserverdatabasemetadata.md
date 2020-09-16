---
description: getMaxTablesInSelect 메서드(SQLServerDatabaseMetaData)
title: getMaxTablesInSelect 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxTablesInSelect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f5291217-2a0c-4daa-9e39-9f348fc911f7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 270f7dfcc8c276fec790dcd2afa47e3f6394fcec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435475"
---
# <a name="getmaxtablesinselect-method-sqlserverdatabasemetadata"></a>getMaxTablesInSelect 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스가 SELECT 문에 허용하는 최대 테이블 수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getMaxTablesInSelect()  
```  
  
## <a name="return-value"></a>Return Value  
 허용되는 최대 테이블 수를 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getMaxTablesInSelect 메서드는 java.sql.DatabaseMetaData 인터페이스의 getMaxTablesInSelect 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
