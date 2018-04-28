---
title: executeUpdate 메서드 (java.lang.String) (SQLServerStatement) | Microsoft Docs
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
- SQLServerStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85e7c3a2-f2da-49bf-9d90-5fd246fd60e1
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 67b71b307337245ec0466c6f80868c75fc246b3f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="executeupdate-method-javalangstring-sqlserverstatement"></a>executeUpdate 메서드(java.lang.String)(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  INSERT, UPDATE 또는 DELETE 문과 같은 지정된 SQL 문이나 SQL DDL 문 같이 아무 것도 반환하지 않는 SQL 문을 실행합니다. 부터는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0에서는 executeUpdate 병합 작업에서 업데이트 된 행의 올바른 수를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int executeUpdate(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 A **문자열** SQL 문이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 **int** DDL 문을 사용 하는 경우 0, 영향을 받는 행의 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 executeUpdate 메서드는 java.sql.Statement 인터페이스의 executeUpdate 메서드에 의해 지정 됩니다.  
  
 1 보다 큰 또는 둘 이상의 결과 집합을 사용 하 여 생성 하 여 업데이트 횟수로 인해 저장된 프로시저를 실행 하는 경우는 [실행](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 저장된 프로시저를 실행 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [executeUpdate 메서드 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
