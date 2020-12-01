---
title: SqlClient에서 Azure Active Directory 인증 사용
description: 지원되는 Azure Active Directory 인증 모드를 사용하여 SqlClient로 Azure SQL 데이터 원본에 연결하는 방법을 설명합니다.
ms.date: 11/20/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: karinazhou
ms.author: v-jizho2
ms.reviewer: ''
ms.openlocfilehash: 0f8aaffc1f87b33a5c685b55d724fe96c44258af
ms.sourcegitcommit: ece151df14dc2610d96cd0d40b370a4653796d74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96297950"
---
# <a name="using-azure-active-directory-authentication-with-sqlclient"></a>SqlClient에서 Azure Active Directory 인증 사용

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

이 문서에서는 SqlClient로 .NET 애플리케이션에서 Azure AD(Azure Active Directory) 인증을 사용하여 Azure SQL 데이터 원본에 연결하는 방법을 설명합니다.

Azure AD 인증은 Azure AD의 ID를 사용하여 Azure SQL Database, Azure SQL Managed Instance 및 Azure Synapse Analytics와 같은 Azure SQL 데이터 원본에 액세스합니다. **Microsoft.Data.SqlClient** 네임스페이스를 사용하면 클라이언트 애플리케이션이 Azure SQL Database에 연결할 때 다른 인증 모드에서 Azure AD 자격 증명을 지정할 수 있습니다. 

연결 문자열에서 `Authentication` 연결 속성을 설정하면 클라이언트에서는 제공된 값에 따라 기본 Azure AD 인증 모드를 선택할 수 있습니다.

- 초기 **Microsoft.Data.SqlClient** 버전은 .NET Framework, .NET Core 및 .NET Standard에 대해 `Active Directory Password`를 지원합니다. 또한, 해당 버전은 .NET Framework에 대해 `Active Directory Integrated` 인증 및 `Active Directory Interactive` 인증도 지원합니다. 

- **Microsoft.Data.SqlClient** 2.0.0부터 `Active Directory Integrated` 인증 및 `Active Directory Interactive` 인증에 대한 지원이 .NET Framework, .NET Core 및 .NET Standard에서 확장되었습니다. 

  새 `Active Directory Service Principal` 인증 모드도 SqlClient 2.0.0에 추가되었습니다. 인증을 수행하기 위해 서비스 주체 ID의 클라이언트 ID와 암호를 사용합니다. 

- **Microsoft.Data.SqlClient** 2.1.0에는 `Active Directory Device Code Flow` 및 `Active Directory Managed Identity`(`Active Directory MSI`라고도 함)를 포함하여 더 많은 인증 모드가 추가되었습니다. 이러한 새로운 모드를 통해 애플리케이션은 서버에 연결하기 위한 액세스 토큰을 획득할 수 있습니다. 

다음 섹션에서 설명하는 것 이외의 Azure AD 인증에 대한 자세한 내용은 [ Azure Active Directory 인증을 사용하여 SQL Database에 연결 ](/azure/azure-sql/database/authentication-aad-overview)을 참조하세요.


## <a name="setting-azure-active-directory-authentication"></a>Setting Azure Active Directory 인증

애플리케이션이 Azure AD 인증을 사용하여 Azure SQL 데이터 원본에 연결하는 경우 유효한 인증 모드를 제공해야 합니다. 다음 표에는 지원되는 인증 모드가 나열되어 있습니다. 애플리케이션은 연결 문자열에서 `Authentication` 연결 속성을 사용하여 모드를 지정합니다.

| 값 | Description  | 프레임워크    | Microsoft.Data.SqlClient 버전 |
|:--|:--|:--|:--:|
| Active Directory 암호 | 사용자 이름과 암호를 사용하여 Azure AD ID로 인증 | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+  | 1.0+|
| Active Directory 통합 |통합 인증을 사용하여 Azure AD ID로 인증 | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+ | 2.0.0+<sup>1</sup> |
| Active Directory 대화형 | 대화형 인증을 사용하여 Azure AD ID로 인증 | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+ | 2.0.0+<sup>1</sup> |
| Active Directory 서비스 주체 | 클라이언트 ID 및 서비스 주체 ID의 암호를 사용하여 Azure AD ID로 인증 | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+ | 2.0.0+ |
| Active Directory 디바이스 코드 흐름 | 디바이스 코드 흐름 모드를 사용하여 Azure AD ID로 인증 | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+ | 2.1.0+ |
| Active Directory 관리 ID, <br>Active Directory MSI | 시스템 할당 또는 사용자 할당 관리 ID를 사용하여 Azure AD ID로 인증 | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+ | 2.1.0+ |

