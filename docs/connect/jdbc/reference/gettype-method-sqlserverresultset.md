---
description: getType 메서드(SQLServerResultSet)
title: getType 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffbc4a02-e851-431c-bc1a-7ab381d982bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c01dc19b6f9dfd1f1816c209f7c2168a68ceb85
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433965"
---
# <a name="gettype-method-sqlserverresultset"></a>getType 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 커서 유형을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getType()  
```  
  
## <a name="return-value"></a>Return Value  
 다음 값 중 하나에 해당되는 현재 커서 유형을 나타내는 **int**입니다.  
  
 ResultSet.TYPE_FORWARD_ONLY  
  
 ResultSet.TYPE_SCROLL_INSENSITIVE  
  
 ResultSet.TYPE_SCROLL_SENSITIVE  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getType 메서드는 java.sql.ResultSet 인터페이스의 getType 메서드에 의해 지정됩니다.  
  
 이 메서드는 실제 커서 유형을 결정하는 데 사용할 수 있습니다. 애플리케이션에서 TYPE_FORWARD_ONLY를 선택하거나 기본 커서 유형을 사용한 경우에는 TYPE_FORWARD_ONLY가 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
