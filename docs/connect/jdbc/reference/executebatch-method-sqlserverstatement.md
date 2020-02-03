---
title: executeBatch 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fb034f63-2532-4da8-a1b0-bc125734585a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d05b367901aae7a37e10b0a2091a268c3a78a7b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67954833"
---
# <a name="executebatch-method-sqlserverstatement"></a>executeBatch 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  실행할 명령 일괄 처리를 데이터베이스로 전송합니다. 모든 명령이 성공적으로 실행되면 업데이트 횟수의 배열을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>Return Value  
 업데이트 횟수가 들어 있는 **int** 배열입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>설명  
 이 executeBatch 메서드는 java.sql.Statement 인터페이스의 executeBatch 메서드에 의해 지정됩니다.  
  
 명령을 데이터베이스로 전송한 후 이 메서드는 일괄 처리의 모든 명령을 지웁니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
