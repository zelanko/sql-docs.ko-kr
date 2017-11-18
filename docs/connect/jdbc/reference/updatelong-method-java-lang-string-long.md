---
title: "updateLong 메서드 (java.lang.String, long) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.updateLong (java.lang.String, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6003706-35de-42b1-8f23-899a388adb5b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a6f1d1768ed72dd2d6cc6bf8c01b9aae85b6e3b0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatelong-method-javalangstring-long"></a>updateLong 메서드(java.lang.String, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  으로 지정된 된 열 업데이트는 **긴** 열 이름이 지정 된 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateLong(java.lang.String columnName,  
                       long x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 A **문자열** 열 이름이 들어 있는입니다.  
  
 *x*  
  
 A **긴** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateLong 메서드는 java.sql.ResultSet 인터페이스의 updateLong 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateLong 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

