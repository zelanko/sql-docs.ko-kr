---
title: "isPoolable 메서드 (SQLServerStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b8a12ac5-57cb-4288-9973-c7d5cebd197c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 29c948e99dcb9411a427e96c1a9a0492c2d8992f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="ispoolable-method-sqlserverstatement"></a>isPoolable 메서드 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  사용자가 제공한 문 풀에 문을 추가할 수 있는지 여부를 나타내는 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isPoolable() throws SQLException  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** ; 사용자가 제공한 문 풀에 문을 추가할 수 있으면 **false** 그렇지 않은 경우.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 [setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md) 개체의 풀링 가능한 동작을 변경 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
