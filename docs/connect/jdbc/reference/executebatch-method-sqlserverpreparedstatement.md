---
title: "executeBatch 메서드 (SQLServerPreparedStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerPreparedStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8418167e-cbd2-464d-b118-73cdd76080ed
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c339a53bd782047db67bc58a61283ce9cd4cbe9e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="executebatch-method-sqlserverpreparedstatement"></a>executeBatch 메서드 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  실행할 명령 일괄 처리를 데이터베이스로 전송합니다. 모든 명령이 성공적으로 실행되면 업데이트 횟수의 배열을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>반환 값  
 업데이트 횟수가 들어 있는 정수 배열입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>주의  
 이 executeBatch 메서드는 java.sql.Statement 인터페이스의 executeBatch 메서드에 의해 지정 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0은 OUT 또는 INOUT 저장된 프로시저에서 허용 하는 경우 (PreparedStatement에서 상속) CallableStatement.executeBatch 메서드를 호출이는 BatchUpdateException를 throw 합니다 JDBC 4.0 권장 사항을 준수 매개 변수 또는 업데이트 횟수가 아닌 반환 합니다.  
  
 이 메서드를 재정의 [SQLServerStatement.executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

