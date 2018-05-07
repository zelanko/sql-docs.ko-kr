---
title: JDBC 드라이버를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03ea3e895fb7d70b392e0c25372536770308049d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-jdbc-driver"></a>JDBC 드라이버 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 섹션에서는 간단한 연결 하는 방법에 대해 간략하게 설명 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 사용 하 여 데이터베이스의 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]합니다. 에 연결 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로컬 컴퓨터 또는 서버를 먼저 설치 해야 하 고 로컬 컴퓨터에 JDBC 드라이버를 설치 해야 합니다.  
  
## <a name="choosing-the-right-jar-file"></a>올바른 JAR 파일 선택  
 SQL Server 용 Microsoft JDBC 드라이버 6.4 제공 **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar**, 및 **mssql-jdbc-6.4.0.jre9.jar** 클래스 라이브러리 기본 Java Runtime Environment (JRE) 설정에 따라 사용할 파일입니다.  
 
 SQL Server 용 Microsoft JDBC 드라이버 6.2 제공 **mssql-jdbc-6.2.1.jre7.jar**, 및 **mssql-jdbc-6.2.1.jre8.jar** 클래스 라이브러리 파일을 기본 Java 런타임 프로그램에 따라 사용 JRE (environment) 설정 합니다.  
  
  Microsoft JDBC Driver 6.0 및 4.2 for SQL Server 제공 **sqljdbc41.jar**, 및 **sqljdbc42.jar** 클래스 라이브러리 파일을 기본 Java Runtime Environment (JRE) 설정에 따라 사용할 수 있습니다.  
  
 SQL Server 용 Microsoft JDBC Driver 4.1 제공는 **sqljdbc41.jar** 클래스 라이브러리 파일을 기본 Java Runtime Environment (JRE) 설정에 따라 사용할 수 있습니다.  
    
 사용 가능한 기능은 사용자의 선택에 따라서도 결정됩니다. JAR 파일 선택에 대 한 자세한 내용은 참조 하십시오. [JDBC 드라이버에 대 한 시스템 요구 사항](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)합니다.  
  
## <a name="setting-the-classpath"></a>클래스 경로 설정  
 JDBC 드라이버는 Java SDK에 포함되어 있지 않습니다. 포함 하도록 클래스 경로 설정 해야 사용 하려는 경우는 **sqljdbc.jar** 파일인 **sqljdbc4.jar** 파일인은 **sqljdbc41.jar** 파일 또는  **sqljdbc42.jar** 파일입니다. JDBC 드라이버 6.2를 사용 하 여 포함 하도록 클래스 경로 설정 하는 경우는 **mssql-jdbc-6.2.1.jre7.jar** 또는 **mssql-jdbc-6.2.1.jre8.jar**합니다. JDBC 드라이버 6.4를 사용 하 여 포함 하도록 클래스 경로 설정 하는 경우는 **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** 또는 **mssql-jdbc-6.4.0.jre9.jar**합니다. 클래스 경로에 항목이 없으면 응용 프로그램에서 일반적인 "클래스를 찾을 수 없습니다." 예외가 throw됩니다.  
  
### <a name="for-microsoft-jdbc-driver-64"></a>Microsoft JDBC Driver 6.4에 대 한
 **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** 또는 **mssql-jdbc-6.4.0.jre9.jar** 파일이 다음 위치에 설치 됩니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \mssql-jdbc-6.4.0.jre7.jar 
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \mssql-jdbc-6.4.0.jre8.jar
 
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \mssql-jdbc-6.4.0.jre9.jar
  
 다음은 Windows 응용 프로그램에 사용되는 CLASSPATH 문의 예입니다.  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
 다음은 Unix/Linux 응용 프로그램에 사용되는 CLASSPATH 문의 예입니다.  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
 CLASSPATH 문에 하나만 포함 되어 있는지 확인 해야 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]mssql-jdbc-6.4.0.jre7.jar, mssql-jdbc-6.4.0.jre8.jar 또는 mssql-jdbc-6.4.0.jre9.jar 등입니다.   

### <a name="for-microsoft-jdbc-driver-62"></a>Microsoft JDBC 드라이버 6.2
 **mssql-jdbc-6.2.1.jre7.jar** 또는 **mssql-jdbc-6.2.1.jre8.jar** 파일이 다음 위치에 설치 됩니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \mssql-jdbc-6.2.1.jre7.jar 
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \mssql-jdbc-6.2.1.jre8.jar
  
 다음은 Windows 응용 프로그램에 사용되는 CLASSPATH 문의 예입니다.  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.1.jre8.jar`  
  
 다음은 Unix/Linux 응용 프로그램에 사용되는 CLASSPATH 문의 예입니다.  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.1.jre8.jar`  
  
 CLASSPATH 문에 하나만 포함 되어 있는지 확인 해야 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], 예: mssql-jdbc-6.2.1.jre7.jar 또는 mssql-jdbc-6.2.1.jre8.jar 중 하나입니다.  

### <a name="for-microsoft-jdbc-driver-41-42-and-60"></a>Microsoft JDBC Driver 4.1, 4.2 및 6.0에 대 한
 sqljdbc.jar 파일, sqljdbc4.jar 파일, sqljdbc41.jar 또는 sqljdbc42.jar 파일은 다음 위치에 설치됩니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \sqljdbc.jar  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \sqljdbc4.jar  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \sqljdbc41.jar  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \sqljdbc42.jar  
  
 다음은 Windows 응용 프로그램에 사용되는 CLASSPATH 문의 예입니다.  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
 다음은 Unix/Linux 응용 프로그램에 사용되는 CLASSPATH 문의 예입니다.  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
 CLASSPATH 문에 하나만 포함 되어 있는지 확인 해야 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar 또는 sqljdbc42.jar 등입니다.  
  