<sup>1</sup> **Microsoft.Data.SqlClient** 2.0.0 이전에는 `Active Directory Integrated` 및 `Active Directory Interactive` 인증이 .NET Framework 4.6 이상에서만 지원되었습니다. 


## <a name="using-active-directory-password-authentication"></a>Active Directory 암호 인증 사용

`Active Directory Password` 인증 모드는 네이티브 또는 페더레이션된 Azure AD 사용자에 대해 Azure AD를 사용하여 Azure 데이터 원본에 대한 인증을 지원합니다. 이 모드를 사용하는 경우 연결 문자열에 사용자 자격 증명을 제공해야 합니다. 다음 예제에서는 `Active Directory Password` 인증을 사용하는 방법을 보여줍니다.

```c#
// Use your own server, database, user ID, and password.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Password; Database=testdb; User Id=user@domain.com; Password=**_";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-integrated-authentication"></a>Active Directory 통합 인증 사용

`Active Directory Integrated` 인증 모드를 사용하려면 클라우드에서 온-프레미스 Active Directory 인스턴스를 Azure AD와 페더레이션해야 합니다. 예를 들어 AD FS(Active Directory Federation Services)를 사용하여 페더레이션을 수행할 수 있습니다.

도메인에 가입된 컴퓨터에 로그인하면 이 모드에서 자격 증명을 입력하라는 메시지가 표시되지 않고 Azure SQL 데이터 원본에 액세스할 수 있습니다. .NET Framework 애플리케이션의 연결 문자열에 사용자 이름과 암호를 지정할 수 없습니다. .NET Core 및 .NET Standard 애플리케이션의 연결 문자열에서 사용자 이름은 선택 사항입니다. 이 모드에서는 SqlConnection의 `Credential` 속성을 설정할 수 없습니다. 

다음 코드 조각은 `Active Directory Integrated` 인증이 사용중인 경우의 예제입니다.

```c#
// Use your own server and database.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Integrated; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

// User ID is optional for .NET Core and .NET Standard.
string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory Integrated; Database=testdb; User Id=user@domain.com";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="using-active-directory-interactive-authentication"></a>Active Directory 대화형 인증 사용

`Active Directory Interactive` 인증은 Azure SQL 데이터 원본에 연결하기 위한 다단계 인증 기술을 지원합니다. 연결 문자열에 이 인증 모드를 제공하면 Azure 인증 화면이 나타나고 사용자에게 유효한 자격 증명을 입력하도록 요청합니다. 연결 문자열에 암호를 지정할 수 없습니다. 

이 모드에서는 SqlConnection의 `Credential` 속성을 설정할 수 없습니다. _ *Microsoft.Data.SqlClient** 2.0.0 이상에서는 대화형 모드에 있을 때 연결 문자열에 사용자 이름이 허용됩니다. 

다음 예제에서는 `Active Directory Interactive` 인증을 사용하는 방법을 보여줍니다.

```c#
// Use your own server, database, and user ID.
// User ID is optional.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Interactive; Database=testdb; User Id=user@domain.com";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

// User ID is not provided.
string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory Interactive; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="using-active-directory-service-principal-authentication"></a>Azure Active Directory 서비스 주체 인증 사용

`Active Directory Service Principal` 인증 모드에서 클라이언트 애플리케이션은 서비스 주체 ID의 클라이언트 ID와 암호를 제공하여 Azure SQL 데이터 원본에 연결할 수 있습니다. 서비스 주체 인증에는 다음이 포함됩니다.
1. 비밀로 앱 등록 설정.
1. Azure SQL Database 인스턴스의 앱에 대한 권한 부여.
1. 올바른 자격 증명으로 연결. 

다음 예제에서는 `Active Directory Service Principal` 인증을 사용하는 방법을 보여줍니다.

```c#
// Use your own server, database, app ID, and secret.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Service Principal; Database=testdb; User Id=AppId; Password=secret";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-device-code-flow-authentication"></a>Active Directory 디바이스 코드 흐름 인증 사용

.NET(MSAL.NET)용 [Microsoft 인증 라이브러리](/azure/active-directory/develop/msal-overview)를 사용하면 `Active Directory Device Code Flow` 인증을 통해 클라이언트 애플리케이션이 대화형 웹 브라우저가 없는 디바이스 및 운영 체제에서 Azure SQL 데이터 원본에 연결할 수 있습니다. 다른 디바이스에서 대화형 인증이 수행됩니다. 디바이스 코드 흐름 인증에 대한 자세한 내용은 [OAuth 2.0 디바이스 코드 흐름](/azure/active-directory/develop/v2-oauth2-device-code)을 참조하세요. 

