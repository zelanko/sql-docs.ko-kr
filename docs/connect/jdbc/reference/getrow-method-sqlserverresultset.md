---
description: getRow 메서드(SQLServerResultSet)
title: getRow 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a266e3bc-05c2-44e2-9346-125ae6780216
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1ba4cb923fcc9c3bae1f2dba7dca31d1bc78815
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434725"
---
# <a name="getrow-method-sqlserverresultset"></a>getRow 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행 번호를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getRow()  
```  
  
## <a name="return-value"></a>Return Value  
 현재 행 번호를 나타내는 **int**이거나, 행이 없는 경우 0입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getRow 메서드는 java.sql.ResultSet 인터페이스의 getRow 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
