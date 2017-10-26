---
title: "updateTime 메서드 (int, java.sql.Time) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.updateTime (int, java.sql.Time)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fa7a3ca5-1111-4480-97ca-65b632aa1e5b
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 52340aab2c4aebd04f3d5549353f294bfe72b607
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatetime-method-int-javasqltime"></a>updateTime 메서드(int, java.sql.Time)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열 인덱스가 지정된 경우 지정된 열을 시간 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateTime(int index,  
                       java.sql.Time x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *인덱스*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
 *x*  
  
 시간 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateTime 메서드는 java.sql.ResultSet 인터페이스의 updateTime 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateTime 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