이 모드를 사용 중이면 `SqlConnection`의 `Credential` 속성을 설정할 수 없습니다. 또한 연결 문자열에 사용자 이름과 암호를 지정하면 안 됩니다. 

다음 코드 조각은 `Active Directory Device Code Flow` 인증을 사용하는 예제입니다.

```c#
// Use your own server and database.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Device Code Flow; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-managed-identity-authentication"></a>Active Directory 관리 ID 인증 사용

Azure 리소스에 대한 *관리 ID* 는 이전에 MSI(관리 서비스 ID)로 알려진 서비스에 대한 새 이름입니다. 클라이언트 애플리케이션이 Azure 리소스를 사용하여 Azure AD 인증을 지원하는 Azure 서비스에 액세스하는 경우 관리 ID를 사용하여 Azure AD에서 Azure 리소스에 대한 ID를 제공하여 인증할 수 있습니다. 그런 다음 해당 ID를 사용하여 액세스 토큰을 얻을 수 있습니다. 이렇게 하면 자격 증명과 비밀을 관리할 필요가 없습니다. 

두 가지 종류의 관리 ID가 있습니다. 

- _시스템 할당 관리 ID_ 는 Azure AD의 서비스 인스턴스에서 생성됩니다. 해당 서비스 인스턴스의 수명 주기와 관련이 있습니다. 
- _사용자 할당 관리 ID_ 는 독립 실행형 Azure 리소스로 생성됩니다. 하나 이상의 Azure 서비스 인스턴스에 할당할 수 있습니다. 

관리 ID에 대한 자세한 내용은 [Azure 리소스의 관리 ID 정보](/azure/active-directory/managed-identities-azure-resources/overview)를 참조하세요.

**Microsoft.Data.SqlClient** 2.1.0부터 드라이버는 관리 ID를 통해 액세스 토큰을 획득하여 Azure SQL Database, Azure Synapse Analytics 및 Azure SQL Managed Instance에 대한 인증을 지원합니다. 이 인증을 사용하려면 연결 문자열에 `Active Directory Managed Identity` 또는 `Active Directory MSI`를 지정하고 암호는 필요하지 않습니다. 

이 모드에서도 `SqlConnection`의 `Credential` 속성을 설정할 수 없습니다. 사용자가 할당한 관리 ID의 경우 사용자 이름을 제공해야 합니다. 

다음 예제는 시스템 할당 관리 ID로 `Active Directory Managed Identity` 인증을 사용하는 방법을 보여줍니다.

```c#
// For system-assigned managed identity
// Use your own server and database.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory MSI; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```

다음 예제는 사용자 지정 관리 ID를 사용한 `Active Directory Managed Identity` 인증을 보여줍니다.

```c#
// For user-assigned managed identity
// Use your own server, database, and user ID.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; User Id=ObjectIdOfManagedIdentity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory MSI; User Id=ObjectIdOfManagedIdentity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="customizing-active-directory-authentication"></a>Active Directory 인증 사용자 지정

드라이버에 내장된 Active Directory 인증을 사용하는 것 외에도, **Microsoft.Data.SqlClient** 2.1.0 이상 버전에서는 애플리케이션에 Active Directory 인증을 사용자 지정하는 옵션을 제공합니다. 사용자 지정은 [`SqlAuthenticationProvider`](/dotnet/api/system.data.sqlclient.sqlauthenticationprovider) 추상 클래스에서 파생된 `ActiveDirectoryAuthenticationProvider` 클래스를 기반으로 합니다. 

Active Directory 인증 중에 클라이언트 애플리케이션은 다음 중 하나를 통해 자체 `ActiveDirectoryAuthencationProvider` 클래스를 정의할 수 있습니다.

- 사용자 지정된 콜백 메서드 사용.
- 액세스 토큰을 가져오기 위해 SqlClient 드라이버를 통해 MSAL 라이브러리에 애플리케이션 클라이언트 ID를 전달합니다.

다음 예제는 `Active Directory Device Code Flow` 인증이 사용 중일 때 사용자 지정 콜백을 사용하는 방법을 표시합니다. 

[!code-csharp [AADAuthenticationCustomDeviceFlowCallback#1](~/../sqlclient/doc/samples/AADAuthenticationCustomDeviceFlowCallback.cs#1)]

사용자 지정된 `ActiveDirectoryAuthenticationProvider` 클래스를 사용하면 지원되는 Active Directory 인증 모드가 사용 중일 때 사용자 정의 애플리케이션 클라이언트 ID를 SqlClient에 전달할 수 있습니다. 지원되는 Active Directory 인증 모드에는 `Active Directory Password`, `Active Directory Integrated`, `Active Directory Interactive`, `Active Directory Service Principal` 및 `Active Directory Device Code Flow`이 있습니다.

애플리케이션 클라이언트 ID는 `SqlAuthenticationProviderConfigurationSection` 또는 `SqlClientAuthenticationProviderConfigurationSection`을 통해 구성할 수도 있습니다. `applicationClientId` 구성 속성은 .NET Framework 4.6 이상 및 .NET Core 2.1 이상에 적용됩니다.

다음 코드 조각은 `Active Directory Interactive` 인증이 사용 중일 때 사용자 정의 애플리케이션 클라이언트 ID와 함께 사용자 지정된 `ActiveDirectoryAuthenticationProvider` 클래스를 사용하는 예제입니다.

[!code-csharp [ApplicationClientIdAzureAuthenticationProvider#1](~/../sqlclient/doc/samples/ApplicationClientIdAzureAuthenticationProvider.cs#1)]

다음 예제는 구성 섹션을 통해 애플리케이션 클라이언트 ID를 설정하는 방법을 보여줍니다.

```xml
<configuration>
  <configSections>
    <section name="SqlClientAuthenticationProviders"
             type="Microsoft.Data.SqlClient.SqlClientAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
  </configSections>
  <SqlClientAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>

