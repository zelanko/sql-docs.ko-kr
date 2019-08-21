---
title: 드라이버 작업 추적 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 723aeae7-6504-4585-ba8b-3525115bea8b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18bfd63a8cf3255a62b6aef5c4c31573c60e76b0
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027590"
---
# <a name="tracing-driver-operation"></a>드라이버 작업 추적
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 추적 또는 로깅 기능을 사용하여 애플리케이션에서 사용되는 JDBC 드라이버 관련 문제를 해결할 수 있습니다. 추적 기능을 활성화하기 위해 JDBC 드라이버는 java.util.logging의 로깅 API를 사용합니다. 이 API는 Logger 및 LogRecord 개체를 만드는 클래스 집합을 제공합니다.  
  
> [!NOTE]  
>  JDBC 드라이버에 포함된 네이티브 구성 요소(sqljdbc_xa.dll)의 경우 BID(Built-In Diagnostics) 프레임워크를 사용하여 추적 기능을 활성화합니다. BID에 대한 자세한 내용은 [SQL Server에서 데이터 액세스 추적](https://go.microsoft.com/fwlink/?LinkId=70042)을 참조하세요.  
  
 애플리케이션을 개발할 때 Logger 개체를 호출한 다음, LogRecord 개체를 만들고 Handler 개체에 전달하여 처리할 수 있습니다. 로 거 및 처리기 개체는 모두 로깅 수준을 사용 하 고 선택적으로 로깅 필터를 사용 하 여 처리 되는 LogRecords를 제어 합니다. 로깅 작업이 완료되면 Handler 개체는 필요에 따라 Formatter 개체를 사용하여 로그 정보를 게시합니다.  
  
 기본적으로 java.util.logging 프레임워크는 출력을 파일에 작성합니다. 이 출력 로그 파일은 JDBC 드라이버가 실행 중인 컨텍스트에 대한 쓰기 권한이 있어야 합니다.  
  
> [!NOTE]  
>  프로그램 추적에 여러 로깅 개체를 사용하는 방법에 대한 자세한 내용은 Sun Microsystems 웹 사이트의 Java Logging APIs 설명서(영문)를 참조하십시오.  
  
 다음 섹션에서는 로깅 수준 및 로깅 가능한 범주를 설명하고 애플리케이션에서 추적 기능을 활성화하는 방법에 대한 정보를 제공합니다.  
  
## <a name="logging-levels"></a>로깅 수준  
 작성되는 모든 로그 메시지에는 연관된 로깅 수준이 있습니다. 로깅 수준은 로그 메시지의 중요도를 결정하며 java.util.logging의 **Level** 클래스에 의해 정의됩니다. 한 수준에서 로깅을 설정하면 상위 수준의 로깅도 모두 설정됩니다. 이 섹션에서는 공용 로깅 범주 및 내부 로깅 범주의 로깅 수준에 대해 설명합니다. 로깅 범주에 대한 자세한 내용은 이 문서의 로깅 범주 섹션을 참조하세요.  
  
 다음 표에서는 공용 로깅 범주에 대해 사용할 수 있는 각 로깅 수준에 대해 설명합니다.  
  
|속성|설명|  
|----------|-----------------|  
|SEVERE|심각한 오류를 나타내는 가장 높은 로깅 수준입니다. JDBC 드라이버에서 이 수준은 오류 및 예외를 보고하는 데 사용합니다.|  
|WARNING|잠재적인 문제를 의미합니다.|  
|INFO|정보 메시지를 제공합니다.|  
|CONFIG|구성 메시지를 제공합니다. JDBC 드라이버는 현재 구성 메시지를 제공하지 않습니다.|  
|FINE|공용 메서드에서 발생한 모든 예외를 포함하는 기본 추적 정보를 제공합니다.|  
|FINER|모든 공용 메서드 진입점 및 진출점과 관련 매개 변수 데이터 형식 및 공용 클래스의 모든 공용 속성을 포함하는 자세한 추적 정보를 제공합니다. 또한 입력 매개 변수, 출력 매개 변수 및 CLOB, BLOB, NCLOB, Reader, \<stream> 반환 값 형식을 제외한 메서드 반환 값을 제공합니다.|  
|FINEST|매우 자세한 추적 정보를 제공합니다. 이 수준은 가장 낮은 로깅 수준입니다.|  
|OFF|로깅을 해제합니다.|  
|ALL|모든 메시지의 로깅을 활성화합니다.|  
  
 다음 표에서는 내부 로깅 범주에 대해 사용할 수 있는 각 로깅 수준에 대해 설명합니다.  
  
|속성|설명|  
|----------|-----------------|  
|SEVERE|심각한 오류를 나타내는 가장 높은 로깅 수준입니다. JDBC 드라이버에서 이 수준은 오류 및 예외를 보고하는 데 사용합니다.|  
|WARNING|잠재적인 문제를 의미합니다.|  
|INFO|정보 메시지를 제공합니다.|  
|FINE|기본 개체 생성 및 소멸을 포함한 추적 정보를 제공합니다. 또한 공용 메서드에서 발생한 모든 예외에 대한 정보도 제공합니다.|  
|FINER|모든 공용 메서드 진입점 및 진출점과 관련 매개 변수 데이터 형식 및 공용 클래스의 모든 공용 속성을 포함하는 자세한 추적 정보를 제공합니다. 또한 입력 매개 변수, 출력 매개 변수 및 CLOB, BLOB, NCLOB, Reader, \<stream> 반환 값 형식을 제외한 메서드 반환 값을 제공합니다.<br /><br /> JDBC 드라이버 버전 1.2에 포함된 로깅 범주 중 로깅 수준이 FINE인 범주는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md), [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), XA 및 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)입니다. 이 범주들은 버전 2.0 릴리스에서부터 FINER 수준으로 업그레이드되었습니다.|  
|FINEST|매우 자세한 추적 정보를 제공합니다. 이 수준은 가장 낮은 로깅 수준입니다.<br /><br /> JDBC 드라이버 버전 1.2에 포함된 로깅 범주 중 로깅 수준이 FINEST인 범주는 TDS.DATA 및 TDS.TOKEN입니다. 버전 2.0 릴리스에서부터 FINEST 로깅 수준이 유지됩니다.|  
|OFF|로깅을 해제합니다.|  
|ALL|모든 메시지의 로깅을 활성화합니다.|  
  
