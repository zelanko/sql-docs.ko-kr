---
title: Azure Active Directory 인증을 사용하여 연결
description: Microsoft JDBC Driver for SQL Server에서 Azure Active Directory 인증 기능을 사용하는 Java 애플리케이션을 개발하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 06/17/2020
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae19b292788af43226de12a342e870768ad2ac26
ms.sourcegitcommit: a4ee6957708089f7d0dda15668804e325b8a240c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87899014"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Azure Active Directory 인증을 사용하여 연결

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 Microsoft JDBC Driver for SQL Server에서 Azure Active Directory 인증 기능을 사용하는 Java 애플리케이션을 개발하는 방법을 설명합니다.

Azure AD(Azure Active Directory)의 ID를 사용하여 Azure SQL Database v12에 연결하는 메커니즘인 Azure AD 인증을 사용할 수 있습니다. Azure Active Directory 인증을 사용하여 중앙에서 데이터베이스 사용자의 ID를 관리하고 SQL Server 인증 대신 사용할 수 있습니다. JDBC 드라이버를 사용하면 JDBC 연결 문자열에서 Azure SQL Database에 연결할 Azure Active Directory 자격 증명을 지정할 수 있습니다. Azure Active Directory 인증을 구성하는 방법에 대한 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL Database에 연결](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)을 참조하세요. 

Microsoft JDBC Driver for SQL Server에서 Azure Active Directory 인증을 지원하는 연결 속성은 다음과 같습니다.
*   **인증**:  이 속성을 사용하여 연결에 사용할 SQL 인증 방법을 지정합니다. 가능한 값은 다음과 같습니다. 
    * **ActiveDirectoryMSI**
        * 드라이버 버전 **v7.2**부터 지원되며, `authentication=ActiveDirectoryMSI`를 사용하여 "ID" 지원이 사용하도록 설정된 Azure 리소스 내부로부터 Azure SQL Database/Data Warehouse에 연결할 수 있습니다. 필요에 따라 이 인증 모드와 함께 연결/데이터 원본 속성에 **msiClientId**를 지정할 수도 있습니다. 여기에는 연결 설정을 위한 **accessToken**을 획득하는 데 사용할 관리 ID의 클라이언트 ID가 포함되어야 합니다.
    * **ActiveDirectoryIntegrated**
        * 드라이버 버전 **v6.0**부터 지원되며, `authentication=ActiveDirectoryIntegrated`를 사용하여 통합 인증을 통해 Azure SQL Database/Data Warehouse에 연결할 수 있습니다. 이 인증 모드를 사용하려면 온-프레미스 ADFS(Active Directory Federation Services)를 클라우드의 Azure Active Directory와 페더레이션해야 합니다. 설정되면 네이티브 라이브러리 ‘mssql-jdbc_auth-\<version>-\<arch>.dll’을 Windows OS의 애플리케이션 클래스 경로에 추가하거나 플랫폼 간 인증 지원을 위한 Kerberos 티켓을 설정하여 연결할 수 있습니다. 도메인 가입 컴퓨터에 로그인하는 경우 자격 증명을 묻는 메시지가 표시되지 않고 Azure SQL Database/SQL Data Warehouse에 액세스할 수 있습니다.
    * **ActiveDirectoryPassword**
        * 드라이버 버전 **v6.0**부터 지원되며, `authentication=ActiveDirectoryPassword`를 사용하여 Azure AD 보안 주체 이름 및 암호를 통해 Azure SQL Database/Data Warehouse에 연결할 수 있습니다.
    * **SqlPassword**
        * `authentication=SqlPassword`를 사용하여 사용자 이름/사용자 및 암호 속성을 사용하여 SQL Server에 연결합니다.
    * **NotSpecified**
        * 이러한 인증 방법이 필요하지 않을 경우 `authentication=NotSpecified`를 사용하거나 기본값으로 둡니다.

*   **accessToken**: 액세스 토큰을 사용하여 SQL Database에 연결하려면 이 연결 속성을 사용합니다. accessToken은 DriverManager 클래스에서 getConnection() 메서드의 Properties 매개 변수를 사용하여 설정할 수 있습니다. 연결 URL에는 사용할 수 없습니다.  

자세한 내용은 [연결 속성 설정](setting-the-connection-properties.md) 페이지에서 인증 속성을 참조하세요.  


