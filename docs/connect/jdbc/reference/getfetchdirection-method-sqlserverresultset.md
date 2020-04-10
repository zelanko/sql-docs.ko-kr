---
title: getFetchDirection 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73a507e48b4ecc7f1ead7e33fe6936f5ed73f424
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924833"
---
# <a name="getfetchdirection-method-sqlserverresultset"></a>getFetchDirection 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 인출 방향을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>Return Value  
 현재 인출 방향을 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getFetchDirection 메서드는 java.sql.ResultSet 인터페이스의 getFetchDirection 메서드에 의해 지정됩니다.  
  
 이 메서드는 정방향 전용 커서에 대해 FETCH_FORWARD를 반환하고, 다른 커서 형식에 대해서는 [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) 메서드를 호출하여 만든 마지막 설정을 반환하며, setFetchDirection 메서드를 호출한 적이 없는 경우에는 이러한 커서 형식에 대해 FETCH_UNKNOWN을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
