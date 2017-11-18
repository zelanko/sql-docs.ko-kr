---
title: "getFetchDirection 메서드 (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2667676b22af4c4f25b8adfb4bb0565dd2e6abf9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getfetchdirection-method-sqlserverresultset"></a>getFetchDirection 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 대 한 인출 방향을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 현재 인출 방향을 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getFetchDirection 메서드는 java.sql.ResultSet 인터페이스의 getFetchDirection 메서드에 의해 지정 됩니다.  
  
 이 메서드를 호출 하 여 만든 마지막 설정 정방향 전용 커서에 대해 FETCH_FORWARD를 반환 합니다.는 [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) 메서드 다른 커서 유형에 대해 FETCH_UNKNOWN 경우 이러한 커서 유형을 반환 합니다는 setFetchDirection 메서드 호출 되지 않았습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

