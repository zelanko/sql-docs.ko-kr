---
title: "getDouble 메서드 (java.lang.String) (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.getDouble (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3ee26412-43d2-404b-bc05-ffd0fc75805c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ebe750b3bf20da6154d03f292c158596dde2d1dd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getdouble-method-javalangstring-sqlserverresultset"></a>getDouble 메서드 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 이름의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **double** Java 프로그래밍 언어의에서 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public double getDouble(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 A **문자열** 열 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 A **double** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getDouble 메서드는 java.sql.ResultSet 인터페이스의 getDouble 메서드에 의해 지정 됩니다.  
  
 이 메서드는 Java 사용 하는 모든 숫자 기반 데이터 형식을 반환 **double** 충실도 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getDouble 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