## <a name="client-setup-requirements"></a>클라이언트 설치 요구 사항
**ActiveDirectoryMSI** 인증의 경우 클라이언트 컴퓨터에 아래 구성 요소를 설치해야 합니다.
* Java 8 이상
* Microsoft JDBC Driver 7.2 for SQL Server(이상)
* 클라이언트 환경은 Azure 리소스여야 하며 "ID" 기능 지원이 사용하도록 설정되어 있어야 합니다.
* Azure 리소스의 시스템 할당 관리 ID 또는 사용자 할당 관리 ID를 나타내거나 관리 ID가 속한 그룹 중 하나를 나타내는 포함된 데이터베이스 사용자가 대상 데이터베이스에 존재해야 하며 CONNECT 권한이 있어야 합니다.

다른 인증 모드의 경우 클라이언트 컴퓨터에 아래 구성 요소를 설치해야 합니다.
* Java 7 이상
* Microsoft JDBC Driver 6.0 for SQL Server(이상)
* 액세스 토큰 기반 인증 모드를 사용하는 경우 이 문서의 예제를 실행하려면 [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성이 필요합니다. 자세한 내용은 **액세스 토큰을 사용하여 연결** 섹션을 참조하세요.
* **ActiveDirectoryPassword** 인증 모드를 사용하는 경우 [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성이 필요합니다. 자세한 내용은 **ActiveDirectoryPassword 인증 모드를 사용하여 연결** 섹션을 참조하세요.
* **ActiveDirectoryIntegrated** 모드를 사용하는 경우 azure-activedirectory-library-for-java 및 해당 종속성이 필요합니다. 자세한 내용은 **ActiveDirectoryIntegrated 인증 모드를 사용하여 연결** 섹션을 참조하세요.

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>ActiveDirectoryMSI 인증 모드를 사용하여 연결
다음 예제에서는 `authentication=ActiveDirectoryMSI` 모드를 사용하는 방법을 보여줍니다. Azure Active Directory와 페더레이션된 Azure 가상 머신, App Service 또는 함수 앱과 같은 Azure 리소스에서 이 예제를 실행합니다.

예제를 실행하기 전에 다음 줄에서 서버/데이터베이스 이름을 자신의 서버/데이터베이스 이름으로 바꿉니다.

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMSIClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned Managed Identity to be used
```

ActiveDirectoryMSI 인증 모드를 사용하는 예제는 다음과 같습니다.

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AAD_MSI {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryMSI");
        // Optional
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned Managed Identity to be used

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

Azure 가상 머신에서 이 예제를 실행하면 _시스템 할당 관리 ID_ 또는 _사용자 할당 관리 ID_(**msiClientId**가 지정된 경우)에서 액세스 토큰을 가져오고 이 액세스 토큰을 사용하여 연결을 설정합니다. 연결이 설정되면 다음과 같은 메시지가 표시됩니다.

```bash
You have successfully logged on as: <your Managed Identity username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>ActiveDirectoryIntegrated 인증 모드를 사용하여 연결
Microsoft JDBC Driver는 버전 6.4에서 여러 플랫폼(Windows, Linux 및 macOS)에서 Kerberos 티켓을 사용하는 ActiveDirectoryIntegrated 인증에 대한 지원을 추가합니다.
자세한 내용은 [Windows, Linux 및 macOS에서 Kerberos 티켓 설정](#set-kerberos-ticket-on-windows-linux-and-macos)을 참조하세요. 또는 Windows에서 JDBC 드라이버를 사용하는 ActiveDirectoryIntegrated 인증에 mssql-jdbc_auth-\<version>-\<arch>.dll을 사용할 수도 있습니다.

> [!NOTE]
>  이전 버전의 드라이버를 사용하는 경우 이 인증 모드를 사용하는 데 필요한 각 종속성에 대한 이 [링크](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)를 확인하세요. 

다음 예제에서는 `authentication=ActiveDirectoryIntegrated` 모드를 사용하는 방법을 보여줍니다. Azure Active Directory와 페더레이션된 도메인 가입 컴퓨터에서 이 예제를 실행합니다. Azure AD 보안 주체를 나타내거나 사용자가 속한 그룹 중 하나를 나타내는 포함된 데이터베이스 사용자가 데이터베이스에 존재해야 하며 CONNECT 권한이 있어야 합니다. 

예제를 빌드하고 실행하기 전에 예제를 실행하려는 클라이언트 컴퓨터에서 [azure-activedirectory-library-for-java library](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성을 다운로드하여 Java 빌드 경로에 포함합니다.

예제를 실행하기 전에 다음 줄에서 서버/데이터베이스 이름을 자신의 서버/데이터베이스 이름으로 바꿉니다.

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

ActiveDirectoryIntegrated 인증 모드를 사용하는 예제는 다음과 같습니다.
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADIntegrated {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

클라이언트 컴퓨터에서 이 예제를 실행하면 자동으로 Kerberos 티켓이 사용되고 암호가 필요하지 않습니다. 연결이 설정되면 다음과 같은 메시지가 표시됩니다.

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-macos"></a>Windows, Linux 및 macOS에서 Kerberos 티켓 설정

현재 사용자를 Windows 도메인 계정에 연결하는 Kerberos 티켓을 설정해야 합니다. 아래에 주요 단계가 요약되어 있습니다.

#### <a name="windows"></a>Windows
JDK는 `kinit`와 함께 제공되며,이를 사용하여 Azure Active Directory와 페더레이션된 도메인 가입 컴퓨터의 KDC(키 배포 센터)에서 TGT를 가져올 수 있습니다.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>1단계: 허용 티켓 검색
- **실행 위치**: Windows
- **작업**:
  - `kinit username@DOMAIN.COMPANY.COM` 명령을 사용하여 KDC에서 TGT를 가져옵니다. 그러면 도메인 암호를 입력하라는 메시지가 표시됩니다.
  - 사용 가능한 티켓을 보려면 `klist`를 사용합니다. kinit가 성공적으로 수행된 경우에는 krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM의 티켓이 표시되어야 합니다.

> [!NOTE]
>  애플리케이션에서 KDC를 찾기 위해 `-Djava.security.krb5.conf`를 사용하여 `.ini` 파일을 지정해야 할 수 있습니다.

#### <a name="linux-and-macos"></a>Linux 및 macOS

##### <a name="requirements"></a>요구 사항
Kerberos 도메인 컨트롤러를 쿼리하기 위해 Windows 도메인에 가입된 머신에 액세스할 수 있어야 합니다.

##### <a name="step-1-find-kerberos-kdc"></a>1단계: Kerberos KDC 찾기
- **실행 위치**: Windows 명령줄
- **작업**: `nltest /dsgetdc:DOMAIN.COMPANY.COM`("DOMAIN.COMPANY.COM"이 도메인의 이름에 매핑됨)
- **샘플 출력**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **추출할 정보** DC 이름(이 경우 `co1-red-dc-33.domain.company.com`)

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>2단계: krb5.conf에서 KDC 구성
- **실행 위치**: Linux/macOS
- **작업**: 선택한 편집기에서 /etc/krb5.conf를 편집합니다. 다음 키 구성
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  이제 krb5.conf 파일을 저장하고 종료합니다.

> [!NOTE]
>  도메인은 모두 대문자여야 합니다.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>3단계: 허용 티켓 검색 테스트
- **실행 위치**: Linux/macOS
- **작업**:
  - `kinit username@DOMAIN.COMPANY.COM` 명령을 사용하여 KDC에서 TGT를 가져옵니다. 그러면 도메인 암호를 입력하라는 메시지가 표시됩니다.
  - 사용 가능한 티켓을 보려면 `klist`를 사용합니다. kinit가 성공적으로 수행된 경우에는 krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM의 티켓이 표시되어야 합니다.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>ActiveDirectoryPassword 인증 모드를 사용하여 연결
다음 예제에서는 `authentication=ActiveDirectoryPassword` 모드를 사용하는 방법을 보여줍니다.

예제를 빌드하고 실행하기 전에 다음을 수행합니다.
1.  예제를 실행하려는 클라이언트 컴퓨터에서 [azure-activedirectory-library-for-java library](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성을 다운로드하여 Java 빌드 경로에 포함합니다.
2.  다음 코드 줄을 찾아 서버/데이터베이스 이름을 자신의 서버/데이터베이스 이름으로 바꿉니다.
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  다음 코드 줄을 찾아 사용자 이름을 연결하려는 Azure AD 사용자의 이름으로 바꿉니다.
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

ActiveDirectoryPassword 인증 모드를 사용하는 예제는 다음과 같습니다.
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADUserPassword {
    
    public static void main(String[] args) throws Exception{
        
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
연결이 설정된 경우 다음 메시지가 출력으로 표시됩니다.
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 포함된 사용자 데이터베이스가 있어야 하고, 지정된 Azure AD 사용자를 나타내거나 지정된 Azure AD 사용자가 속한 그룹 중 하나를 나타내는 포함된 데이터베이스 사용자가 데이터베이스에 있어야 하며 CONNECT 권한이 있어야 합니다(Azure Active Directory 관리자 또는 그룹 제외).

## <a name="connecting-using-access-token"></a>액세스 토큰을 사용하여 연결
애플리케이션/서비스는 Azure Active Directory에서 액세스 토큰을 검색하고 이를 사용하여 Azure SQL Database/Data Warehouse에 연결할 수 있습니다.

> [!NOTE] 
> **accessToken**은 DriverManager 클래스에서 getConnection() 메서드의 Properties 매개 변수를 사용하여 설정할 수 있습니다. 연결 문자열에서는 사용할 수 없습니다.

아래 예제에는 액세스 토큰 기반 인증을 사용하여 Azure SQL Database/Data Warehouse에 연결하는 간단한 Java 애플리케이션이 포함되어 있습니다. 예제를 빌드하고 실행하기 전에 다음 단계를 수행합니다.
1.  서비스에 대한 Azure Active Directory에서 애플리케이션 계정을 만듭니다.
    1. Azure Portal에 로그인합니다.
    2. 왼쪽 탐색 창에서 Azure Active Directory를 클릭합니다.
    3. "앱 등록" 탭을 클릭합니다.
    4. 서랍에서 "새 애플리케이션 등록"을 클릭합니다.
    5. 애플리케이션의 식별 이름으로 mytokentest를 입력하고 "웹앱/API"를 선택합니다.
    6. 로그온 URL은 필요하지 않습니다. 아무 것도 제공할: "https://mytokentest" 입니다.
    7. 맨 아래에서 "만들기"를 클릭합니다.
    9. 여전히 Azure Portal에 있는 상태에서 애플리케이션의 "설정" 탭을 클릭하고 "속성" 탭을 엽니다.
    10. “애플리케이션 ID”(클라이언트 ID라고도 함) 값을 찾아 복사해 둡니다. 나중에 애플리케이션을 구성할 때 이 값이 필요합니다(예: 1846943b-ad04-4808-aa13-4702d908b5c1). 다음 스냅샷을 참조하세요.
    11. "키" 섹션에서 이름 필드를 입력하고 키의 기간을 선택한 다음 구성을 저장하여 키를 만듭니다. 값 필드는 비워 둡니다. 저장하면 값 필드가 자동으로 채워집니다. 생성된 값을 복사합니다. 클라이언트 비밀입니다.
    12. 왼쪽 패널에서 Azure Active Directory를 클릭합니다. "앱 등록"에서 "엔드포인트" 탭을 찾습니다. "OATH 2.0 토큰 엔드포인트"에서 URL을 복사합니다. 이것이 STS URL입니다.
    
    ![JDBC_AAD_Token](media/jdbc_aad_token.png)  
2. Azure SQL Server의 사용자 데이터베이스에 Azure Active Directory 관리자로 로그인하고 T-SQL 명령을 사용하여 애플리케이션 보안 주체에 대해 포함된 데이터베이스 사용자를 프로비전합니다. Azure Active Directory 관리자 및 포함된 데이터베이스 사용자를 만드는 방법에 대한 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL Database에 또는 SQL Data Warehouse에 연결](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)을 참조하세요.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  예제를 실행하려는 클라이언트 컴퓨터에서 [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성을 다운로드하여 Java 빌드 경로에 포함합니다. azure-activedirectory-library-for-java는 이 예제를 실행하는 데만 필요합니다. 이 예제에서는 이 라이브러리의 API를 사용하여 Azure AD에서 액세스 토큰을 검색합니다. 액세스 토큰이 이미 있는 경우 이 단계를 건너뜁니다. 또한 예제에서 액세스 토큰을 검색하는 섹션을 제거해야 합니다.

다음 예제에서는 STS URL, 클라이언트 ID, 클라이언트 암호, 서버 및 데이터베이스 이름을 자신의 값으로 바꿉니다.

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD.
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;

public class AADTokenBased {

    public static void main(String[] args) throws Exception {

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);

        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

연결이 성공하면 다음 메시지가 출력됩니다.

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
