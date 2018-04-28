---
title: SQLServerXAConnection 클래스 | Microsoft Docs
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
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e095b498807412a40d4df1092b6c151c8c030c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverxaconnection-class"></a>SQLServerXAConnection 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  분산(XA) 트랜잭션에 참여할 수 있는 JDBC 연결을 나타냅니다.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **확장:** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **구현:** javax.sql.XAConnection  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>주의  
 SQLServerXAConnection 개체를 통해 분산 트랜잭션에 참여할 수 있습니다는 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체입니다. SQLServerXAResource 개체를 통해 SQLServerXAConnection 개체를 관리 하는 트랜잭션 관리자는 중간 계층 서버에서의 일부입니다.  
  
> [!NOTE]  
>  응용 프로그램 프로그래머는 일반적으로 이 인터페이스를 직접 사용하지 않습니다. 이 인터페이스는 중간 계층 서버에서 작업하는 트랜잭션 관리자가 주로 사용합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXAConnection 멤버](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
