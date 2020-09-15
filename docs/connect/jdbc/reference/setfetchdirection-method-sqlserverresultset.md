---
description: setFetchDirection 메서드(SQLServerResultSet)
title: setFetchDirection 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ee82290-508d-4bff-a5c5-8a56338deef8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1056136ec3f7cef61e22c237d250fd6709c23e22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431895"
---
# <a name="setfetchdirection-method-sqlserverresultset"></a>setFetchDirection 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 행을 처리할 방향에 관한 힌트를 제공합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 현재 이 메서드가 지원되지 않습니다. 이 메서드를 사용할 경우 JDBC 드라이버에서는 설정을 기억하지만 현재는 이 메서드와 관련된 작업을 수행하지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setFetchDirection(int direction)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *direction*  
  
 제안된 페치 방향을 나타내는 **int**입니다. 다음 값 중 하나일 수 있습니다.  
  
 ResultSet.FETCH_FORWARD  
  
 ResultSet.FETCH_REVERSE  
  
 ResultSet.FETCH_UNKNOWN  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setFetchDirection 메서드는 java.sql.ResultSet 인터페이스의 setFetchDirection 메서드에 의해 지정됩니다.  
  
 이 메서드의 초기 값은 이 SQLServerResultSet 개체를 생성한 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 결정됩니다. 인출 방향은 언제든지 변경할 수 있습니다.  
  
> [!NOTE]  
>  커서 유형이 정방향 전용인 경우에는 이 메서드를 사용해도 아무 작업도 수행되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
