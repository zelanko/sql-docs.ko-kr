---
title: Azure Active Directory 인증을 사용하여 연결 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b596936010fcdce4eb5c0701c5f0c6631cd9687e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028119"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Azure Active Directory 인증을 사용하여 연결

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 SQL Server 용 Microsoft JDBC Driver를 사용 하 여 Azure Active Directory 인증 기능을 사용 하는 Java 응용 프로그램을 개발 하는 방법에 대 한 정보를 제공 합니다.

Azure Active Directory에서 id를 사용 하 여 Azure SQL Database v12에 연결 하는 메커니즘인 AAD (Azure Active Directory) 인증을 사용할 수 있습니다. Azure Active Directory 인증을 사용하여 중앙에서 데이터베이스 사용자의 ID를 관리하고 SQL Server 인증 대신 사용할 수 있습니다. JDBC 드라이버를 사용 하면 JDBC 연결 문자열에 Azure Active Directory 자격 증명을 지정 하 여 Azure SQL DB에 연결할 수 있습니다. Azure Active Directory 인증을 구성 하는 방법에 대 한 자세한 내용은 [Azure Active Directory 인증을 사용 하 여 SQL Database에 연결을](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)참조 하세요. 

Microsoft JDBC Driver for SQL Server에서 Azure Active Directory 인증을 지 원하는 연결 속성은 다음과 같습니다.
*   **인증**:이 속성을 사용 하 여 연결에 사용할 SQL 인증 방법을 지정 합니다. 가능한 값은 
    * **ActiveDirectoryMSI**
        * 드라이버 버전 **v 7.2**이후 지원 되며 `authentication=ActiveDirectoryMSI` , "id" 지원을 사용 하도록 설정 하 여 Azure 리소스 내부에서 Azure SQL Database/데이터 웨어하우스에 연결 하는 데 사용할 수 있습니다. 필요에 따라 **msiClientId** 를 설정 하기 위해 **accessToken** 를 획득 하는 데 사용할 관리 서비스 ID의 클라이언트 ID를 포함 해야 하는이 인증 모드와 연결/데이터 원본 속성에도 지정할 수 있습니다. 연결입니다.
    * **ActiveDirectoryIntegrated**
        * 드라이버 버전 **v 6.0** `authentication=ActiveDirectoryIntegrated` 부터 지원 되며 통합 인증을 사용 하 여 Azure SQL Database/데이터 웨어하우스에 연결 하는 데 사용할 수 있습니다. 이 인증 모드를 사용 하려면 온-프레미스 Active Directory Federation Services (ADFS)를 클라우드의 Azure Active Directory와 페더레이션 해야 합니다. 설정 되 면 네이티브 라이브러리 ' sqljdbc_auth '를 Windows OS의 응용 프로그램 클래스 경로에 추가 하거나 플랫폼 간 인증 지원에 대 한 Kerberos 티켓을 설정 하 여 연결할 수 있습니다. 도메인에 가입 된 컴퓨터에 로그인 하는 경우 자격 증명을 묻는 메시지가 표시 되지 않고 Azure SQL DB/DW에 액세스할 수 있습니다.
    * **ActiveDirectoryPassword**
        * 드라이버 버전 **v 6.0** `authentication=ActiveDirectoryPassword` 부터 지원 되며 Azure AD 사용자 이름 및 암호를 사용 하 여 Azure SQL Database/데이터 웨어하우스에 연결 하는 데 사용할 수 있습니다.
    * **SqlPassword**
        * 사용자 `authentication=SqlPassword` 이름/사용자 및 암호 속성을 사용 하 여 SQL Server에 연결 하는 데 사용 합니다.
    * **NotSpecified**
        * 이러한 `authentication=NotSpecified` 인증 방법이 필요 하지 않을 경우에는이를 기본값으로 사용 하거나 기본값으로 둡니다.

*   **accessToken**: 액세스 토큰을 사용 하 여 SQL Database에 연결 하려면이 연결 속성을 사용 합니다. accessToken는 DriverManager 클래스에서 getConnection () 메서드의 Properties 매개 변수를 사용 하 여 설정할 수 있습니다. 연결 URL에는 사용할 수 없습니다.  

자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md) 페이지에서 인증 속성을 참조 하세요.  


