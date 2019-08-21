---
title: JDBC 드라이버 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 828f58249f525a7c694b15eb85f051d80ba2211a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025768"
---
# <a name="using-the-jdbc-driver"></a>JDBC 드라이버 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 섹션에서는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 손쉽게 연결하는 방법에 대한 빠른 시작 지침을 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하려면 먼저 로컬 컴퓨터 또는 서버에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하고 로컬 컴퓨터에 JDBC 드라이버를 설치해야 합니다.  
  
## <a name="choosing-the-right-jar-file"></a>올바른 JAR 파일 선택

Microsoft JDBC Driver에서는 기본 JRE(Java Runtime Environment) 설정에 따라 아래와 같이 다른 Jar를 사용할 수 있습니다.

SQL Server용 Microsoft JDBC Driver 7.4에서는 **mssql-jdbc-7.4.1.jre8.jar**, **mssql-jdbc-7.4.1.jre11.jar** 및 **mssql-jdbc-7.4.1.jre12.jar** 클래스 라이브러리 파일을 제공합니다.

SQL Server용 Microsoft JDBC Driver 7.2에서는 **mssql-jdbc-7.2.2.jre8.jar** 및 **mssql-jdbc-7.2.2.jre11.jar** 클래스 라이브러리 파일을 제공합니다.

SQL Server용 Microsoft JDBC Driver 7.0에서는 **mssql-jdbc-7.0.0.jre8.jar** 및 **mssql-jdbc-7.0.0.jre10.jar** 클래스 라이브러리 파일을 제공합니다.

SQL Server용 Microsoft JDBC Driver 6.4에서는 **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** 및 **mssql-jdbc-6.4.0.jre9.jar** 클래스 라이브러리 파일을 제공합니다.

SQL Server용 Microsoft JDBC Driver 6.2에서는 **mssql-jdbc-6.2.2.jre7.jar** 및 **mssql-jdbc-6.2.2.jre8.jar** 클래스 라이브러리 파일을 제공합니다.
  
SQL Server용 Microsoft JDBC Driver 6.0 및 4.2에서는 **sqljdbc41.jar** 및 **sqljdbc42.jar** 클래스 라이브러리 파일을 제공합니다.
  
SQL Server용 Microsoft JDBC Driver 4.1에서는 **sqljdbc41.jar** 클래스 라이브러리 파일을 제공합니다.

사용 가능한 기능은 사용자의 선택에 따라서도 결정됩니다. 선택할 JAR 파일에 대한 자세한 내용은 [JDBC 드라이버 시스템 요구 사항](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)을 참조하세요.  
  
## <a name="setting-the-classpath"></a>클래스 경로 설정

Microsoft JDBC Driver jar는 Java SDK의 일부가 아니며 사용자 애플리케이션의 클래스 경로에 포함되어야 합니다.

JDBC Driver 4.1 또는 4.2를 사용하는 경우 해당 드라이버 다운로드의 **sqljdbc41.jar** 또는 **sqljdbc42.jar** 파일을 포함하도록 클래스 경로를 설정합니다.

JDBC Driver 6.2를 사용하는 경우 **mssql-jdbc-6.2.2.jre7.jar** 또는 **mssql-jdbc-6.2.2.jre8.jar**를 포함하도록 클래스 경로를 설정합니다.

JDBC Driver 6.4를 사용하는 경우 **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** 또는 **mssql-jdbc-6.4.0.jre9.jar**를 포함하도록 클래스 경로를 설정합니다.

JDBC Driver 7.0을 사용하는 경우 **mssql-jdbc-7.0.0.jre8.jar** 또는 **mssql-jdbc-7.0.0.jre10.jar**를 포함하도록 클래스 경로를 설정합니다.

JDBC Driver 7.2를 사용하는 경우**mssql-jdbc-7.2.2.jre8.jar** 또는 **mssql-jdbc-7.2.2.jre11.jar**를 포함하도록 클래스 경로를 설정합니다.

JDBC Driver 7.4를 사용하는 경우 **mssql-jdbc-7.4.1.jre8.jar**, **mssql-jdbc-7.4.1.jre11.jar** 또는 **mssql-jdbc-7.4.1.jre12.jar**를 포함하도록 클래스 경로를 설정합니다.

클래스 패스에 적절한 Jar 파일 항목이 없는 경우, 애플리케이션은 공통의 `Class not found`예외를 throw합니다.  

### <a name="for-microsoft-jdbc-driver-74"></a>Microsoft JDBC Driver 7.4의 경우

**mssql-jdbc-7.4.1.jre8.jar**, **mssql-jdbc-7.4.1.jre11.jar** 또는 **mssql-jdbc-7.4.1.jre12.jar** 파일이 다음 위치에 설치됩니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.4.1.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.4.1.jre11.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.4.1.jre12.jar
```

다음 코드 조각은 Windows 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.4 for SQL Server\sqljdbc_7.4\enu\mssql-jdbc-7.4.1.jre11.jar`

