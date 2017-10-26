---
title: "updateBoolean 메서드 (int, boolean) | Microsoft Docs"
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
- SQLServerResultSet.updateBoolean (int, boolean)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7937f4bb-8537-4012-af81-837f9ac123a2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4b86ef004e5da959c94c24166a93f5c05e5a3484
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updateboolean-method-int-boolean"></a>updateBoolean 메서드(int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  으로 지정된 된 열 업데이트는 **부울** 열 인덱스가 지정 된 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBoolean(int index,  
                          boolean x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *인덱스*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
 *x*  
  
 A **부울** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateBoolean 메서드는 java.sql.ResultSet 인터페이스의 updateBoolean 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateBoolean 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