## <a name="logging-categories"></a>로깅 범주  
 Logger 개체를 만들 때 로그 정보를 가져올 명명된 엔터티나 범주가 어떤 것인지 이 개체에 알려야 합니다. JDBC 드라이버는 com.microsoft.sqlserver.jdbc 드라이버 패키지에 정의된 다음 공용 로깅 범주를 지원합니다.  
  
|속성|설명|  
|----------|-----------------|  
|연결|[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINER로 설정할 수 있습니다.|  
|인수를 제거합니다.|[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINER로 설정할 수 있습니다.|  
|DataSource|[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE으로 설정할 수 있습니다.|  
|ResultSet|[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINER로 설정할 수 있습니다.|  
|드라이버|[SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINER로 설정할 수 있습니다.|  
  
 Microsoft JDBC 드라이버 버전 2.0 이상에서는 드라이버가 다음 내부 로깅 범주에 대한 로깅 지원을 포함하는 com.microsoft.sqlserver.jdbc.internals 패키지를 제공합니다.  
  
|속성|설명|  
|----------|-----------------|  
|AuthenticationJNI|Windows 통합 인증 문제에 관한 메시지를 기록 합니다 ( **Authenticationscheme** 연결 속성이 암시적 또는 명시적으로 **NativeAuthentication**로 설정 된 경우).<br /><br /> 애플리케이션에서는 로깅 수준을 FINEST 및 FINE으로 설정할 수 있습니다.|  
|SQLServerConnection|[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE 및 FINER로 설정할 수 있습니다.|  
|SQLServerDataSource|[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) 및 [SQLServerPooledConnection](../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 클래스의 메시지를 로깅합니다.<br /><br /> 애플리케이션에서는 로깅 수준을 FINER로 설정할 수 있습니다.|  
|InputStream|java.io.InputStream, java.io.Reader 및 varchar, nvarchar, varbinary 데이터 형식 등의 최대값 지정자가 있는 데이터 형식과 관련된 메시지를 로깅합니다.<br /><br /> 애플리케이션에서는 로깅 수준을 FINER로 설정할 수 있습니다.|  
|SQLServerException|[SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE으로 설정할 수 있습니다.|  
|SQLServerResultSet|[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE, FINER 및 FINEST로 설정할 수 있습니다.|  
|SQLServerStatement|[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE, FINER 및 FINEST로 설정할 수 있습니다.|  
|XA|[SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 클래스의 모든 XA 트랜잭션에 대한 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE 및 FINER로 설정할 수 있습니다.|  
|KerbAuthentication|유형 4 Kerberos 인증에 대 한 메시지를 기록 합니다 ( **Authenticationscheme** 연결 속성이 **JavaKerberos**로 설정 된 경우). 애플리케이션에서는 로깅 수준을 FINE 또는 FINER로 설정할 수 있습니다.|  
|TDS.DATA|드라이버와 SQL 서버 간 TDS 프로토콜 수준 대화를 포함하는 메시지를 로깅합니다. 주고받는 각 TDS 패킷의 자세한 내용이 ASCII 및 16진수로 로깅됩니다. 로그인 자격 증명(사용자 이름 및 암호)은 로깅되지 않습니다. 다른 모든 데이터는 로깅됩니다.<br /><br /> 이 범주는 매우 자세한 메시지를 작성하기 때문에 로깅 수준을 FINEST로 설정해야만 사용할 수 있습니다.|  
|TDS.Channel|이 범주는 SQL 서버와의 TCP 통신 채널의 동작을 추적합니다. 로깅된 메시지는 소켓을 열고 닫는 동작과 읽고 쓰는 동작을 포함합니다. 또한 SQL 서버와의 SSL(Secure Sockets Layer) 연결 설정과 관련된 메시지를 추적합니다.<br /><br /> 이 범주는 로깅 수준을 FINE, FINER 또는 FINEST로 설정해야만 사용할 수 있습니다.|  
|TDS.Writer|이 범주는 TDS 채널에 대한 쓰기 동작을 추적합니다. 내용이 아닌, 쓰기 길이만 추적됩니다. 또한 이 범주에서는 문의 실행을 취소하기 위해 주의 신호가 서버로 전송되는 경우의 문제를 추적합니다.<br /><br /> 이 범주는 로깅 수준을 FINEST로 설정해야만 사용할 수 있습니다.|  
|TDS.Reader|FINEST 수준에서 이 범주는 TDS 채널의 특정 읽기 동작을 추적합니다. FINEST 수준에서는 추적이 자세할 수 있습니다. WARNING 및 SEVERE 수준에서 이 범주는 드라이버가 연결을 닫기 전 SQL 서버에서 잘못된 TDS 프로토콜을 수신하는 경우 추적을 수행합니다.<br /><br /> 이 범주는 로깅 수준을 FINER 또는 FINEST로 설정해야만 사용할 수 있습니다.|  
|TDS.Command|이 범주는 낮은 수준의 상태 전환 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 실행, ResultSet 커서 인출, 커밋 등 TDS 명령 실행과 관련된 기타 정보를 추적합니다.<br /><br /> 이 범주는 로깅 수준을 FINEST로 설정해야만 사용할 수 있습니다.|  
|TDS.TOKEN|이 범주는 TDS 패킷 내의 토큰만 로깅하며 TDS.DATA 범주보다 정보가 덜 자세합니다. 이 범주는 로깅 수준을 FINEST로 설정해야만 사용할 수 있습니다.<br /><br /> FINEST 수준에서 이 범주는 응답에서 처리되는 TDS 토큰을 추적합니다. SEVERE 수준에서 이 범주는 잘못된 TDS 토큰이 발견되는 경우 추적을 수행합니다.|  
|SQLServerDatabaseMetaData|[SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE으로 설정할 수 있습니다.|  
|SQLServerResultSetMetaData|[SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE으로 설정할 수 있습니다.|  
|SQLServerParameterMetaData|[SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE으로 설정할 수 있습니다.|  
|SQLServerBlob|[SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE으로 설정할 수 있습니다.|  
|SQLServerClob|[SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE으로 설정할 수 있습니다.|  
|SQLServerSQLXML|내부 SQLServerSQLXML 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE으로 설정할 수 있습니다.|  
|SQLServerDriver|[SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE으로 설정할 수 있습니다.|  
|SQLServerNClob|[SQLServerNClob](../../connect/jdbc/reference/sqlservernclob-class.md) 클래스의 메시지를 로깅합니다. 애플리케이션에서는 로깅 수준을 FINE으로 설정할 수 있습니다.|  
  
## <a name="enabling-tracing-programmatically"></a>프로그래밍 방식으로 추적 활성화  
 Logger 개체를 만들고 로깅할 범주를 지시하여 프로그래밍 방식으로 추적을 활성화할 수 있습니다. 예를 들어 다음 코드에서는 SQL 문의 로깅을 활성화하는 방법을 보여 줍니다.  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.FINER);  
```  
  
 코드에서 로깅을 해제하려면 다음을 사용합니다.  
  
```java
logger.setLevel(Level.OFF);  
```  
  
 사용 가능한 모든 범주를 로깅하려면 다음을 사용합니다,  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc");  
logger.setLevel(Level.FINE);  
```  
  
 특정 범주를 로깅하지 않으려면 다음을 사용합니다.  
  
```java
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.OFF);  
```  
  
## <a name="enabling-tracing-by-using-the-loggingproperties-file"></a>Logging.Properties 파일을 사용하여 추적 활성화  
 JRE(Java Runtime Environment) 설치의 `lib` 디렉터리에 있는 `logging.properties` 파일을 사용하여 추적을 활성화하는 방법도 있습니다. 이 파일은 추적 기능을 활성화할 때 사용할 로거 및 처리기의 기본 값을 설정하는 데 사용할 수 있습니다.  
  
 다음은 `logging.properties` 파일에서 설정할 수 있는 예입니다.  
  
```  
# Specify the handler, the handlers will be installed during VM startup.  
handlers= java.util.logging.FileHandler  
  
# Default global logging level.  
.level= OFF  
  
# default file output is in user's home directory.  
java.util.logging.FileHandler.pattern = %h/java%u.log  
java.util.logging.FileHandler.limit = 5000000  
java.util.logging.FileHandler.count = 20  
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter  
java.util.logging.FileHandler.level = FINEST  
  
# Facility specific properties.  
com.microsoft.sqlserver.jdbc.level=FINEST  
  
```  
  
> [!NOTE]  
>  java.util.logging의 일부인 LogManager 개체를 사용하여 `logging.properties` 파일의 속성을 설정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 관련 문제 진단](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
