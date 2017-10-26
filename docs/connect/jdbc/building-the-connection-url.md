---
title: "연결 URL 작성 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 44996746-d373-4f59-9863-a8a20bb8024a
caps.latest.revision: 53
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b5707221b51bff301aa5e9214497ba9090750aae
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="building-the-connection-url"></a>연결 URL 작성
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  연결 URL의 일반적인 형식은 다음과 같습니다.  
  
 `jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]]`  
  
 각 항목이 나타내는 의미는 다음과 같습니다.  
  
-   **jdbc:sqlserver: / /** (필수)는 하위 프로토콜 이라고 하며 일정.  
  
-   **serverName** (선택 사항)는 주소에 연결할 서버입니다. 이는 DNS나 IP 주소일 수도 있고 로컬 컴퓨터인 경우 localhost나 127.0.0.1일 수도 있습니다. 연결 URL에 지정하지 않은 경우 속성 컬렉션에 서버 이름을 지정해야 합니다.  
  
-   **instanceName** (옵션)은 serverName에서 연결할 인스턴스입니다. instanceName을 지정하지 않으면 기본 인스턴스에 연결됩니다.  
  
-   **portNumber** (옵션)은 serverName에서 연결할 포트입니다. 기본값은 1433입니다. 기본값을 사용하는 경우 URL에 포트나 앞에 붙는 ':'을 지정할 필요가 없습니다.  
  
    > [!NOTE]  
    >  연결 성능을 최적화하려면 명명된 인스턴스에 연결할 때 portNumber를 설정해야 합니다. 그러면 포트 번호를 확인하기 위해 서버까지 왕복 이동할 필요가 없습니다. portNumber 및 instanceName을 모두 사용하는 경우 portNumber가 우선 순위를 갖고 instanceName은 무시됩니다.  
  
-   **속성** (선택 사항)는 하나 이상의 옵션 연결 속성입니다. 자세한 내용은 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다. 목록에 있는 속성은 모두 지정할 수 있습니다. 속성은 세미콜론(';')으로만 구분할 수 있고 중복될 수 없습니다.  
  
> [!CAUTION]  
>  보안을 위해 사용자 입력을 토대로 연결 URL을 작성하지 않는 것이 좋습니다. URL에는 서버 이름과 드라이버만 지정해야 합니다. 사용자 이름 및 암호 값에는 연결 속성 컬렉션을 사용합니다. JDBC 응용 프로그램의 보안에 대 한 자세한 내용은 참조 [JDBC 드라이버 응용 프로그램 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)합니다.  
  
## <a name="connection-examples"></a>연결 예  
 사용자 이름 및 암호를 사용하여 로컬 컴퓨터에서 기본 데이터베이스에 연결합니다.  
  
 `jdbc:sqlserver://localhost;user=MyUserName;password=*****;`  
  
> [!NOTE]  
>  이전 예제에서는 연결 문자열에 사용자 이름과 암호를 사용했지만 보다 안전한 통합 보안을 사용해야 합니다. 자세한 내용은 참조는 [통합 인증으로 연결](#Connectingintegrated) 이 항목의 뒷부분에 나오는 섹션.  
  
 다음 연결 문자열에 연결 하는 방법의 예를 보여 줍니다.는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서 지 원하는 모든 운영 체제에서 실행 중인 응용 프로그램에서 통합된 인증 및 Kerberos를 사용 하 여 데이터베이스의 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]:  
  
```  
jdbc:sqlserver://;servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos  
```  
  
 통합 인증을 사용하여 로컬 컴퓨터의 기본 데이터베이스에 연결하는 경우:  
  
 `jdbc:sqlserver://localhost;integratedSecurity=true;`  
  
 원격 서버의 명명된 데이터베이스에 연결하는 경우:  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 기본 포트에서 원격 서버에 연결하는 경우:  
  
 `jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 사용자 지정 응용 프로그램 이름을 지정하여 연결하는 경우:  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;applicationName=MyApp;`  
  
## <a name="named-and-multiple-sql-server-instances"></a>명명된 다중 SQL Server 인스턴스  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]한 서버에 여러 개의 데이터베이스 인스턴스를 설치할 수 있습니다. 각 인스턴스는 특정 이름으로 식별합니다. 명명 된 인스턴스에 연결 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)](기본 설정), 명명 된 인스턴스의 포트 번호를 지정 하거나, 또는 인스턴스 이름을 JDBC URL 속성으로 지정할 수 있습니다 또는 **datasource** 속성입니다. 인스턴스 이름이나 포트 번호 속성을 지정하지 않으면 기본 인스턴스에 대한 연결이 설정됩니다. 다음 예를 참조하십시오.  
  
 포트 번호를 사용하려면 다음을 수행합니다.  
  
 `jdbc:sqlserver://localhost:1433;integratedSecurity=true;<more properties as required>;`  
  
 JDBC URL 속성을 사용하려면 다음을 수행합니다.  
  
 `jdbc:sqlserver://localhost;instanceName=instance1;integratedSecurity=true;<more properties as required>;`  
  
## <a name="escaping-values-in-the-connection-url"></a>연결 URL에서 값 이스케이프 처리  
 공백, 세미콜론, 인용 부호와 같은 특수 문자가 삽입되어 있으므로 연결 URL 값의 일부를 이스케이프 처리해야 하는 경우가 있을 수 있습니다. JDBC 드라이버는 이런 문자가 중괄호로 묶인 경우 이스케이프 처리를 지원합니다. 예를 들어 {;}는 세미콜론을 이스케이프 처리합니다.  
  
 이스케이프 처리되는 값에 특수 문자(특히 '=', ';', '[]' 및 공백)는 포함될 수 있지만 중괄호는 포함될 수 없습니다. 이스케이프 처리해야 하는 값에 중괄호가 포함된 경우 해당 값을 속성 컬렉션에 추가해야 합니다.  
  
> [!NOTE]  
>  중괄호 안의 공백은 리터럴이며 잘리지 않습니다.  
  
##  <a name="Connectingintegrated"></a>Windows 통합된 인증으로 연결  
 JDBC 드라이버는 integratedSecurity 연결 문자열 속성을 통해 Windows 운영 체제에서 형식 2 통합 인증을 사용할 수 있습니다. 통합 인증을 사용하려면 sqljdbc_auth.dll 파일을 JDBC 드라이버가 설치된 컴퓨터의 Windows 시스템 경로에 있는 디렉터리에 복사합니다.  
  
 sqljdbc_auth.dll 파일은 다음 위치에 설치되어 있습니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \auth\  
  
 지 원하는 모든 운영 체제에 대 한는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], 참조 [Kerberos 통합 인증을 사용 하려면 SQL Server에 연결](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) 에 추가 된 기능에 대 한 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 응용 프로그램에 연결을 허용 하는 유형 4 Kerberos 통합된 인증을 사용 하는 데이터베이스입니다.  
  
> [!NOTE]  
>  32비트 JVM(Java Virtual Machine)을 실행할 경우 운영 체제가 x64 버전이라도 x86 폴더에 있는 sqljdbc_auth.dll 파일을 사용하십시오. x64 프로세서에서 64비트 JVM을 실행할 경우 x64 폴더의 sqljdbc_auth.dll 파일을 사용하십시오.  
  
 또는 java.libary.path 시스템 속성에 sqljdbc_auth.dll의 디렉터리를 지정할 수도 있습니다. 예를 들어 JDBC 드라이버가 기본 디렉터리에 설치된 경우 Java 응용 프로그램이 시작될 때 다음과 같은 가상 컴퓨터(VM) 인수를 사용하여 DLL의 위치를 지정할 수 있습니다.  
  
 `-Djava.library.path=C:\Microsoft JDBC Driver 4.0 for SQL Server\sqljdbc_<version>\enu\auth\x86`  
  
## <a name="connecting-with-ipv6-addresses"></a>IPv6 주소로 연결  
 JDBC 드라이버는 연결 속성 컬렉션 및 serverName 연결 문자열 속성에 IPv6 주소를 사용하도록 지원합니다. Jdbc 등의 초기 serverName 값:*sqlserver*://*serverName*, 연결 문자열의 IPv6 주소에 대 한 지원 되지 않습니다. 에 대 한 이름을 사용 하 여 *serverName* 대신 원시 IPv6 주소는 연결의 모든 경우에서 작동 합니다. 자세한 내용은 다음 예를 참조하십시오.  
  
 **ServerName 속성을 사용 하려면**  
  
 `jdbc:sqlserver://;serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1;integratedSecurity=true;`  
  
 **Properties 컬렉션을 사용 하려면**  
  
 `Properties pro = new Properties();`  
  
 `pro.setProperty("serverName", "serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1");`  
  
 `Connection con = DriverManager.getConnection("jdbc:sqlserver://;integratedSecurity=true;", pro);`  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