다음 코드 조각은 Unix/Linux 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.4/enu/mssql-jdbc-7.4.1.jre11.jar`

CLASSPATH 문에는 **mssql-jdbc-7.4.1.jre8.jar**, **mssql-jdbc-7.4.1.jre11.jar** 또는 **mssql-jdbc-7.4.1.jre12.jar**와 같은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]이(가) 하나만 포함되어 있어야 합니다.

### <a name="for-microsoft-jdbc-driver-72"></a>Microsoft JDBC Driver 7.2의 경우

**mssql-jdbc-7.2.2.jre8.jar** 또는 **mssql-jdbc-7.2.2.jre11.jar** 파일이 다음 위치에 설치됩니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.2.2.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.2.2.jre11.jar
```

다음 코드 조각은 Windows 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.2 for SQL Server\sqljdbc_7.2\enu\mssql-jdbc-7.2.2.jre11.jar`

다음 코드 조각은 Unix/Linux 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.2/enu/mssql-jdbc-7.2.2.jre11.jar`

CLASSPATH 문에는 **mssql-jdbc-7.2.2.jre8.jar** 또는 **mssql-jdbc-7.2.2.jre11.jar**와 같은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 하나만 포함되어 있어야 합니다.
  
### <a name="for-microsoft-jdbc-driver-70"></a>Microsoft JDBC Driver 7.0의 경우

**mssql-jdbc-7.0.0.jre8.jar** 또는 **mssql-jdbc-7.0.0.jre10.jar** 파일이 다음 위치에 설치됩니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.0.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.0.0.jre10.jar
```

다음 코드 조각은 Windows 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.  

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.0 for SQL Server\sqljdbc_7.0\enu\mssql-jdbc-7.0.0.jre10.jar`  
  
다음 코드 조각은 Unix/Linux 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.0/enu/mssql-jdbc-7.0.0.jre10.jar`  
  
CLASSPATH 문에는 **mssql-jdbc-7.0.0.jre8.jar** 또는 **mssql-jdbc-7.0.0.jre10.jar**와 같은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 하나만 포함되어 있어야 합니다.

### <a name="for-microsoft-jdbc-driver-64"></a>Microsoft JDBC Driver 6.4의 경우

**mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar 또는 **mssql-jdbc-6.4.0.jre9.jar** 파일이 다음 위치에 설치됩니다.  

```bash  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre7.jar
  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre9.jar
```

다음 코드 조각은 Windows 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
다음 코드 조각은 Unix/Linux 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
CLASSPATH 문에는 **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar 또는 **mssql-jdbc-6.4.0.jre9.jar**와 같은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 하나만 포함되어 있어야 합니다.

### <a name="for-microsoft-jdbc-driver-62"></a>Microsoft JDBC Driver 6.2의 경우

**mssql-jdbc-6.2.2.jre7.jar** 또는 **mssql-jdbc-6.2.2.jre8.jar** 파일이 다음 위치에 설치됩니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.2.2.jre7.jar
  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.2.2.jre8.jar
```

다음 코드 조각은 Windows 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.2.jre8.jar`  
  
다음 코드 조각은 Unix/Linux 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.2.jre8.jar`  
  
CLASSPATH 문에는 mssql-jdbc-6.2.2.jre7.jar 또는 mssql-jdbc-6.2.2.jre8.jar와 같은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 하나만 포함되어 있어야 합니다.  

### <a name="for-microsoft-jdbc-driver-41-42-and-60"></a>Microsoft JDBC Driver 4.1, 4.2 및 6.0의 경우

sqljdbc.jar 파일, sqljdbc4.jar 파일, sqljdbc41.jar 또는 sqljdbc42.jar 파일은 다음 위치에 설치됩니다.  

```bash
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc4.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc41.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc42.jar  
```

다음 코드 조각은 Windows 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
다음 코드 조각은 Unix/Linux 애플리케이션에 사용되는 CLASSPATH 문의 예제입니다.  

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
CLASSPATH 문에는 sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar 또는 sqljdbc42.jar와 같은 하나의 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]만 포함되도록 합니다.  
  
> [!NOTE]  
> Windows 시스템의 경우 디렉터리 이름이 8.3 파일 이름 규칙보다 길거나 폴더 이름에 공백이 있으면 클래스 경로에 문제가 발생할 수 있습니다. 이러한 유형의 문제가 있는 것으로 의심되면 sqljdbc.jar 파일, sqljdbc4.jar 파일 또는 sqljdbc41.jar 파일을 `C:\Temp` 같은 단순한 이름의 디렉터리로 일시적으로 이동하고 클래스 경로를 변경한 다음, 문제가 해결되는지 확인합니다.  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>명령 프롬프트에서 바로 실행되는 애플리케이션

