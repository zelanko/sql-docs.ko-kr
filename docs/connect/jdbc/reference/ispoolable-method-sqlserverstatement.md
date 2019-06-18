---
title: isPoolable 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8a12ac5-57cb-4288-9973-c7d5cebd197c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a5fcc6d842299884bec758ca66f303bf3e8ed625
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796468"
---
# <a name="ispoolable-method-sqlserverstatement"></a>isPoolable 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  사용자가 제공한 문 풀에 문을 추가할 수 있는지 여부를 나타내는 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isPoolable() throws SQLException  
```  
  
## <a name="return-value"></a>반환 값  
 사용자가 제공한 문 풀에 문을 추가할 수 있으면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)은 개체의 풀링 가능한 동작을 변경합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
