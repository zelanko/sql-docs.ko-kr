---
title: setAutoCommit 메서드 (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 971b23d6ab738f87ca89ef48a0d8c6f6c50fffac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32842688"
---
# <a name="setautocommit-method-sqlserverconnection"></a>setAutoCommit 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 대 한 자동 커밋 모드를 설정 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체 지정 된 상태입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *value*  
  
 **true 이면** 자동 커밋 모드에 대 한 연결을 사용할 수 있도록 **false** 사용 하지 않도록 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setAutoCommit 메서드는 java.sql.Connection 인터페이스의 setAutoCommit 메서드에 의해 지정 됩니다.  
  
 연결이 자동 커밋 모드이면 해당 연결의 모든 SQL 문이 개별 트랜잭션으로 실행되고 커밋됩니다. SQL 문은에 대 한 호출으로 종료 되 트랜잭션으로 그룹화 되어 그렇지 않은 경우는 [커밋](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) 메서드 또는 [롤백](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md) 메서드. 기본적으로 새 연결은 자동 커밋 모드로 설정됩니다.  
  
 어느 쪽이 먼저이든 관계없이 문이 완료되거나 다음 실행이 수행되면 커밋이 수행됩니다. 반환 하는 문의 경우는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 결과 집합이 닫힌 경우 또는 결과 집합의 마지막 행을 검색 할 때 문이 완료 합니다. 고급 수준에서는 단일 문으로 출력 매개 변수 값뿐 아니라 여러 결과도 반환할 수 있습니다. 이러한 경우 결과와 출력 매개 변수 값이 모두 검색된 후에 커밋이 수행됩니다.  
  
 자동 커밋 모드가 인 경우 **false**, JDBC 드라이버는 각 커밋 후 새 트랜잭션을 암시적으로 시작 됩니다.  
  
> [!NOTE]  
>  트랜잭션 도중에 이 메서드를 호출해도 트랜잭션이 커밋됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