클래스 경로는 운영 체제에 구성되어 있습니다. sqljdbc.jar, sqljdbc4.jar 또는 sqljdbc41.jar을 시스템의 클래스 경로에 추가합니다. 애플리케이션을 실행하는 Java 명령줄에서 `java -classpath` 옵션을 사용하여 클래스 경로를 지정할 수도 있습니다.  
  
### <a name="applications-that-run-in-an-ide"></a>IDE에서 실행되는 애플리케이션  

IDE 공급업체마다 자체 IDE에 클래스 경로를 설정하기 위한 서로 다른 메서드를 제공합니다. 운영 체제에서 클래스 경로를 설정하는 것만으로는 올바르게 작동하지 않습니다. sqljdbc.jar, sqljdbc4.jar 또는 sqljdbc41.jar을 IDE 클래스 경로에 추가해야 합니다.  
  
### <a name="servlets-and-jsps"></a>Servlet 및 JSP  

Servlet과 JSP는 Tomcat 같은 servlet/JSP 엔진에서 실행됩니다. 클래스 경로는 servlet/JSP 엔진 설명서에 따라 설정해야 합니다. 운영 체제에서 클래스 경로를 설정하는 것만으로는 올바르게 작동하지 않습니다. 일부 servlet/JSP 엔진은 설치 화면을 통해 엔진의 클래스 경로를 설정할 수 있습니다. 이 경우 올바른 JDBC 드라이버 JAR 파일을 기존 엔진 클래스 경로에 추가하고 엔진을 다시 시작해야 합니다. 경우에 따라 엔진을 설치하는 동안 sqljdbc.jar, sqljdbc4.jar 또는 sqljdbc41.jar 파일을 lib 같은 특정 디렉터리에 복사하여 드라이버를 배포할 수 있습니다. 엔진 드라이버의 클래스 경로는 엔진 지정 구성 파일에 지정할 수도 있습니다.  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Beans  

EJB(Enterprise Java Bean)는 EJB 컨테이너에서 실행됩니다. EJB 컨테이너는 다양한 공급업체에서 제공합니다. Java 애플릿은 브라우저에서 실행되지만 웹 서버에서 다운로드합니다. sqljdbc.jar, sqljdbc4.jar 또는 sqljdbc41.jar을 웹 서버 루트에 복사하고 `<applet ... archive=mssql-jdbc-***.jar>` 같이 애플릿의 HTML 보관 탭에 JAR 파일의 이름을 지정합니다.  
  
## <a name="making-a-simple-connection-to-a-database"></a>데이터베이스에 대해 단순한 연결 만들기

애플리케이션은 sqljdbc.jar 클래스 라이브러리를 사용하여 먼저 다음과 같이 드라이버를 등록해야 합니다.  
  
`Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  

드라이버가 로드되면 다음과 같이 연결 URL 및 DriverManager 클래스의 getConnection 메서드를 사용하여 연결을 설정할 수 있습니다.

```java
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```

JDBC API 4.0부터는 JDBC Driver를 자동으로 로드할 수 있도록 `DriverManager.getConnection()` 메서드가 개선되었습니다. 따라서 애플리케이션은 드라이버 jar 클래스 라이브러리를 사용할 때 드라이버를 등록하거나 로드하기 위해 `Class.forName` 메서드를 호출할 필요가 없습니다.  
  
DriverManager 클래스의 getConnection 메서드가 호출되면 등록된 JDBC 드라이버 집합에서 적합한 드라이버가 검색됩니다. sqljdbc4.jar, sqljdbc41.jar 또는 sqljdbc42.jar 파일에는 "META-INF/services/java.sql.Driver" 파일이 포함되어 있으며, 이 파일에는 **com.microsoft.sqlserver.jdbc.SQLServerDriver**가 등록된 드라이버로 포함되어 있습니다. 현재 Class.forName 메서드를 사용하여 드라이버를 로드하는 기존 애플리케이션은 수정하지 않아도 계속 작동합니다.  
  
> [!NOTE]  
> sqljdbc4.jar, sqljdbc41.jar 또는 sqljdbc42.jar 클래스 라이브러리를 이전 버전의 JRE(Java Runtime Environment)와 함께 사용할 수는 없습니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서 지원되는 JRE 버전 목록은 [JDBC 드라이버 시스템 요구 사항](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)을 참조하세요.  

데이터 원본에 연결하는 방법 및 연결 URL을 사용하는 방법에 대한 자세한 내용은 [연결 URL 작성](../../connect/jdbc/building-the-connection-url.md) 및 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  

[JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
