---
title: Azure Active Directory 인증을 사용 하 여 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6df50936da3d8b31ec3bc7ecd62212fa6987c4d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32833084"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Azure Active Directory 인증을 사용 하 여 연결

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 SQL Server 용 Microsoft JDBC Driver 6.0 (또는 이상)과 Azure Active Directory 인증 기능을 사용 하는 Java 응용 프로그램을 개발 하는 방법을 설명 합니다.

Azure SQL 데이터베이스 v 12에 연결 하는 메커니즘은 Azure Active Directory (AAD) 인증을 사용할 수 있습니다 Azure Active Directory에서 id를 사용 합니다. Azure Active Directory 인증을 사용 하 여 중앙에서 데이터베이스 사용자 및 SQL Server 인증 하는 대신 id를 관리 하 합니다. JDBC 드라이버를 사용 하면 Azure SQL DB에 연결 하는 데 JDBC 연결 문자열에 Azure Active Directory 자격 증명을 지정할 수 있습니다. Azure Active Directory 인증을 구성 하는 방법에 대 한 내용은 방문 [SQL 데이터베이스에서 사용 하 여 Azure Active Directory 인증 연결할](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)합니다. 

Azure Active Directory 인증을 지원 하기 위해 두 개의 새로운 연결 속성이 추가 되었습니다.
*   **인증**: 연결에 사용할 SQL 인증 방법을 나타내려면이 속성을 사용 합니다. 가능한 값은: **ActiveDirectoryIntegrated**, **ActiveDirectoryPassword**, **SqlPassword**, 및 기본 **NotSpecified**.
    * 사용 하 여 ' 인증 ActiveDirectoryIntegrated =' Windows 통합된 인증을 사용 하 여 SQL 데이터베이스에 연결 합니다. 이 인증 모드를 사용 하는 온-프레미스 페더레이션 서비스 ADFS (Active Directory)를 Azure AD와 클라우드에서 페더레이션 해야 합니다. 이 설치 되 면 Kerberos 티켓 뿐만 아니라, 도메인 가입 된 컴퓨터에 로그온 하면 자격 증명 입력 하지 않고도 Azure SQL DB를 액세스할 수 있습니다. 
    * 사용 하 여 ' 인증 ActiveDirectoryPassword =' Azure AD 사용자 이름 및 암호를 사용 하 여 SQL 데이터베이스에 연결 합니다.
    * 사용 하 여 ' 인증 SqlPassword =' 사용자 이름/사용자 및 암호 속성을 사용 하 여 SQL Server에 연결 합니다.
    * 사용 하 여 ' 인증 NotSpecified =' 이러한 인증 방법을 필요할 경우 기본값으로 둡니다.

*   **accessToken**: 액세스 토큰을 사용 하 여 SQL 데이터베이스에 연결 하려면이 속성을 사용 합니다. 만 DriverManager 클래스에서 getConnection() 메서드의 Properties 매개 변수를 사용 하 여 accessToken은 설정할 수 있습니다. 연결 URL에 사용할 수 없습니다.  

인증 속성을 참조는 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md) 페이지.  


