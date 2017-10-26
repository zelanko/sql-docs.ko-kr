---
title: "연결 풀링을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 699d4e8a-34bf-4c60-b0d5-4a10dad6084a
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 47a65bf1c9ce6afdedd1f68c0431912af4aea402
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-connection-pooling"></a>연결 풀링 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 지원 Java platform, Enterprise Edition (Java EE) 연결 풀링을 합니다. 미들웨어 공급업체가 제공하며 JDBC 3.0과 호환되는 모든 연결 풀링 구현에 참여할 수 있도록 JDBC 드라이버는 JDBC 3.0 필수 인터페이스를 구현합니다. Java EE 응용 프로그램 서버와 같은 미들웨어는 대개 호환되는 연결 풀링 기능을 제공합니다. JDBC 드라이버는 이러한 환경에서 풀링된 연결에 참여합니다.  
  
> [!NOTE]  
>  JDBC 드라이버는 Java EE 연결 풀링을 지원하지만 자체 풀링 구현을 제공하지는 않습니다. 대신 JDBC 드라이버는 타사 Java 응용 프로그램 서버를 통해 연결을 관리합니다.  
  
## <a name="remarks"></a>주의  
 연결 풀링을 구현하는 데 필요한 클래스는 다음과 같습니다.  
  
|클래스|구현|Description|  
|-----------|----------------|-----------------|  
|com.microsoft.sqlserver.jdbc 합니다. SQLServerXADataSource|javax.sql.ConnectionPoolDataSource and javax.sql.XADataSource|사용 하는 것이 좋습니다는 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 모든 JDBC 3.0 풀링과 XA 인터페이스를 구현 하므로 Java EE 서버에 대 한 클래스 필요 합니다.|  
|com.microsoft.sqlserver.jdbc 합니다. SQLServerConnectionPoolDataSource|javax.sql.ConnectionPoolDataSource|이 클래스는 Java EE 응용 프로그램 서버에서 해당 연결 풀을 실제 연결로 채울 수 있도록 하는 연결 팩터리입니다. Java EE 공급 업체의 구성에 javax.sql.ConnectionPoolDataSource를 구현 하는 클래스를 필요한 경우 클래스 이름으로 지정 [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)합니다. 일반적으로 사용 하는 권장는 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 클래스 대신 및 XA 인터페이스를 모두 풀링을 구현 하 고 더 많은 Java EE 서버 구성에서 검증 되었으므로 합니다.|  
  
 JDBC 응용 프로그램 코드에서 풀링의 이점을 극대화하려면 항상 연결을 명시적으로 닫아야 합니다. 응용 프로그램에서 연결을 명시적으로 닫으면 풀링 구현은 연결을 바로 다시 사용할 수 있습니다. 연결을 닫지 않으면 다른 응용 프로그램에서 이를 다시 사용할 수 없습니다. 응용 프로그램이 사용할 수는 `finally` 구문을 예외가 발생 하더라도 풀링된 연결이 닫혀 있는지 확인 합니다.  
  
> [!NOTE]  
>  JDBC 드라이버는 현재 연결을 풀에 반환할 때 sp_reset_connection 저장 프로시저를 호출하지 않습니다. 대신 JDBC 드라이버는 타사 Java 응용 프로그램 서버를 통해 연결을 원래 상태로 되돌립니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

