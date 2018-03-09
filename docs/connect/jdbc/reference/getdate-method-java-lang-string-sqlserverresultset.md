---
title: "getDate 메서드 (java.lang.String) 열 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerResultSet.getDate (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 821058ae-cbe3-4a14-aa02-d55e45491437
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b20e134b918592f563d1e0630e25454635c46ac
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getdate-method-javalangstring-sqlserverresultset"></a>getDate 메서드 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 이름의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 java.sql.Date 개체로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Date getDate(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 A **문자열** 열 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 Date 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getDate 메서드는 java.sql.ResultSet 인터페이스의 getDate 메서드에 의해 지정 됩니다.  
  
 유효한 날짜 부분을 반환 하는이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] datetime 또는 smalldatetime 데이터 형식의 시간 부분은 Java 기준 시간인 00:00 (자정)으로 설정 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getDate 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
