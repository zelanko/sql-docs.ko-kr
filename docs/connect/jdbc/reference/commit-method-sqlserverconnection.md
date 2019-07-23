---
title: commit 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7561a77d91ca7de4aafd9a5d7aab2c9a4b312124
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955561"
---
# <a name="commit-method-sqlserverconnection"></a>commit 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이전의 커밋 또는 롤백 후에 변경된 모든 내용을 영구적으로 만들고, 이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에서 현재 보유 중인 데이터베이스 잠금을 해제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 commit 메서드는 java.sql.Connection 인터페이스의 commit 메서드에 의해 지정됩니다.  
  
 이 메서드는 자동 커밋 모드가 해제된 경우에만 사용해야 합니다.  
  
 클라이언트에서 수동 트랜잭션을 시작한 다음 어떤 이유로 SQL Server에서 수동 트랜잭션을 롤백할 경우에는 이 메서드가 실패하고 예외가 발생합니다. 예를 들어 클라이언트에서 ROLLBACK TRANSACTION을 명시적으로 호출하는 저장 프로시저를 호출한 다음, commit 메서드를 호출하면 예외가 발생합니다. 또한 SQL Server에서 심각도가 16 이상으로 매우 높은 오류를 발생시켜 클라이언트에서 시작한 수동 트랜잭션을 롤백할 경우 이후에 commit 메서드를 호출하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
