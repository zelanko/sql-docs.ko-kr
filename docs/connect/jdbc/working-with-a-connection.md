---
title: "연결 사용 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 03921ad2e09bb1da941c3570fac0b3d9c6a1ba31
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="working-with-a-connection"></a>연결 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  다음 섹션에서는 제공에 연결 하는 다른 방법의 예는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 사용 하 여 데이터베이스는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 의 클래스는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]합니다.  
  
> [!NOTE]  
>  에 연결 하는 데 문제가 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC 드라이버를 사용 하 여 참조 [연결 문제 해결](../../connect/jdbc/troubleshooting-connectivity.md) 수정 하는 방법에 대 한 제안 합니다.  
  
## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>DriverManager 클래스를 사용한 연결  
 에 연결할 수는 가장 간단한 방식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스가 JDBC 드라이버를 로드 하의 DriverManager 클래스를 다음과 같이 getConnection 메서드를 호출 합니다.  
  
```  
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 이 기법에서는 드라이버 목록에 있는 사용 가능한 드라이버 중 주어진 URL로 연결할 수 있는 첫 번째 드라이버를 사용하여 데이터베이스에 연결합니다.  
  
> [!NOTE]  
>  Sqljdbc4.jar 클래스 라이브러리를 사용할 때 응용 프로그램을 명시적으로 등록 하거나 Class.forName 메서드를 사용 하 여 드라이버를 로드할 필요 하지 않습니다. DriverManager 클래스의 getConnection 메서드를 호출할 때 해당 드라이버를 등록 된 JDBC 드라이버 집합에서. 자세한 내용은 JDBC 드라이버 사용을 참조하십시오.  
  
## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>SQLServerDriver 클래스를 사용한 연결 만들기  
 드라이버에 대 한 드라이버 목록에서 특정 드라이버를 지정 해야 할 경우 사용 하 여 데이터베이스 연결을 만들 수 있습니다는 [연결](../../connect/jdbc/reference/connect-method-sqlserverdriver.md) 의 메서드는 [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) 다음과 같이 클래스:  
  
```  
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```  
  
## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>SQLServerDataSource 클래스를 사용한 연결  
 사용 하 여 연결을 만들어야 하는 경우는 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스를 호출 하기 전에 클래스의 다양 한 setter 메서드를 사용할 수 없다는 [getConnection](../../connect/jdbc/reference/getconnection-method.md) 메서드를 다음과 같이 합니다.  
  
```  
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setUser("MyUserName");  
ds.setPassword("*****");  
ds.setServerName("localhost");  
ds.setPortNumber(1433);   
ds.setDatabaseName("AdventureWorks");  
Connection con = ds.getConnection();  
```  
  
## <a name="creating-a-connection-that-targets-a-very-specific-data-source"></a>특정 데이터 원본을 대상으로 한 연결  
 특정 데이터 원본을 대상으로 하는 데이터베이스 연결을 설정해야 하는 경우 여러 가지 접근 방식을 사용할 수 있습니다. 각 접근 방식은 연결 URL을 사용하여 설정하는 속성에 따라 달라집니다.  
  
 원격 서버의 기본 인스턴스에 연결하려면 다음을 사용합니다.  
  
 `String url = "jdbc:sqlserver://MyServer;integratedSecurity=true;"`  
  
 서버의 특정 포트에 연결하려면 다음을 사용합니다.  
  
 `String url = "jdbc:sqlserver://MyServer:1533;integratedSecurity=true;"`  
  
 서버의 명명된 인스턴스에 연결하려면 다음을 사용합니다.  
  
 `String url = "jdbc:sqlserver://209.196.43.19;instanceName=INSTANCE1;integratedSecurity=true;"`  
  
 서버의 특정 데이터베이스에 연결하려면 다음을 사용합니다.  
  
 `String url = "jdbc:sqlserver://172.31.255.255;database=AdventureWorks;integratedSecurity=true;"`  
  
 더 많은 연결 URL 예에 대 한 참조 [연결 URL 작성](../../connect/jdbc/building-the-connection-url.md)합니다.  
  
## <a name="creating-a-connection-with-a-custom-login-time-out"></a>사용자 지정 로그인 제한 시간이 있는 연결  
 서버 부하나 네트워크 트래픽을 조절해야 하는 경우 다음과 같이 초 단위의 세부적인 로그인 제한 시간이 있는 연결을 설정할 수 있습니다.  
  
 `String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"`  
  
## <a name="create-a-connection-with-application-level-identity"></a>응용 프로그램 수준 ID가 있는 연결  
 로깅 및 프로파일링을 사용해야 하는 경우 다음과 같이 연결을 특정 응용 프로그램에서 시작된 것으로 식별해야 합니다.  
  
 `String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"`  
  
## <a name="closing-a-connection"></a>연결 닫기  
 호출 하 여 데이터베이스 연결을 명시적으로 닫을 수 있습니다는 [닫습니다](../../connect/jdbc/reference/close-method-sqlserverconnection.md) 다음과 같이 SQLServerConnection 클래스의 메서드:  
  
 `con.close();`  
  
 SQLServerConnection 개체를 사용 하 여 데이터베이스 리소스가 해제 되거나 연결이 풀링된 시나리오의 연결 풀에 반환 됩니다.  
  
> [!NOTE]  
>  Close 메서드를 호출 또한 롤백합니다 보류 중인 모든 트랜잭션이 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

