---
title: rollback 메서드 (sql-dmo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.rollback (java.sql.Savepoint)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d5dbd9ef-194f-4130-bfcc-7901a4fa8ded
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4aad09c11a3003a286e27ecd144cefc22e4bb9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975737"
---
# <a name="rollback-method-javasqlsavepoint"></a>rollback 메서드(java.sql.Savepoint)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 개체가 설정된 후의 모든 변경 내용을 취소합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void rollback(java.sql.Savepoint s)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *s*  
  
 롤백할 저장점 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 rollBack 메서드는 java. .sql. 연결 인터페이스에서 rollBack 메서드로 지정 됩니다.  
  
 이 메서드는 자동 커밋 모드가 해제된 경우에만 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [rollback 메서드 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