## <a name="client-setup-requirements"></a>클라이언트 설치 요구 사항
다음 구성 요소가 클라이언트 컴퓨터에 설치 되어 있는지 확인 하세요.
* Java 7 이상
*   Microsoft JDBC Driver 6.0 (또는 이상) for SQL Server
*   액세스 토큰 기반 인증 모드를 사용 하는 경우 해야 [azure-active directory-라이브러리-에-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 종속성이이 문서에서 예제를 실행 합니다. 자세한 내용은 참조 **액세스 토큰을 사용 하 여 연결** 섹션.
*   ActiveDirectoryPassword 인증 모드를 사용 하는 경우 해야 [azure-active directory-라이브러리-에-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 와 그 종속성입니다. 자세한 내용은 참조 **ActiveDirectoryPassword 인증 모드를 사용 하 여 연결** 섹션.
*   ActiveDirectoryIntegrated 모드를 사용 하는 경우 azure-active directory-라이브러리-에-java 및 해당 종속성이 필요 합니다. 자세한 내용은 참조 **ActiveDirectoryIntegrated 인증 모드를 사용 하 여 연결** 섹션.
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>ActiveDirectoryIntegrated 인증 모드를 사용 하 여 연결
 버전 6.4 Microsoft JDBC Driver ActiveDirectoryIntegrated 인증 Kerberos 티켓을 사용 하 여 여러 플랫폼 (Windows/Linux 및 Mac)에 대 한 지원을 추가 합니다.
참조 [Windows, Linux 및 Mac에서 설정 하는 Kerberos 티켓](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) 내용을 확인 합니다. 또는 windows에서 sqljdbc_auth.dll JDBC 드라이버와 함께 ActiveDirectoryIntegrated 인증용 데도 수 있습니다.

> [!NOTE]
>  이전 버전의 드라이버를 사용 하는 경우이 옵션을 선택 [링크](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) 이 인증 모드를 사용 하는 데 필요한 각 종속성에 대 한 합니다. 

다음 예제에서는 사용 하는 방법을 보여 줍니다. ' authentication = ActiveDirectoryIntegrated' 모드입니다. Azure Active Directory와 페더레이션된 도메인에 가입된 컴퓨터에이 예제를 실행 합니다. 포함 된 데이터베이스 사용자를 Azure AD 보안 주체에 또는 그룹 중 하나를 나타내는 있습니다에, 데이터베이스에 존재 해야 합니다 속하며 CONNECT 권한이 가져야 합니다. 

빌드하고 클라이언트 컴퓨터에서 예제를 실행 하기 전에 (기반이, 예제를 실행 하려는), 다운로드는 [azure-active directory-라이브러리-에-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성을 Java 빌드 경로에 포함

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
Kerberos 티켓을 사용 하 여 클라이언트 컴퓨터에서 자동으로이 예제를 실행 하 고 암호가 필요 합니다. 연결 된 경우에 다음과 같은 메시지가 나타납니다.
```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Windows, Linux 및 Mac에서 Kerberos 티켓을 설정 합니다.

현재 사용자는 Windows 도메인 계정에 연결 하는 Kerberos 티켓을 설정 해야 합니다. 주요 단계를 요약 한 아래에 포함 되어 있습니다.

#### <a name="windows"></a>Windows
JDK와 함께 제공 `kinit` 가입 된 도메인에 KDC (키 배포 센터)에서 TGT를 가져오는 데 사용할 수 있는 Azure Active Directory와 페더레이션 하는 컴퓨터입니다.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>1 단계: 티켓 허용 티켓 검색
- **실행**: Windows
- **작업**:
  - 명령을 사용 하 여 `kinit username@DOMAIN.COMPANY.COM` TGT는 KDC에서 가져오려는 다음 물어봅니다 도메인 암호입니다.
  - 사용 하 여 `klist` 사용 가능한 티켓을 볼 수 있습니다. kinit에 성공 하면 krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM 티켓을 표시 되어야 합니다.

> [!NOTE]
>  지정 해야 할 수도 있습니다는 `.ini` 파일 `-Djava.security.krb5.conf` KDC 찾을 응용 프로그램에 대 한 합니다.

#### <a name="linux-and-mac"></a>Linux 및 Mac

##### <a name="requirements"></a>요구 사항
Kerberos 도메인 컨트롤러를 쿼리 하기 위해 Windows 도메인에 가입 된 컴퓨터에 대 한 액세스

##### <a name="step-1-find-kerberos-kdc"></a>1 단계: Kerberos KDC 찾기
- **실행**: Windows 명령줄
- **동작**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (여기서 "DOMAIN.COMPANY.COM" 매핑됩니다 도메인의 이름)
- **샘플 출력**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **정보를 추출할** DC 이름,이 경우 `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>2 단계: krb5.conf에서 KDC를 구성합니다.
- **실행**: Linux/Mac
- **작업**: /etc/krb5.conf 선택한 편집기에서 편집 합니다. 다음 키를 구성
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  그런 다음, krb5.conf 파일 및 종료

> [!NOTE]
>  도메인은 모두 대문자로 이어야 합니다.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>3 단계: 테스트 티켓 허용 티켓 검색
- **실행**: Linux/Mac
- **작업**:
  - 명령을 사용 하 여 `kinit username@DOMAIN.COMPANY.COM` TGT는 KDC에서 가져오려는 다음 물어봅니다 도메인 암호입니다.
  - 사용 하 여 `klist` 사용 가능한 티켓을 볼 수 있습니다. kinit에 성공 하면 krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM 티켓을 표시 되어야 합니다.

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
연결이 설정 되 면 다음과 같은 메시지가 출력으로 나타납니다.
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 포함 된 사용자 데이터베이스가 있어야 합니다 및 포함된 된 데이터베이스 사용자를 나타내는 지정 된 Azure AD 사용자 또는 그룹을 지정 된 Azure AD 사용자에 속해 있으며 데이터베이스에 존재 해야 합니다 (제외를 Azure Active Directory CONNECT 권한을 가져야 합니다 서버 관리자 또는 그룹)


## <a name="connecting-using-access-token"></a>액세스 토큰을 사용 하 여 연결
응용 프로그램/서비스 Azure Active Directory에서 액세스 토큰을 검색 하는 사용 하 여 SQL Azure 데이터베이스에 연결할 수 있으며 Note DriverManager 클래스 getConnection() 메서드의 Properties 매개 변수를 사용 하 여 해당 accessToken 설정할만 수 있습니다. 연결 문자열에 사용할 수 없습니다.
 
다음 예제에서는 액세스 토큰 기반 인증을 사용 하 여 Azure SQL 데이터베이스에 연결 하는 단순한 Java 응용 프로그램을 포함 합니다. 빌드하고 예제를 실행 하기 전에 다음 단계를 수행 합니다.
1.  서비스에 대 한 Azure Active Directory에 응용 프로그램 계정을 만듭니다.
    1. Azure 관리 포털에 로그인
    2. 왼쪽 탐색 창에서에서 Azure Active Directory 클릭
    3. "응용 프로그램 등록" 탭을 클릭 합니다.
    4. 서랍을에서 "새 응용 프로그램 등록"을 클릭 합니다.
    5. 응용 프로그램에 대 한 알기 쉬운 이름으로 mytokentest를 입력 하 고 "웹 응용 프로그램/API"를 선택 합니다.
    6. 우리는 로그온 URL 필요 하지 않습니다. 아무 것도 제공 하는 것: "http://mytokentest"입니다.
    7. 맨 아래에 "만들기"를 클릭 합니다.
    9. Azure 포털에서 계속 하는 동안 응용 프로그램의 "설정" 탭을 클릭 하 고 "속성" 탭을 엽니다.
    10. "응용 프로그램 ID" 즉, 클라이언트 ID () 값을 찾아 복사 제외 하 고, 지정 해야이 나중에 응용 프로그램 (예를 들어 1846943b-ad04-4808-aa13-4702d908b5c1)을 구성 합니다. 스냅숏을 참조 합니다.
    11. "키" 섹션에서 이름 필드에 입력, 키의 기간을 선택 하 고 (값 필드를 비워 둠) 구성을 저장 하 여 키를 만듭니다. 값 필드 여야 합니다 저장 한 후 자동으로 가득 차면 생성 되는 값을 복사 합니다. 클라이언트 암호입니다.
    12. 왼쪽 패널에서 Azure Active Directory를 클릭 합니다. "응용 프로그램 등록"에서 "끝점" 탭을 찾습니다. "OATH 2.0 토큰 끝점" 아래에서 URL을 복사, STS URL입니다.
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Azure Active Directory 관리자 및 주 응용 프로그램에 대 한 포함된 된 데이터베이스 사용자 T-SQL 명령 프로 비전을 사용 하 여 Azure SQL Server의 사용자 데이터베이스에 로그온 합니다. 참조는 [SQL 데이터베이스 또는 SQL 데이터 웨어하우스를 사용 하 여 Azure Active Directory 인증 여 연결할](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) Azure Active Directory 관리자 및 포함된 된 데이터베이스 사용자를 만드는 방법에 대 한 자세한 내용은 합니다.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  클라이언트 컴퓨터에서 (기반이, 예제를 실행 하려는), 다운로드는 [azure-active directory-라이브러리-에-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 라이브러리 및 해당 종속성을 Java 빌드 경로에 포함 합니다. 이 라이브러리에서 Api를 사용 하 여 Azure AD에서 액세스 토큰을 검색 하는 대로이 특정 예제를 실행 하려면 azure-active directory-라이브러리-에-java만 필요한 것을 참고 합니다. 액세스 토큰을 이미 있는 경우이 단계를 건너뛸 수 있습니다. 또한 검색 액세스 토큰 예제에서 섹션을 제거 해야 하는 참고 합니다.

다음 예에서 STS URL, 클라이언트 ID, 클라이언트 암호, 서버 및 데이터베이스 이름을 값으로 바꿉니다.

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
        ds.setHostNameInCertificate("*.database.windows.net");

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
``` 

연결이 성공적 이면 다음과 같은 메시지가 출력으로 나타납니다.
```
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
