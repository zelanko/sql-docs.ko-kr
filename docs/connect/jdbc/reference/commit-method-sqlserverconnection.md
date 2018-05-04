---
title: commit 메서드 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42cd2c1d8a189e353d4bfd6bbd2f67b3c14e0df1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="commit-method-sqlserverconnection"></a>commit 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이전의 커밋 또는 롤백 후 내용을 영구적으로 적용 된 모든 변경 내용을 적용 하 고이 현재 보유 하 고 있는 데이터베이스 잠금을 해제 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 커밋 메서드는 java.sql.Connection 인터페이스의 커밋 메서드에 의해 지정 됩니다.  
  
 이 메서드는 자동 커밋 모드가 해제된 경우에만 사용해야 합니다.  
  
 클라이언트에서 수동 트랜잭션을 시작한 다음 어떤 이유로 SQL Server에서 수동 트랜잭션을 롤백할 경우에는 이 메서드가 실패하고 예외가 발생합니다. 예를 들어 클라이언트 ROLLBACK TRANSACTION을 명시적으로 호출 하는 저장된 프로시저를 호출 하는 경우 예외가 throw 됩니다 및 클라이언트 commit 메서드를 호출 합니다. 또한 SQL Server 롤백할 수 충분 한 심각도 16 이상인 오류가 발생 하는 경우 클라이언트에서 시작한 수동 트랜잭션을; commit 메서드를 한 후속 호출에는 예외가 throw 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
