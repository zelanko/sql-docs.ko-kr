---
title: "Azure Active Directory 인증을 사용 하 여 연결 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.topic: article
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 83d5ad3bae131b58dd344c3f5f9bfc7f5d0c4f5a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-using-azure-active-directory-authentication"></a>Azure Active Directory 인증을 사용 하 여 연결
이 문서에서는 SQL Server 용 Microsoft JDBC Driver 6.0 (또는 이상)과 Azure Active Directory 인증 기능을 사용 하는 Java 응용 프로그램을 개발 하는 방법을 설명 합니다.

SQL Server 용 Microsoft JDBC Driver 6.0부터, Azure SQL 데이터베이스 v 12에 연결 하는 메커니즘인 Direcoty AAD (Azure Active) 인증 사용할 수 있습니다 Azure Active Directory에서 id를 사용 합니다. Azure Active Directory 인증을 사용 하 여 중앙에서 데이터베이스 사용자 및 SQL Server 인증 하는 대신 id를 관리 하 합니다. JDBC Driver 6.0 (또는 이상)를 사용 하면 Azure SQL DB에 연결 하는 데 JDBC 연결 문자열에 Azure Active Directory 자격 증명을 지정할 수 있습니다. Azure Active Directory 인증을 구성 하는 방법에 대 한 내용은 방문 [SQL 데이터베이스에서 사용 하 여 Azure Active Directory 인증 연결할](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)합니다. 

Azure Active Directory 인증을 지원 하기 위해 두 개의 새로운 연결 속성이 추가 되었습니다.
*   **인증**: 연결에 사용할 SQL 인증 방법을 나타내려면이 속성을 사용 합니다. 가능한 값은: **ActiveDirectoryIntegrated**, **ActiveDirectoryPassword**, **SqlPassword** 및 기본 **NotSpecified** .
    * 사용 하 여 ' 인증 ActiveDirectoryIntegrated =' Windows 통합된 인증을 사용 하 여 SQL 데이터베이스에 연결 합니다. 이 인증 모드를 사용 하는 온-프레미스 페더레이션 서비스 ADFS (Active Directory)를 Azure AD와 클라우드에서 페더레이션 해야 합니다. 설치 되 면 도메인 가입 된 컴퓨터에 로그온 하면 ceredentials 입력 하지 않고도 Azure SQL DB를 액세스할 수 있습니다. 
    * 사용 하 여 ' 인증 ActiveDirectoryPassword =' Azure AD 사용자 이름 및 암호를 사용 하 여 SQL 데이터베이스에 연결 합니다.
    * 사용 하 여 ' 인증 SqlPassword =' 사용자 이름/사용자 및 암호 속성을 사용 하 여 SQL Server에 연결 합니다.
    * 사용 하 여 ' authentication = NotSpecified' 필요 하지 않습니다. 이러한 인증 방법의 경우 기본적으로 두십시오.

*   **accessToken**: 액세스 토큰을 사용 하 여 SQL 데이터베이스에 연결 하려면이 속성을 사용 합니다. 만 DriverManager 클래스에서 getConnection() 메서드의 Properties 매개 변수를 사용 하 여 accessToken은 설정할 수 있습니다. 연결 URL에 사용할 수 없습니다.  

인증 속성을 참조는 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md) 페이지.  


