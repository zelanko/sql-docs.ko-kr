---
title: getString 메서드(java.lang.String)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerResultSet.getString (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a98c8a8-61d0-40c9-9335-25a87b732dc3
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 07f6a17c49143fcb0ca6cffd2656ce200bedf2e1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getstring-method-javalangstring-sqlserverresultset"></a>getString 메서드(java.lang.String)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 이름의 값을 검색하여 Java 프로그래밍 언어의 **문자열**로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getString(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 **문자열** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getString 메서드는 java.sql.ResultSet 인터페이스의 getString 메서드에 의해 지정됩니다.  
  
 SQL Server의 모든 열은 String으로 반환될 수 있습니다. 즉, 모든 숫자 기반 및 문자 기반 형식의 **문자열** 표현과 binary, varbinary, varbinary(max), image, timestamp 및 uniqueidentifier 같은 이진 열의 16진수 문자 표현이 반환될 수 있습니다.  
  
 money, smallmoney, datetime, smalldatetime, float, real, decimal 및 numeric과 같이 위치에 영향을 받는 형식은 해당 형식의 기본 값에 대해 정규 toString() 형식을 반환합니다.  
  
 사용자 정의 형식은 16진수 **문자열** 값으로 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getString 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
