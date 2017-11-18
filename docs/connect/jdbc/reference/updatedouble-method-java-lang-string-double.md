---
title: "updateDouble 메서드 (java.lang.String, double) | Microsoft Docs"
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
- SQLServerResultSet.updateDouble (java.lang.String, double)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f70971d5-34cc-4f70-8a91-5d46356b24ae
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f2053f2c0a94bd18cbd6f0260fe3f3d1fda8d4ed
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatedouble-method-javalangstring-double"></a>updateDouble 메서드(java.lang.String, double)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  으로 지정된 된 열 업데이트는 **double** 열 이름이 지정 된 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateDouble(java.lang.String columnName,  
                         double x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 A **문자열** 열 이름이 들어 있는입니다.  
  
 *x*  
  
 A **double** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateDouble 메서드는 java.sql.ResultSet 인터페이스의 updateDouble 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateDouble 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