## <a name="client-setup-requirements"></a>클라이언트 설치 요구 사항
다음 구성 요소가 클라이언트 컴퓨터에 설치 되어 있는지 확인 하세요.
* Java 7 이상
*   Microsoft JDBC Driver 6.2 (또는 이상) for SQL Server
*   액세스 토큰 기반된 인증 모드를 사용 하는 경우 해야 [azure-active directory-라이브러리-에-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 종속성이이 문서에서 예제를 실행 합니다. 참조 **액세스 토큰을 사용 하 여 연결** 자세한 내용은 섹션.
*   ActiveDirectoryPassword 인증 모드를 사용 하는 경우 해야 [azure-active directory-라이브러리-에-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 와 그 종속성입니다. 참조 **ActiveDirectoryPassword 인증 모드를 사용 하 여 연결** 자세한 내용은 섹션.
*   ActiveDirectoryIntegrated 모드를 사용 하는 경우 (ADALSQL SQL Server 용 Active Directory 인증 라이브러리를 설치 해야 합니다. DLL) 및 sqljdbc_auth.dll 합니다.
    * ADALSQL 합니다. DLL 응용 프로그램을 Azure Active Directory를 사용 하 여 Microsoft Azure SQL 데이터베이스에 인증할 수 있습니다. DLL 다운로드 [Microsoft SQL Server 용 Microsoft Active Directory 인증 라이브러리](http://www.microsoft.com/en-us/download/details.aspx?id=48742)
    * 에 대 한 ADALSQL 합니다. DLL 두 이진 버전 X86 및 X64 다운로드할 수 있는 합니다. 잘못 된 이진 버전은 설치 DLL가 없는 경우 드라이버에서 다음 오류를 발생 한 경우: "adalsql.dll을 로드할 수 없습니다 (Authentication =...). 오류 코드: 0x2. "입니다. 이런 경우에서 ADALSQL의 올바른 버전을 다운로드 합니다. DLL입니다. 
    * 드라이버 패키지에 sqljdbc_auth.dll ´ ù입니다. JDBC 드라이버를 설치한 컴퓨터에서 Windows 시스템 경로에 있는 디렉터리를 sqljdbc_auth.dll 파일을 복사 합니다. 또는 java.libary.path 시스템 속성에 sqljdbc_auth.dll의 디렉터리를 지정할 수도 있습니다. 
    * x64 프로세서에서 64비트 JVM을 실행할 경우 x64 폴더의 sqljdbc_auth.dll 파일을 사용하십시오. 
    * 32비트 JVM(Java Virtual Machine)을 실행할 경우 운영 체제가 x64 버전이라도 x86 폴더에 있는 sqljdbc_auth.dll 파일을 사용하십시오. 
    * 예를 들어 32 비트 JVM을 사용 하는 경우 JDBC 드라이버는 기본 디렉터리에 설치 되어 있으면 Java 응용 프로그램을 시작 하는 경우에 다음 가상 컴퓨터 (VM) 인수를 사용 하 여 DLL의 위치를 지정할 수 있습니다.  
        ```
        -Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86
        ```
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>ActiveDirectoryIntegrated 인증 모드를 사용 하 여 연결
다음 예제에서는 사용 하는 방법을 보여 줍니다. ' authentication = ActiveDirectoryIntegrated' 모드입니다. Azure Active Directory와 페더레이션된 도메인에 가입된 컴퓨터에이 예제를 실행 합니다. 포함 된 데이터베이스 사용자를 Azure AD 보안 주체에 또는 그룹 중 하나를 나타내는 있습니다에, 데이터베이스에 존재 해야 합니다 속하며 CONNECT 권한이 가져야 합니다. 
    
서버/데이터베이스 이름을 예를 실행 하기 전에 다음 줄에서 사용자 서버/데이터베이스의 이름을 바꿉니다.

```
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

ActiveDirectoryIntegrated 인증 모드를 사용 하도록 예제:
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class IntegratedExample {

    public static void main(String[] args) throws Exception {
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");
        ds.setHostNameInCertificate("*.database.windows.net");

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
암호가 필요 하지 않은 및 Azure Active Directory와 페더레이션된 도메인에 가입 된 컴퓨터에서이 예제를 실행 합니다. Windows 자격 증명 자동으로 사용 됩니다. 연결이 설정 되 면 다음과 같은 메시지가 표시 됩니다.
```
You have successfully logged on as: <your domain user name>
```

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>ActiveDirectoryPassword 인증 모드를 사용 하 여 연결
다음 예제에서는 사용 하는 방법을 보여 줍니다. ' authentication = ActiveDirectoryPassword' 모드입니다.

빌드하고 예제를 실행 하기 전에:
1.  클라이언트 컴퓨터에서 (기반이, 예제를 실행 하려는), 다운로드는 [azure-active directory-라이브러리-에-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성을 Java 빌드 경로에 포함
2.  다음 코드 줄을 찾아 서버/데이터베이스 이름을 서버/데이터베이스 이름으로 바꿉니다.
    ```
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  다음 코드 줄을 찾아 사용자 이름으로 연결 하려면 Azure AD 사용자의 이름으로 대체 합니다.
    ```
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

ActiveDirectoryPassword 인증 모드를 사용 하도록 예제:
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class UserPasswordExample {
    
    public static void main(String[] args) throws Exception{
        SQLServerDataSource ds = new SQLServerDataSource();
        
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        ds.setHostNameInCertificate("*.database.windows.net");
        
        Connection connection = ds.getConnection();
        
        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
연결이 설정 되 면 출력으로 다음과 같은 메시지가 나타납니다.
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 포함 된 사용자 데이터베이스가 있어야 합니다 및 포함된 된 데이터베이스 사용자를 나타내는 지정 된 Azure AD 사용자 또는 그룹을 지정 된 Azure AD 사용자에 속해 있으며 데이터베이스에 존재 해야 합니다 (제외를 Azure Active Directory CONNECT 권한을 가져야 합니다 서버 관리자 또는 그룹)


## <a name="connecting-using-access-token"></a>액세스 토큰을 사용 하 여 연결
응용 프로그램/서비스 Azure Active Directory에서 액세스 토큰을 검색 하는 사용 하 여 SQL Azure 데이터베이스에 연결할 수 있으며 Note DriverManager 클래스 getConnection() 메서드의 Properties 매개 변수를 사용 하 여 해당 accessToken 설정할만 수 있습니다. 연결 문자열에 사용할 수 없습니다.
 
다음 예제에서는 액세스 토큰 기반된 인증을 사용 하 여 Azure SQL 데이터베이스에 연결 하는 단순한 Java 응용 프로그램을 포함 합니다. 빌드하고 예제를 실행 하기 전에 다음 단계를 수행 합니다.
1.  서비스에 대 한 Azure Active Directory에 응용 프로그램 계정을 만듭니다.
    1. Azure 관리 포털에 로그인
    2. 왼쪽 탐색 창에서에서 Azure Active Directory 클릭
    3. 샘플 응용 프로그램을 등록 하려면 디렉터리 테 넌 트를 클릭 합니다. 이 데이터베이스 (데이터베이스를 호스트 하는 서버)와 연결 된 동일한 디렉터리 여야 합니다.
    4. 응용 프로그램 탭을 클릭 합니다.
    5. 서랍을에서 추가 클릭 합니다.
    6. "내 조직에서 개발 중인 응용 프로그램을 추가 하는 경우"를 클릭 합니다.
    7. Mytokentest 응용 프로그램에 대 한 이름으로 입력 하 고 "웹 응용 프로그램 및/또는 웹 API"를 선택한 다음 클릭 합니다.
    8. 이 응용 프로그램은 데몬/서비스 및 웹 응용 프로그램이 아닌을 가정할 수 없는 로그인 URL 또는 앱 ID URI입니다. 이 두 필드에 대 한 입력 http://mytokentest
    9. Azure 포털에서 계속 하는 동안 응용 프로그램의 구성 탭을 클릭
    10. 클라이언트 ID 값을 찾아 복사, 하면 나중에 필요 (즉, 응용 프로그램을 구성 하는 경우  a4bbfe26-dbaa-4fec-8ef5-223d229f647d)입니다. 아래 스냅숏을 참조 하십시오.
    11. "키" 섹션에서 키의 기간을 선택 하 여 구성을 저장 및 나중에 사용할 키를 복사 합니다. 클라이언트 암호입니다.
    12. 아래쪽에 "끝점 보기"를 클릭 하 고 나중에 사용할 "OAUTH 2.0 권한 부여 끝점" 아래에서 URL을 복사 합니다. STS URL입니다.


![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)


2. Azure Active Directory 관리자 및 응용 프로그램 사용자에 대 한 포함된 된 데이터베이스 사용자 T-SQL 명령 프로 비전을 사용 하 여 Azure SQL Server의 사용자 데이터베이스에 로그온 합니다. 참조는 [SQL 데이터베이스 또는 SQL 데이터 웨어하우스를 사용 하 여 Azure Active Directory 인증 여 연결할](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/) Azure Active Directory 관리자 및 포함된 된 데이터베이스 사용자를 만드는 방법에 대 한 자세한 내용은 합니다.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  클라이언트 컴퓨터에서 (기반이, 예제를 실행 하려는), 다운로드는 [azure-active directory-라이브러리-에-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 라이브러리 및 해당 종속성을 Java 빌드 경로에 포함 합니다. 이 라이브러리에서 Api를 사용 하 여 Azure AD에서 액세스 토큰을 검색 하는 대로이 특정 예제를 실행 하려면 azure-active directory-라이브러리-에-java만 필요한 것을 참고 합니다. 액세스 토큰을 이미 있는 경우이 단계를 건너뛸 수 있습니다. 참고 액세스 토큰을 검색 하는 예제 섹션을 제거 해야도 합니다.

아래 예제에서 STS URL의 클라이언트 ID, 클라이언트 암호, 서버 및 데이터베이스 이름을 값으로 바꿉니다.

```
import java.sql.Connection;
import java.sql.ResultSet;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD. 
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;


public class TokenBasedExample {

    public static void main(String[] args) throws Exception{

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "a4bbfe26-dbaa-4fec-8ef5-223d229f647d"; // Replace with your client ID.
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
        ds.setHostNameInCertificate("*.database.windows.net");

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
``` 

연결에 성공한 경우 출력으로 다음과 같은 메시지가 나타납니다.
```
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