## <a name="client-setup-requirements"></a>클라이언트 설치 요구 사항
**ActiveDirectoryMSI** 인증의 경우 클라이언트 컴퓨터에 아래 구성 요소를 설치 해야 합니다.
* Java 8 이상
* SQL Server 용 Microsoft JDBC Driver 7.2 이상
* 클라이언트 환경은 Azure 리소스 여야 하며 "Id" 기능 지원이 사용 하도록 설정 되어 있어야 합니다.
* Azure 리소스의 시스템 할당 관리 Id 또는 사용자 할당 관리 Id 또는 MSI가 속한 그룹 중 하나를 나타내는 포함 된 데이터베이스 사용자는 대상 데이터베이스에 존재 해야 하며 CONNECT 권한이 있어야 합니다.

다른 인증 모드의 경우 클라이언트 컴퓨터에 아래 구성 요소를 설치 해야 합니다.
* Java 7 이상
* SQL Server 용 Microsoft JDBC Driver 6.0 이상
* 액세스 토큰 기반 인증 모드를 사용 하는 경우이 문서의 예제를 실행 하려면 [activedirectory](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성이 필요 합니다. 자세한 내용은 **액세스 토큰을 사용 하 여 연결** 섹션을 참조 하세요.
* **ActiveDirectoryPassword** 인증 모드를 사용 하는 경우 [azure-activedirectory-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성이 필요 합니다. 자세한 내용은 **ActiveDirectoryPassword 인증 모드를 사용 하 여 연결** 섹션을 참조 하세요.
* **ActiveDirectoryIntegrated** 모드를 사용 하는 경우에는 azure-activedirectory-java 및 해당 종속성이 필요 합니다. 자세한 내용은 **ActiveDirectoryIntegrated 인증 모드를 사용 하 여 연결** 섹션을 참조 하세요.

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>ActiveDirectoryMSI 인증 모드를 사용 하 여 연결
다음 예제에서는 `authentication=ActiveDirectoryMSI` 모드를 사용하는 방법을 보여줍니다. Azure 리소스, e, g, Azure 가상 머신, App Service 또는 Azure Active Directory 페더레이션 된 함수 앱 내에서이 예제를 실행 합니다.

예제를 실행 하기 전에 다음 줄에서 서버/데이터베이스 이름을 서버/데이터베이스 이름으로 바꿉니다.

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

ActiveDirectoryMSI 인증 모드를 사용 하는 예제는 다음과 같습니다.

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
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used

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

Azure 가상 머신에서이 예제를 실행 하면 _시스템 할당 관리 id_ 또는 _사용자 할당 관리 id_ ( **msiClientId** 가 지정 된 경우)에서 액세스 토큰을 페치 하 고 인출 된 액세스를 사용 하 여 연결을 설정 합니다. 토큰. 연결이 설정 되 면 다음과 같은 메시지가 표시 됩니다.

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>ActiveDirectoryIntegrated 인증 모드를 사용 하 여 연결
버전 6.4에서 Microsoft JDBC Driver는 여러 플랫폼 (Windows, Linux 및 macOS)에서 Kerberos 티켓을 사용 하는 ActiveDirectoryIntegrated 인증에 대 한 지원을 추가 합니다.
자세한 내용은 [Windows, Linux 및 Mac에서 Kerberos 티켓 설정](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) 을 참조 하세요. 또는 Windows에서 sqljdbc_auth는 JDBC 드라이버를 사용 하 여 ActiveDirectoryIntegrated 인증에도 사용할 수 있습니다.

> [!NOTE]
>  이전 버전의 드라이버를 사용 하는 경우이 인증 모드를 사용 하는 데 필요한 각 종속성에 대해이 [링크](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) 를 선택 합니다. 

다음 예제에서는 `authentication=ActiveDirectoryIntegrated` 모드를 사용하는 방법을 보여줍니다. Azure Active Directory와 페더레이션 된 도메인에 가입 된 컴퓨터에서이 예제를 실행 합니다. Azure AD 보안 주체를 나타내는 포함 된 데이터베이스 사용자 또는 사용자가 속한 그룹 중 하나는 데이터베이스에 존재 해야 하며 CONNECT 권한이 있어야 합니다. 

예제를 빌드하고 실행 하기 전에 예제를 실행 하려는 클라이언트 컴퓨터에서 [activedirectory 라이브러리](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성을 다운로드 하 여 java 빌드 경로에 포함 합니다 .이 라이브러리는

예제를 실행 하기 전에 다음 줄에서 서버/데이터베이스 이름을 서버/데이터베이스 이름으로 바꿉니다.

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

ActiveDirectoryIntegrated 인증 모드를 사용 하는 예제는 다음과 같습니다.
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

클라이언트 컴퓨터에서이 예제를 실행 하면 Kerberos 티켓이 자동으로 사용 되 고 암호가 필요 하지 않습니다. 연결이 설정 되 면 다음과 같은 메시지가 표시 됩니다.

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Windows, Linux 및 Mac에서 Kerberos 티켓 설정

현재 사용자를 Windows 도메인 계정에 연결 하는 Kerberos 티켓을 설정 해야 합니다. 주요 단계에 대 한 요약이 아래에 포함 되어 있습니다.

#### <a name="windows"></a>Windows
JDK는와 `kinit`함께 제공 되며,이를 사용 하 여 Azure Active Directory 페더레이션 된 도메인 가입 컴퓨터의 키 배포 센터 (KDC)에서 TGT를 가져올 수 있습니다.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>1 단계: 티켓을 부여 하는 티켓 검색
- **실행**위치: Windows
- **작업**:
  - 명령을 `kinit username@DOMAIN.COMPANY.COM` 사용 하 여 KDC에서 TGT를 가져온 다음 도메인 암호를 입력 하 라는 메시지가 표시 됩니다.
  - 사용 `klist` 가능한 티켓을 확인 하는 데 사용 합니다. Kinit가 성공적으로 완료 되 면 krbtgt/DOMAIN. .COM @ DOMAIN.COMPANY.COM의 티켓이 표시 됩니다.

> [!NOTE]
>  응용 프로그램에서 KDC를 찾기 `.ini` 위해 `-Djava.security.krb5.conf` 파일을 지정 해야 할 수 있습니다.

#### <a name="linux-and-mac"></a>Linux 및 Mac

##### <a name="requirements"></a>요구 사항
Kerberos 도메인 컨트롤러를 쿼리하기 위해 Windows 도메인에 가입된 머신에 액세스할 수 있어야 합니다.

##### <a name="step-1-find-kerberos-kdc"></a>1 단계: Kerberos KDC 찾기
- **실행**위치: Windows 명령줄
- **작업**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` ("DOMAIN.COMPANY.COM"가 도메인의 이름에 매핑됨)
- **샘플 출력**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **추출할 정보** DC 이름 (이 경우)`co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>2 단계: krb5.conf에서 KDC 구성
- **실행**위치: Linux/Mac
- **작업**: 선택한 편집기에서/Etc/krb5.conf를 편집 합니다. 다음 키 구성
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

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>3단계: TGS(Ticket-Granting Service) 검색 테스트
- **실행**위치: Linux/Mac
- **작업**:
  - 명령을 `kinit username@DOMAIN.COMPANY.COM` 사용 하 여 KDC에서 TGT를 가져온 다음 도메인 암호를 입력 하 라는 메시지가 표시 됩니다.
  - 사용 `klist` 가능한 티켓을 확인 하는 데 사용 합니다. Kinit가 성공적으로 완료 되 면 krbtgt/DOMAIN. .COM @ DOMAIN.COMPANY.COM의 티켓이 표시 됩니다.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>ActiveDirectoryPassword 인증 모드를 사용 하 여 연결
다음 예제에서는 `authentication=ActiveDirectoryPassword` 모드를 사용하는 방법을 보여줍니다.

예제를 빌드하고 실행 하기 전에 다음을 수행 합니다.
1.  클라이언트 컴퓨터 (예제를 실행 하려는 경우)에서 [activedirectory 라이브러리](https://github.com/AzureAD/azure-activedirectory-library-for-java) 및 해당 종속성을 다운로드 하 여 java 빌드 경로에 포함 합니다.
2.  다음 코드 줄을 찾아 서버/데이터베이스 이름을 서버/데이터베이스 이름으로 바꿉니다.
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  다음 코드 줄을 찾아 사용자 이름을 연결 하려는 AAD 사용자의 이름으로 바꿉니다.
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

ActiveDirectoryPassword 인증 모드를 사용 하는 예제는 다음과 같습니다.
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
연결이 설정 된 경우 다음 메시지가 출력으로 표시 되어야 합니다.
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 포함 된 사용자 데이터베이스가 있어야 하 고, 지정 된 Azure ad 사용자를 나타내는 포함 된 데이터베이스 사용자 또는 지정 된 Azure AD 사용자가 속한 그룹 중 하나를 나타내는 포함 된 데이터베이스 사용자가 데이터베이스에 있어야 하 고 연결 권한이 있어야 합니다. 단,를 제외 하 고는 Azure Active Directory 서버 관리 또는 그룹)

## <a name="connecting-using-access-token"></a>액세스 토큰을 사용 하 여 연결
응용 프로그램/서비스는 Azure Active Directory에서 액세스 토큰을 검색 하 고이를 사용 하 여 Azure SQL Database/데이터 웨어하우스에 연결할 수 있습니다.

> [!NOTE] 
> **accessToken** 는 drivermanager 클래스에서 getconnection () 메서드의 Properties 매개 변수를 사용 하 여 설정할 수 있습니다. 연결 문자열에서 사용할 수 없습니다.

아래 예제에는 액세스 토큰 기반 인증을 사용 하 여 Azure SQL Database/데이터 웨어하우스에 연결 하는 간단한 Java 응용 프로그램이 포함 되어 있습니다. 예제를 빌드하고 실행 하기 전에 다음 단계를 수행 합니다.
1.  서비스에 대 한 Azure Active Directory에서 응용 프로그램 계정을 만듭니다.
    1. Azure Portal에 로그인합니다.
    2. 왼쪽 탐색 모음에서 Azure Active Directory를 클릭 합니다.
    3. "앱 등록" 탭을 클릭 합니다.
    4. 서랍에서 "새 응용 프로그램 등록"을 클릭 합니다.
    5. 응용 프로그램에 대 한 친숙 한 이름으로 mytokentest를 입력 하 고 "웹 앱/a p i"를 선택 합니다.
    6. 로그온 URL이 필요 하지 않습니다. 아무 것도 제공할: "https://mytokentest" 입니다.
    7. 맨 아래에서 "만들기"를 클릭 합니다.
    9. 계속 Azure Portal에 있는 동안 응용 프로그램의 "설정" 탭을 클릭 하 고 "속성" 탭을 엽니다.
    10. "응용 프로그램 ID" (즉, Client ID) 값을 찾아 따로 복사 합니다. 나중에 응용 프로그램을 구성할 때 필요 합니다 (예: 1846943b-ad04-4808-aa13-4702d908b5c1). 다음 스냅숏을 참조 하세요.
    11. "키" 섹션에서 이름 필드를 입력 하 고 키의 기간을 선택한 다음 구성을 저장 하 여 키를 만듭니다. 값 필드는 비워 둡니다. 저장 한 후에는 값 필드를 자동으로 채워야 하므로 생성 된 값을 복사 합니다. 클라이언트 비밀입니다.
    12. 왼쪽 패널에서 Azure Active Directory를 클릭 합니다. "앱 등록"에서 "끝점 종료" 탭을 찾습니다. "OATH 2.0 토큰 끝점"에서 URL을 복사 합니다 .이 url은 STS URL입니다.
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Azure SQL Server의 사용자 데이터베이스에 Azure Active Directory 관리자로 로그인 하 고 T-sql 명령을 사용 하 여 응용 프로그램 보안 주체에 대해 포함 된 데이터베이스 사용자를 프로 비전 합니다. 자세한 내용은 Azure Active Directory 관리자 및 포함 된 데이터베이스 사용자를 만드는 방법에 대 한 자세한 내용은 [Azure Active Directory 인증을 사용 하 여 SQL Database에 연결 또는 SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) 를 참조 하세요.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  클라이언트 컴퓨터 (이 예제를 실행 하려는 경우)에서 [activedirectory](https://github.com/AzureAD/azure-activedirectory-library-for-java) 라이브러리 및 해당 종속성을 다운로드 하 여 java 빌드 경로에 포함 합니다. Activedirectory-java는이 특정 예제를 실행 하는 데만 필요 합니다. 이 예제에서는이 라이브러리의 Api를 사용 하 여 Azure AAD에서 액세스 토큰을 검색 합니다. 액세스 토큰이 이미 있는 경우이 단계를 건너뛸 수 있습니다. 또한 액세스 토큰을 검색 하는 예제에서 섹션을 제거 해야 합니다.

다음 예에서는 STS URL, 클라이언트 ID, 클라이언트 암호, 서버 및 데이터베이스 이름을 값으로 바꿉니다.

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

연결에 성공 하면 다음 메시지가 출력으로 표시 되어야 합니다.

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
