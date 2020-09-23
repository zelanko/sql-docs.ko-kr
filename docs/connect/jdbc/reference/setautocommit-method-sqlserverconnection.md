---
title: setAutoCommit 메서드(SQLServerConnection)
description: SQL Server용 JDBC Driver에서 SQLServerConnection 클래스의 setAutoCommit 메서드에 대한 공용 API를 자세히 알아봅니다.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 117fa85e5ec6bdd7d0d37de9fc057dd8127cf42a
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435370"
---
# <a name="setautocommit-method-sqlserverconnection"></a>setAutoCommit 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 자동 커밋 모드를 지정된 상태로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *value*  
  
 연결에 자동 커밋 모드를 사용하려면 **true**이고, 사용하지 않으려면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setAutoCommit 메서드는 java.sql.Connection 인터페이스의 setAutoCommit 메서드에 의해 지정됩니다.  
  
 연결이 자동 커밋 모드이면 해당 연결의 모든 SQL 문이 개별 트랜잭션으로 실행되고 커밋됩니다. 그렇지 않으면 SQL 문은 [commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) 메서드 또는 [rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md) 메서드 호출로 종료되는 트랜잭션으로 그룹화됩니다. 기본적으로 새 연결은 자동 커밋 모드로 설정됩니다.  
  
 어느 쪽이 먼저이든 관계없이 문이 완료되거나 다음 실행이 수행되면 커밋이 수행됩니다. 문이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 반환하는 경우에는 결과 집합의 마지막 행이 검색되거나 결과 집합이 닫힌 후에 문이 완료됩니다. 고급 수준에서는 단일 문으로 출력 매개 변수 값뿐 아니라 여러 결과도 반환할 수 있습니다. 이러한 경우 결과와 출력 매개 변수 값이 모두 검색된 후에 커밋이 수행됩니다.  
  
 자동 커밋 모드가 **false**이면 JDBC 드라이버에서는 각 커밋 후에 새 트랜잭션을 암시적으로 시작합니다.  
  
> [!NOTE]  
> 트랜잭션 도중에 이 메서드를 호출해도 트랜잭션이 커밋됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)  
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