<!--or-->

<configuration>
  <configSections>
    <section name="SqlAuthenticationProviders"
             type="Microsoft.Data.SqlClient.SqlAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
  </configSections>
  <SqlAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>
```

## <a name="support-for-a-custom-sql-authentication-provider"></a>사용자 지정 SQL 인증 공급자 지원

더 많은 유연성이 주어지면 클라이언트 애플리케이션은 `ActiveDirectoryAuthenticationProvider` 클래스를 사용하는 대신 Active Directory 인증에 자체 공급자를 사용할 수도 있습니다. 사용자 지정 인증 제공자는 대체 메서드가 있는 `SqlAuthenticationProvider`의 하위 클래스여야 합니다. 

다음 예제는 `Active Directory Device Code Flow` 인증에 새 인증 제공자를 사용하는 방법을 보여줍니다.

[!code-csharp [CustomDeviceCodeFlowAzureAuthenticationProvider#1](~/../sqlclient/doc/samples/CustomDeviceCodeFlowAzureAuthenticationProvider.cs#1)]

`Active Directory Interactive` 인증 환경을 개선하는 것 외에도, **Microsoft.Data.SqlClient** 2.1.0 이상 버전에서는 대화형 인증 및 디바이스 코드 흐름 인증을 사용자 지정하기 위해 클라이언트 애플리케이션에 대해 다음 API를 제공합니다.

```c#
public class ActiveDirectoryAuthenticationProvider
{
    // For .NET Framework targeted applications only
    // Sets a reference to the current System.Windows.Forms.IWin32Window that triggers the browser to be shown. 
    // Used to center the browser pop-up onto this window.
    public void SetIWin32WindowFunc(Func<IWin32Window> iWin32WindowFunc);

    // For .NET Standard targeted applications only
    // Sets a reference to the ViewController (if using Xamarin.iOS), Activity (if using Xamarin.Android) IWin32Window, or IntPtr (if using .NET Framework). 
    // Used for invoking the browser for Active Directory Interactive authentication.
    public void SetParentActivityOrWindowFunc(Func<object> parentActivityOrWindowFunc);

    // For .NET Framework, .NET Core, and .NET Standard targeted applications
    // Sets a callback method that's invoked with a custom web UI instance that will let the user sign in with Azure AD, present consent if needed, and get back the authorization code. 
    // Applicable when working with Active Directory Interactive authentication.
    public void SetAcquireAuthorizationCodeAsyncCallback(Func<Uri, Uri, CancellationToken, Task<Uri>> acquireAuthorizationCodeAsyncCallback);

    // For .NET Framework, .NET Core, and .NET Standard targeted applications
    // Clears cached user tokens from the token provider.
    public static void ClearUserTokenCache();
}
```


## <a name="see-also"></a>참고 항목
- [Azure Active Directory의 애플리케이션 및 서비스 주체 개체](/azure/active-directory/develop/app-objects-and-service-principals)
- [인증 흐름](/azure/active-directory/develop/msal-authentication-flows)
