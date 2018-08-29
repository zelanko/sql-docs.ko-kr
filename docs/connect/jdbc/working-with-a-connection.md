---
title: 연결 사용 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5878e83f9b23f273da46f356b05f8ce6563712e
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785628"
---
# <a name="working-with-a-connection"></a>연결 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

다음 섹션에서는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]의 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 다양한 방법의 예를 보여 줍니다.

> [!NOTE]  
> JDBC 드라이버를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하는 데 문제가 있으면 [연결 문제 해결](../../connect/jdbc/troubleshooting-connectivity.md)에서 문제 해결을 위한 제안 사항을 참조하세요.

## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>DriverManager 클래스를 사용한 연결

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 가장 간단한 방식은 다음과 같이 JDBC 드라이버를 로드하고 DriverManager 클래스의 getConnection 메서드를 호출하는 것입니다.

```java
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```

이 기법에서는 드라이버 목록에 있는 사용 가능한 드라이버 중 주어진 URL로 연결할 수 있는 첫 번째 드라이버를 사용하여 데이터베이스에 연결합니다.

> [!NOTE]  
> sqljdbc4.jar 클래스 라이브러리를 사용할 때 응용 프로그램은 Class.forName 메서드를 사용하여 드라이버를 명시적으로 등록 또는 로드할 필요가 없습니다. DriverManager 클래스의 getConnection 메서드를 호출 되 면 해당 드라이버를 등록 된 JDBC 드라이버 집합에서. 자세한 내용은 JDBC 드라이버 사용을 참조하십시오.

## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>SQLServerDriver 클래스를 사용한 연결 만들기

DriverManager에 대해 드라이버 목록에서 특정 드라이버를 지정하려면 다음과 같이 [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) 클래스의 [connect](../../connect/jdbc/reference/connect-method-sqlserverdriver.md) 메서드를 사용하여 데이터베이스에 연결합니다.

```java
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```

## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>SQLServerDataSource 클래스를 사용한 연결

[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스를 사용하여 연결하려면 다음과 같이 [getConnection](../../connect/jdbc/reference/getconnection-method.md) 메서드를 호출하기 전에 클래스의 다양한 setter 메서드를 사용합니다.

```java
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

```java
String url = "jdbc:sqlserver://MyServer;integratedSecurity=true;"
```

서버의 특정 포트에 연결하려면 다음을 사용합니다.

```java
String url = "jdbc:sqlserver://MyServer:1533;integratedSecurity=true;"
```

서버의 명명된 인스턴스에 연결하려면 다음을 사용합니다.

```java
String url = "jdbc:sqlserver://209.196.43.19;instanceName=INSTANCE1;integratedSecurity=true;"
```

서버의 특정 데이터베이스에 연결하려면 다음을 사용합니다.

```java
String url = "jdbc:sqlserver://172.31.255.255;database=AdventureWorks;integratedSecurity=true;"
```

더 많은 연결 URL 예를 참조 하세요 [연결 URL 작성](../../connect/jdbc/building-the-connection-url.md)합니다.

## <a name="creating-a-connection-with-a-custom-login-time-out"></a>사용자 지정 로그인 제한 시간이 있는 연결

서버 부하나 네트워크 트래픽을 조절해야 하는 경우 다음과 같이 초 단위의 세부적인 로그인 제한 시간이 있는 연결을 설정할 수 있습니다.

```java
String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"
```

## <a name="create-a-connection-with-application-level-identity"></a>응용 프로그램 수준 ID가 있는 연결

로깅 및 프로파일링을 사용해야 하는 경우 다음과 같이 연결을 특정 응용 프로그램에서 시작된 것으로 식별해야 합니다.

```java
String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"
```

## <a name="closing-a-connection"></a>연결 닫기

다음과 같이 SQLServerConnection 클래스의 [close](../../connect/jdbc/reference/close-method-sqlserverconnection.md) 메서드를 호출하여 데이터베이스 연결을 명시적으로 닫을 수 있습니다.

```java
con.close();
```

이렇게 하면 SQLServerConnection 개체가 사용하고 있는 데이터베이스 리소스가 해제되거나 연결이 풀링 시나리오의 연결 풀에 반환됩니다.

> [!NOTE]  
> 또한 close 메서드를 호출하면 보류 중인 모든 트랜잭션이 롤백됩니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
