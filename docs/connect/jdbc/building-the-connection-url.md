---
title: 연결 URL 작성 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 44996746-d373-4f59-9863-a8a20bb8024a
caps.latest.revision: 53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31cc897383c7ffc8a11bc74a1881b12313da68f4
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278824"
---
# <a name="building-the-connection-url"></a>연결 URL 작성
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  연결 URL의 일반적인 형식은 다음과 같습니다.  
  
 `jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]]`  
  
 각 항목이 나타내는 의미는 다음과 같습니다.  
  
-   **jdbc:sqlserver://**(필수)는 하위 프로토콜이라고 하며 일정한 형태를 나타냅니다.  
  
-   **serverName**(옵션)은 연결할 서버의 주소입니다. 이는 DNS나 IP 주소일 수도 있고 로컬 컴퓨터인 경우 localhost나 127.0.0.1일 수도 있습니다. 연결 URL에 지정하지 않은 경우 속성 컬렉션에 서버 이름을 지정해야 합니다.  
  
-   **instanceName**(옵션)은 serverName에서 연결할 인스턴스입니다. instanceName을 지정하지 않으면 기본 인스턴스에 연결됩니다.  
  
-   **portNumber**(옵션)는 serverName에서 연결할 포트이며 기본값은 1433입니다. 기본값을 사용하는 경우 URL에 포트나 앞에 붙는 ':'을 지정할 필요가 없습니다.  
  
    > [!NOTE]  
    >  연결 성능을 최적화하려면 명명된 인스턴스에 연결할 때 portNumber를 설정해야 합니다. 그러면 포트 번호를 확인하기 위해 서버까지 왕복 이동할 필요가 없습니다. portNumber 및 instanceName을 모두 사용하는 경우 portNumber가 우선 순위를 갖고 instanceName은 무시됩니다.  
  
-   **property**(옵션)는 하나 이상의 옵션 연결 속성입니다. 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요. 목록에 있는 속성은 모두 지정할 수 있습니다. 속성은 세미콜론(';')으로만 구분할 수 있고 중복될 수 없습니다.  
  
> [!CAUTION]  
>  보안을 위해 사용자 입력을 토대로 연결 URL을 작성하지 않는 것이 좋습니다. URL에는 서버 이름과 드라이버만 지정해야 합니다. 사용자 이름 및 암호 값에는 연결 속성 컬렉션을 사용합니다. JDBC 응용 프로그램의 보안에 대 한 자세한 내용은 참조 하세요. [JDBC 드라이버 응용 프로그램 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)합니다.  
  
## <a name="connection-examples"></a>연결 예  
 사용자 이름 및 암호를 사용하여 로컬 컴퓨터에서 기본 데이터베이스에 연결합니다.  
  
 `jdbc:sqlserver://localhost;user=MyUserName;password=*****;`  
  
