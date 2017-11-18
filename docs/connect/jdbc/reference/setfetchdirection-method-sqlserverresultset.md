---
title: "setFetchDirection 메서드 (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ee82290-508d-4bff-a5c5-8a56338deef8
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dd6ab9a94acf883ed27cdd79fee886b6c54ca596
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setfetchdirection-method-sqlserverresultset"></a>setFetchDirection 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  방향에 관한 힌트를 제공이 행 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 처리 됩니다.  
  
> [!NOTE]  
>  이 메서드는 현재 지원 되지 않습니다는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]합니다. 이 메서드를 사용할 경우 JDBC 드라이버에서는 설정을 기억하지만 현재는 이 메서드와 관련된 작업을 수행하지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setFetchDirection(int direction)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *방향*  
  
 **int** 권장된 인출 방향을 나타내는입니다. 다음 값 중 하나를 사용할 수 있습니다.  
  
 ResultSet.FETCH_FORWARD  
  
 ResultSet.FETCH_REVERSE  
  
 ResultSet.FETCH_UNKNOWN  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setFetchDirection 메서드는 java.sql.ResultSet 인터페이스의 setFetchDirection 메서드로 지정 됩니다.  
  
 이 메서드의 초기 값 결정 되는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 이 SQLServerResultSet 개체를 생성 하는 개체입니다. 인출 방향은 언제든지 변경할 수 있습니다.  
  
> [!NOTE]  
>  커서 유형이 정방향 전용인 경우에는 이 메서드를 사용해도 아무 작업도 수행되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

