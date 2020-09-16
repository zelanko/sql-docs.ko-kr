---
description: getResultSetConcurrency 메서드(SQLServerStatement)
title: getResultSetConcurrency 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResultSetConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 47ef6547-5ec7-4cf5-a4d4-e34cbeec72eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c8cdec4c233f2a7d9241d63e3c1e6e29265157fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434775"
---
# <a name="getresultsetconcurrency-method-sqlserverstatement"></a>getResultSetConcurrency 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 의해 생성된 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 결과 집합 동시성을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int getResultSetConcurrency()  
```  
  
## <a name="return-value"></a>Return Value  
 결과 집합 동시성 유형을 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getResultSetConcurrency 메서드는 java.sql.Statement 인터페이스의 getResultSetConcurrency 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
