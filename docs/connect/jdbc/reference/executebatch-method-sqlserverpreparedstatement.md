---
title: "executeBatch 메서드 (SQLServerPreparedStatement) | Microsoft Docs"
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
- SQLServerPreparedStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8418167e-cbd2-464d-b118-73cdd76080ed
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 774a382c6e026094261ec562f21e11ba80dc85fb
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
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
    
 이 메서드를 재정의 [SQLServerStatement.executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
