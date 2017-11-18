---
title: "getTime 메서드 (int) (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.getTime (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e18c84f5-7171-4057-8c9e-fe1d43ae9c20
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5608722069507b813213fe4489da115b7f6f37b3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="gettime-method-int-sqlserverresultset"></a>getTime 메서드(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 인덱스의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 java.sql.Time 개체로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Time getTime(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 시간 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getTime 메서드는 java.sql.ResultSet 인터페이스의 getTime 메서드에 의해 지정 됩니다.  
  
 유효한 시간 부분을 반환 하는이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] datetime 또는 smalldatetime 데이터 형식의 날짜 부분은 Java 기준 날짜인 1970-01-01로 설정 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getTime 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