> [!NOTE]  
>  Windows 시스템의 경우 디렉터리 이름이 8.3 파일 이름 규칙보다 길거나 폴더 이름에 공백이 있으면 클래스 경로에 문제가 발생할 수 있습니다. 이러한 유형의 문제를 의심 되는 경우 일시적으로 이동 해야 sqljdbc.jar 파일, sqljdbc4.jar 파일 또는 sqljdbc41.jar 파일 이름의 단순한 디렉터리로 같은 `C:\Temp`고 클래스 경로 변경 하 고 문제가 해결 되는지 확인 합니다.  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>명령 프롬프트에서 바로 실행되는 응용 프로그램  
 클래스 경로는 운영 체제에 구성되어 있습니다. sqljdbc.jar, sqljdbc4.jar 또는 sqljdbc41.jar을 시스템의 클래스 경로에 추가합니다. 또는 사용 하 여 응용 프로그램을 실행 하는 Java 명령줄에서 클래스 경로 지정할 수 있습니다는 `java -classpath` 옵션입니다.  
  
### <a name="applications-that-run-in-an-ide"></a>IDE에서 실행되는 응용 프로그램  
 IDE 공급업체마다 자체 IDE에 클래스 경로를 설정하기 위한 서로 다른 메서드를 제공합니다. 운영 체제에서 클래스 경로를 설정하는 것만으로는 올바르게 작동하지 않습니다. sqljdbc.jar, sqljdbc4.jar 또는 sqljdbc41.jar을 IDE 클래스 경로에 추가해야 합니다.  
  
### <a name="servlets-and-jsps"></a>Servlet 및 JSP  
 Servlet과 JSP는 Tomcat 같은 servlet/JSP 엔진에서 실행됩니다. 클래스 경로는 servlet/JSP 엔진 설명서에 따라 설정해야 합니다. 운영 체제에서 클래스 경로를 설정하는 것만으로는 올바르게 작동하지 않습니다. 일부 servlet/JSP 엔진은 설치 화면을 통해 엔진의 클래스 경로를 설정할 수 있습니다. 이 경우 올바른 JDBC 드라이버 JAR 파일을 기존 엔진 클래스 경로에 추가하고 엔진을 다시 시작해야 합니다. 경우에 따라 엔진을 설치하는 동안 sqljdbc.jar, sqljdbc4.jar 또는 sqljdbc41.jar 파일을 lib 같은 특정 디렉터리에 복사하여 드라이버를 배포할 수 있습니다. 엔진 드라이버의 클래스 경로는 엔진의 특정 구성 파일에 지정할 수도 있습니다.  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Beans  
 EJB(Enterprise Java Bean)는 EJB 컨테이너에서 실행됩니다. EJB 컨테이너는 다양한 공급업체에서 제공합니다. Java 애플릿은 브라우저에서 실행되지만 웹 서버에서 다운로드합니다. Sqljdbc.jar, sqljdbc4.jar 또는 sqljdbc41.jar을 웹 서버 루트에 복사 하 고 예를 들어 애플릿의 HTML 보관 탭에 JAR 파일의 이름을 지정 `<applet ... archive=sqljdbc.jar>`합니다.  
  
## <a name="making-a-simple-connection-to-a-database"></a>데이터베이스에 대해 단순한 연결 만들기  
 응용 프로그램은 sqljdbc.jar 클래스 라이브러리를 사용하여 먼저 다음과 같이 드라이버를 등록해야 합니다.  
  
 `Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  
  
 드라이버 로드 될 때 연결 URL 및 DriverManager 클래스의 getConnection 메서드를 사용 하 여 연결을 설정할 수 있습니다.  
  
```  
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 JDBC API 4.0에서는 JDBC 드라이버를 자동으로 로드 DriverManager.getConnection 메서드가 개선 되었습니다. 따라서 응용 프로그램을 등록 하거나 sqljdbc4.jar, sqljdbc41.jar 또는 sqljdbc42.jar 클래스 라이브러리를 사용 하는 경우 드라이버를 로드할 Class.forName 메서드를 호출할 필요가 없습니다.  
  
 DriverManager 클래스의 getConnection 메서드를 호출할 때 해당 드라이버를 등록 된 JDBC 드라이버 집합에서. sqljdbc4.jar, sqljdbc41.jar 또는 sqljdbc42.jar 파일에 포함 된 "META-INF/services/java.sql.Driver" 파일을 포함 되어는 **com.microsoft.sqlserver.jdbc.SQLServerDriver** 가 등록 된 드라이버로 합니다. 현재 Class.forName 메서드를 사용 하 여 드라이버를 로드, 하는 기존 응용 프로그램을 수정 하지 않고 계속 됩니다.  
  
> [!NOTE]  
>  sqljdbc4.jar, sqljdbc41.jar 또는 sqljdbc42.jar 클래스 라이브러리를 이전 버전의 JRE(Java Runtime Environment)와 함께 사용할 수는 없습니다. 참조 [JDBC 드라이버에 대 한 시스템 요구 사항](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) 에서 지 원하는 JRE 버전 목록은 여 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]합니다.  
  
 데이터 원본 연결 및 연결 URL을 사용 하는 방법에 대 한 자세한 내용은 참조 [연결 URL 작성](../../connect/jdbc/building-the-connection-url.md) 및 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
