---
title: executeBatch 메서드(SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8418167e-cbd2-464d-b118-73cdd76080ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 463106c14a63feddb68998affff8131933e81dfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954895"
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
  
## <a name="remarks"></a>Remarks  
 이 executeBatch 메서드는 java.sql.Statement 인터페이스의 executeBatch 메서드에 의해 지정됩니다.  
    
 이 메서드는 [SQLServerStatement.executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)를 재정의합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
