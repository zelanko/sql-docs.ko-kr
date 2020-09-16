---
description: getTime 메서드(int, java.util.Calendar)(SQLServerResultSet)
title: getTime 메서드(int, java.util.Calendar)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTime (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d21e0c1d-9d6e-468f-8b11-cc7209b2c2e5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b647e4dff3980e5828a92d54866f17ddf8790d97
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434245"
---
# <a name="gettime-method-int-javautilcalendar-sqlserverresultset"></a>getTime 메서드(int, java.util.Calendar)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 인덱스의 값을 지정된 Calendar 개체를 사용하여 Java 프로그래밍 언어의 java.sql.Time 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Time getTime(int columnIndex,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *cal*  
  
 Calendar 개체입니다.  
  
## <a name="return-value"></a>Return Value  
 Time 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getTime 메서드는 java.sql.ResultSet 인터페이스의 getTime 메서드에 의해 지정됩니다.  
  
 이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 또는 smalldatetime 데이터 형식의 유효한 시간 부분을 반환합니다. 이때 날짜 부분은 제공된 달력의 표준 시간대에서 Java 기준 날짜인 1970/01/01로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getTime 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
