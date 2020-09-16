---
description: getMaxFieldSize 메서드(SQLServerStatement)
title: getMaxFieldSize 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed7bbcb8-660b-4e9b-8241-e216c42826f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0930c5ab4b3c2e907a6de9caeef96f78d57e2737
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435565"
---
# <a name="getmaxfieldsize-method-sqlserverstatement"></a>getMaxFieldSize 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 문자 및 이진 열 값에 대해 반환될 수 있는 최대 바이트 수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int getMaxFieldSize()  
```  
  
## <a name="return-value"></a>Return Value  
 열에 포함될 수 있는 최대 바이트 수를 나타내는 **int**이거나, 제한이 없는 경우 0입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getMaxFieldSize 메서드는 java.sql.Statement 인터페이스의 getMaxFieldSize 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 메서드](../../../connect/jdbc/reference/sqlserverstatement-methods.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
