---
title: "setFetchSize 메서드 (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed3f37d12253c03ae192b03db27caf4d180e568d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setfetchsize-method-sqlserverresultset"></a>setFetchSize 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터베이스에서이 대 한 추가 행이 필요할 때 인출 되는 행 수에 관한 힌트를 JDBC 드라이버에 제공 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *행*  
  
 **int** 인출할 행 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setFetchSize 메서드는 java.sql.ResultSet 인터페이스의 setFetchSize 메서드로 지정 됩니다.  
  
 지정된 인출 크기가 0이면 JDBC 드라이버는 이 값을 무시하고 필요한 인출 크기를 예측합니다. 기본 값을 설정한는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 결과 집합 생성 개체입니다. 인출 크기는 언제든지 변경할 수 있습니다.  
  
 이 메서드는 서버 커서의 블록 인출 크기를 변경하며, 다음에 JDBC 드라이버에서 sp_cursorfetch를 호출해야 할 때 적용됩니다. 인출 크기를 0으로 설정하면 현재 사용 중인 커서 유형의 기본 인출 크기가 복원됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