> [!NOTE]  
>  이전 예제에서는 연결 문자열에 사용자 이름과 암호를 사용했지만 보다 안전한 통합 보안을 사용해야 합니다. 자세한 내용은 이 항목 후반에 있는 [통합 인증으로 연결](#Connectingintegrated) 섹션을 참조하십시오.  
  
 다음 연결 문자열에서는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서 지원되는 운영 체제에서 실행 중인 응용 프로그램에서 통합 인증 및 Kerberos를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스에 연결하는 방법의 예를 보여 줍니다.  
  
```java
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
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에서는 서버당 여러 개의 데이터베이스 인스턴스를 설치할 수 있습니다. 각 인스턴스는 특정 이름으로 식별합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]의 명명된 인스턴스에 연결하려면 명명된 인스턴스의 포트 번호를 지정하거나(기본 설정) 인스턴스 이름을 JDBC URL 속성 또는 **datasource** 속성으로 지정합니다. 인스턴스 이름이나 포트 번호 속성을 지정하지 않으면 기본 인스턴스에 대한 연결이 설정됩니다. 다음 예를 참조하십시오.  
  
 포트 번호를 사용하려면 다음을 수행합니다.  
  
 `jdbc:sqlserver://localhost:1433;integratedSecurity=true;<more properties as required>;`  
  
 JDBC URL 속성을 사용하려면 다음을 수행합니다.  
  
 `jdbc:sqlserver://localhost;instanceName=instance1;integratedSecurity=true;<more properties as required>;`  
  
## <a name="escaping-values-in-the-connection-url"></a>연결 URL에서 값 이스케이프 처리  
 공백, 세미콜론, 인용 부호와 같은 특수 문자가 삽입되어 있으므로 연결 URL 값의 일부를 이스케이프 처리해야 하는 경우가 있을 수 있습니다. JDBC 드라이버는 이런 문자가 중괄호로 묶인 경우 이스케이프 처리를 지원합니다. 예를 들어 {;}는 세미콜론을 이스케이프 처리합니다.  
  
 이스케이프 처리되는 값에 특수 문자(특히 '=', ';', '[]' 및 공백)는 포함될 수 있지만 중괄호는 포함될 수 없습니다. 이스케이프 처리해야 하는 값에 중괄호가 포함된 경우 해당 값을 속성 컬렉션에 추가해야 합니다.  
  
> [!NOTE]  
>  중괄호 안의 공백은 리터럴이며 잘리지 않습니다.  
  
##  <a name="Connectingintegrated"></a> Windows에서 통합 인증으로 연결  
 JDBC 드라이버는 integratedSecurity 연결 문자열 속성을 통해 Windows 운영 체제에서 형식 2 통합 인증을 사용할 수 있습니다. 통합 인증을 사용하려면 sqljdbc_auth.dll 파일을 JDBC 드라이버가 설치된 컴퓨터의 Windows 시스템 경로에 있는 디렉터리에 복사합니다.  
  
 sqljdbc_auth.dll 파일은 다음 위치에 설치되어 있습니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \auth\  
  
 지 원하는 운영 체제에 대 한 합니다 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 참조 하세요 [Kerberos 통합 인증을 사용 하려면 SQL Server에 연결](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) 에 추가 된 기능에 대 한 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 응용 프로그램에 연결할 수 있도록를 유형 4 Kerberos 통합된 인증을 사용 하는 데이터베이스입니다.  
  
> [!NOTE]  
>  32비트 JVM(Java Virtual Machine)을 실행할 경우 운영 체제가 x64 버전이라도 x86 폴더에 있는 sqljdbc_auth.dll 파일을 사용하십시오. x64 프로세서에서 64비트 JVM을 실행할 경우 x64 폴더의 sqljdbc_auth.dll 파일을 사용하십시오.  
  
 또는 java.libary.path 시스템 속성에 sqljdbc_auth.dll의 디렉터리를 지정할 수도 있습니다. 예를 들어 JDBC 드라이버가 기본 디렉터리에 설치된 경우 Java 응용 프로그램이 시작될 때 다음과 같은 가상 컴퓨터(VM) 인수를 사용하여 DLL의 위치를 지정할 수 있습니다.  
  
 `-Djava.library.path=C:\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_<version>\enu\auth\x86`  
  
## <a name="connecting-with-ipv6-addresses"></a>IPv6 주소로 연결  
 JDBC 드라이버는 연결 속성 컬렉션 및 serverName 연결 문자열 속성에 IPv6 주소를 사용하도록 지원합니다. jdbc:*sqlserver*://*serverName*과 같은 serverName 초기값은 연결 문자열의 IPv6 주소에는 지원되지 않습니다. 원시 IPv6 주소 대신 *serverName*의 이름을 사용하면 모든 경우의 연결에 원활하게 작동합니다. 자세한 내용은 다음 예를 참조하십시오.  
  
 **serverName 속성을 사용하려면**  
  
 `jdbc:sqlserver://;serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1;integratedSecurity=true;`  
  
 **속성 컬렉션을 사용하려면**  
  
 `Properties pro = new Properties();`  
  
 `pro.setProperty("serverName", "serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1");`  
  
 `Connection con = DriverManager.getConnection("jdbc:sqlserver://;integratedSecurity=true;", pro);`  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
