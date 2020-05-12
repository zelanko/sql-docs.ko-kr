---
title: ODBC 드라이버에서 Azure Active Directory 사용
description: Microsoft ODBC Driver for SQL Server를 사용하면 ODBC 애플리케이션에서 Azure Active Directory를 사용하여 Azure SQL Database 인스턴스에 연결할 수 있습니다.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b829cb837eafb1a47283d50ede3ee789471e5f7f
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886310"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>ODBC 드라이버에서 Azure Active Directory 사용
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>목적

Microsoft ODBC Driver for SQL Server 버전 13.1 이상에서는 ODBC 애플리케이션이 Active Directory의 페더레이션된 ID로 사용자 이름/암호, Azure Active Directory 액세스 토큰, Azure Active Directory 관리 서비스 ID 또는 Windows 통합 인증(_Windows 드라이버만 해당_)을 사용하여 Azure SQL Database 인스턴스에 연결할 수 있습니다. ODBC 드라이버 버전 13.1의 경우 Azure Active Directory 액세스 토큰 인증은 _Windows 전용_입니다. ODBC 드라이버 버전 17 이상에서는 모든 플랫폼(Windows, Linux 및 macOS)에서 이 인증을 지원합니다. 로그인 ID를 사용하는 새로운 Azure Active Directory 대화형 인증은 Windows용 ODBC 드라이버 버전 17.1에서 도입되었습니다. 시스템 할당 ID와 사용자 할당 ID 모두에 대해 새로운 Azure Active Directory 관리 서비스 ID 인증 방법이 ODBC 드라이버 버전 17.3.1.1에서 추가되었습니다. 이러한 기능은 모두 새 DSN 및 연결 문자열 키워드를 사용하고 연결 특성을 사용하여 수행됩니다.

> [!NOTE]
> Linux 및 macOS의 ODBC 드라이버는 Azure Active Directory에 대해 직접 Azure Active Directory 인증만을 지원합니다. Linux 또는 macOS 클라이언트에서 Azure Active Directory 사용자 이름/암호 인증을 사용하고 Active Directory 구성에서 Active Directory Federation Services 엔드포인트에 대해 클라이언트를 인증해야 하는 경우 인증이 실패할 수 있습니다.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>새로운 및/또는 수정된 DSN 및 연결 문자열 키워드

`Authentication` 키워드를 사용하여 DSN 또는 연결 문자열과 연결하여 인증 모드를 제어할 수 있습니다. 제공된 경우, 연결 문자열에 설정된 값이 DSN에서이를 재정의합니다. `Authentication` 설정의 _사전 특성 값_은 연결 문자열 및 DSN 값에서 계산된 값입니다.

|속성|값|기본값|Description|
|-|-|-|-|
|`Authentication`|(설정 안 됨), (빈 문자열), `SqlPassword`, `ActiveDirectoryPassword`, `ActiveDirectoryIntegrated`, `ActiveDirectoryInteractive`, `ActiveDirectoryMsi` |(설정 안 됨)|인증 모드를 제어합니다.<table><tr><th>값<th>Description<tr><td>(설정 안 됨)<td>다른 키워드에 의해 결정되는 인증 모드입니다(기존 레거시 연결 옵션).<tr><td>(빈 문자열)<td>(연결 문자열만 해당) DSN에 설정된 `Authentication` 값을 재정의하고 설정 해제합니다.<tr><td>`SqlPassword`<td>사용자 이름 및 암호를 사용하여 SQL Server 인스턴스에 직접 인증합니다.<tr><td>`ActiveDirectoryPassword`<td>Azure Active Directory ID로 사용자 이름 및 암호를 사용하여 인증합니다.<tr><td>`ActiveDirectoryIntegrated`<td>_Windows 드라이버만 해당_. 통합 인증을 사용하여 Azure Active Directory ID로 인증합니다.<tr><td>`ActiveDirectoryInteractive`<td>_Windows 드라이버만 해당_. 대화형 인증을 사용하여 Azure Active Directory ID로 인증합니다.<tr><td>`ActiveDirectoryMsi`<td>관리 서비스 ID 인증을 사용하여 Azure Active Directory ID로 인증합니다. 사용자 할당 ID의 경우 UID를 사용자 ID의 개체 ID로 설정합니다.</table>|
|`Encrypt`|(설정 안 됨), `Yes`, `No`|(설명 참조)|연결의 암호화를 제어합니다. `Authentication` 설정의 사전 특성 값이 DSN 또는 연결 문자열에서 _none_이 아닌 경우 기본값은 `Yes`입니다. 그렇지 않은 경우 기본값은 `No`입니다. 특성 `SQL_COPT_SS_AUTHENTICATION` `Authentication`의 사전 특성 값을 재정의하는 경우 DSN 또는 연결 문자열 또는 연결 특성에서 암호화 값을 명시적으로 설정합니다. DSN 또는 연결 문자열에서 값이 `Yes`로 설정된 경우에는 사전 특성 값의 암호화가 `Yes`입니다.|

## <a name="new-andor-modified-connection-attributes"></a>새로운 및/또는 수정된 연결 특성

다음 연결 전 연결 특성이 Azure Active Directory 인증을 지원하도록 도입 또는 수정되었습니다. 연결 특성에 해당하는 연결 문자열 또는 DSN 키워드가 있고 설정된 경우 연결 특성이 우선적으로 적용됩니다.

|attribute|Type|값|기본값|Description|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_AD_MSI`, `SQL_AU_RESET`|(설정 안 됨)|위의 `Authentication` 키워드에 대한 설명을 참조하세요. `SQL_AU_NONE`는 DSN 및/또는 연결 문자열의 설정된 `Authentication` 값을 명시적으로 재정의하기 위해 제공되며, `SQL_AU_RESET`는 설정된 경우 특성을 설정 해제하여 DSN 또는 연결 문자열 값이 우선적으로 적용될 수 있도록 합니다.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|`ACCESSTOKEN` 또는 NULL에 대한 포인터|NULL|Null이 아닌 경우 사용할 AzureAD 액세스 토큰을 지정합니다. 액세스 토큰을 지정하는 것은 오류이며 `UID`, `PWD`, `Trusted_Connection` 또는 `Authentication` 연결 문자열 키워드 또는 이와 동등한 특성을 지정하는 것도 오류입니다. <br> **참고:** ODBC 드라이버 버전 13.1은 _Windows_에서만 이를 지원합니다.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(설명 참조)|연결의 암호화를 제어합니다. `SQL_EN_OFF`는 암호화를 사용하지 않도록 설정하고, `SQL_EN_ON`는 사용하도록 설정합니다. `Authentication` 설정의 사전 특성 값이 _none_이거나 `SQL_COPT_SS_ACCESS_TOKEN`이 설정되어 있고 DSN 또는 연결 문자열에 `Encrypt`가 지정되지 않은 경우 기본값은 `SQL_EN_ON`입니다. 그렇지 않은 경우 기본값은 `SQL_EN_OFF`입니다. 연결 특성 `SQL_COPT_SS_AUTHENTICATION`이 _none_으로 설정된 경우 DSN 또는 연결 문자열에 `Encrypt`가 지정되지 않았으면 명시적으로 `SQL_COPT_SS_ENCRYPT`를 원하는 값으로 설정합니다. 이 특성의 유효한 값은 [연결에 암호화를 사용할지 여부](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)를 제어합니다.|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|ODBC 연결을 통해서는 AAD 보안 주체에 대한 암호 변경을 수행할 수 없으므로 Azure Active Directory에서는 지원되지 않습니다. <br><br>SQL Server 인증의 암호 만료가 SQL Server 2005에 도입되었습니다. 클라이언트에서 연결에 대한 기존 암호와 새 암호를 모두 제공할 수 있도록 `SQL_COPT_SS_OLDPWD` 특성이 추가되었습니다. 이 속성을 설정하면 변경된 “이전 암호”가 연결 문자열에 포함되기 때문에 공급자가 첫 번째 연결 또는 이후 연결에 연결 풀을 사용하지 않습니다.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_사용되지 않습니다_. 대신 `SQL_AU_AD_INTEGRATED`로 설정된 `SQL_COPT_SS_AUTHENTICATION`을 사용합니다. <br><br>서버 로그인에 대한 액세스 유효성 검사에 Windows 인증(Linux 및 macOS의 Kerberos)을 강제로 사용합니다. Windows 인증을 사용하는 경우 드라이버는 `SQLConnect`, `SQLDriverConnect` 또는 `SQLBrowseConnect` 처리의 일부로 제공된 사용자 ID 및 암호 값을 무시합니다.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Azure Active Directory에 대한 UI 추가(Windows 드라이버만 해당)

Azure AD를 통한 인증을 사용하는 데 필요한 추가 옵션으로 드라이버의 DSN 설정 및 연결 UI가 향상되었습니다.

### <a name="creating-and-editing-dsns-in-the-ui"></a>UI에서 DSN 만들기 및 편집

드라이버의 설치 UI를 사용하여 기존 DSN을 만들거나 편집할 때 새로운 Azure AD 인증 옵션을 사용할 수 있습니다.

`Authentication=ActiveDirectoryIntegrated` SQL Azure에 대한 Azure Active Directory 통합 인증

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword` SQL Azure에 대한 Azure Active Directory 사용자 이름/암호 인증

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` SQL Azure에 대한 Azure Active Directory 대화형 인증 지원

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` SQL Server에 대한 사용자 이름/암호 인증(Azure 또는 기타)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` Windows 레거시 SSPI 통합 인증

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

5가지 옵션은 `Trusted_Connection=Yes`(기존 레거시 Windows SSPI 전용 통합 인증) 및 `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`, `ActiveDirectoryPassword` 및 `ActiveDirectoryInteractive`입니다.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect 프롬프트(Windows 드라이버만 해당)

SQLDriverConnect에서 연결을 완료하는 데 필요한 정보를 요청할 때 표시되는 프롬프트 대화 상자에는 Azure AD 인증을 위한 세 가지 새로운 옵션이 포함되어 있습니다.

![ServerLogin.png](windows/ServerLogin.png)

이러한 옵션은 위의 DSN 설정 UI에서 사용할 수 있는 것과 동일한 5가지 옵션에 해당합니다.

### <a name="example-connection-strings"></a>연결 문자열 예
1. SQL Server 인증 - 레거시 구문. 서버 인증서의 유효성을 검사하지 않고 암호화는 서버에서 적용하는 경우에만 사용됩니다. 사용자 이름/암호가 연결 문자열에 전달됩니다.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 인증 - 새 구문. 클라이언트는 암호화를 요청하고(`Encrypt` 기본값은 `true`) 암호화 설정에 관계없이 서버 인증서의 유효성을 검사합니다(`TrustServerCertificate`를 `true`로 설정하지 않은 경우). 사용자 이름/암호가 연결 문자열에 전달됩니다.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. SSPI를 사용하는 Windows 통합 인증(Linux 및 macOS의 Kerberos)(SQL Server 또는 SQL IaaS로) - 현재 구문. 암호화를 사용하지 않는 한 서버 인증서의 유효성이 검사되지 않습니다. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Windows 드라이버만 해당_.) SSPI를 사용하는 Windows 통합 인증(대상 데이터베이스가 SQL Server 또는 SQL IaaS에 있는 경우) - 새 구문. 클라이언트는 암호화를 요청하고(`Encrypt` 기본값은 `true`) 암호화 설정에 관계없이 서버 인증서의 유효성을 검사합니다(`TrustServerCertificate`를 `true`로 설정하지 않은 경우). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD 사용자 이름/암호 인증(대상 데이터베이스가 Azure SQL DB에 있는 경우). 암호화 설정에 관계없이 서버 인증서의 유효성을 검사합니다(`TrustServerCertificate`를 `true`로 설정하지 않은 경우). 사용자 이름/암호가 연결 문자열에 전달됩니다. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Windows 드라이버만 해당_.) Windows 계정 자격 증명을 AAD 발급 액세스 토큰으로 교환하는 ADAL을 사용하는 Windows 통합 인증(대상 데이터베이스가 Azure SQL Database에 있는 것으로 가정). 암호화 설정에 관계없이 서버 인증서의 유효성을 검사합니다(`TrustServerCertificate`를 `true`로 설정하지 않은 경우). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Windows 드라이버만 해당_.) AAD 대화형 인증은 Azure Multi-factor Authentication 기술을 사용하여 연결을 설정합니다. 이 모드에서 로그인 ID를 제공하면 Azure 인증 대화 상자가 트리거되고 사용자가 암호를 입력하여 연결을 완료할 수 있습니다. 사용자 이름은 연결 문자열에서 전달됩니다.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. AAD 관리 서비스 ID 인증은 인증에 시스템 할당 또는 사용자 할당 ID를 사용하여 연결을 설정합니다. 사용자 할당 ID의 경우 UID를 사용자 ID의 개체 ID로 설정합니다.<br>
시스템 할당 ID의 경우<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
개체 ID가 myObjectId와 동일한 사용자 할당 ID의 경우<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE]
>- Active Directory 옵션을 17.4.2 이전 버전의 Windows ODBC 드라이버에서 사용하는 경우 [SQL Server용 Active Directory 인증 라이브러리](https://go.microsoft.com/fwlink/?LinkID=513072)를 설치했는지 확인합니다.****** Linux 및 macOS 드라이버를 사용하는 경우 `libcurl`가 설치되어 있는지 확인합니다. 드라이버 버전 17.2 이상에서는 다른 인증 방법 또는 ODBC 작업에 필요하지 않으므로 이는 명시적 종속성이 아닙니다.
>- SQL Server 계정 사용자 이름 및 암호를 사용하여 연결하려면 이제 새 `SqlPassword` 옵션을 사용할 수 있습니다. 이 옵션을 통해 보다 안전한 연결 기본값을 사용할 수 있으므로 특히 SQL Azure에서 이 옵션을 사용하는 것이 좋습니다.
>- Azure Active Directory 계정 사용자 이름 및 암호를 사용하여 연결하려면 연결 문자열에 `Authentication=ActiveDirectoryPassword`를 지정하고 사용자 이름 및 암호를 사용하여 `UID` 및 `PWD` 키워드를 각각 지정합니다.
>- Windows 통합 인증 또는 Active Directory 통합 인증(Windows 드라이버만 해당)을 사용하여 연결하려면 연결 문자열에 `Authentication=ActiveDirectoryIntegrated`를 지정합니다. 드라이버에서 자동으로 올바른 인증 모드를 선택합니다. `UID` 및 `PWD`는 지정하지 않아야 합니다.
>- Active Directory 대화형 인증(Windows 드라이버만 해당)을 사용하여 연결하려면 `UID`를 지정해야 합니다.

## <a name="authenticating-with-an-access-token"></a>액세스 토큰을 사용하여 인증

`SQL_COPT_SS_ACCESS_TOKEN` 사전 연결 특성을 사용하면 인증을 위해 사용자 이름 및 암호 대신 Azure AD에서 얻은 액세스 토큰을 사용할 수 있으며, 드라이버에 의한 액세스 토큰 협상 및 가져오기를 우회합니다. 액세스 토큰을 사용하려면 `SQL_COPT_SS_ACCESS_TOKEN` 연결 특성을 `ACCESSTOKEN` 구조에 대한 포인터로 설정합니다.

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

`ACCESSTOKEN`은 4바이트 _길이_ 뒤에 액세스 토큰을 구성하는 불투명 데이터의 바이트 _길이_가 이어지는 가변 길이 구조입니다. SQL Server에서 액세스 토큰을 처리하는 방법 때문에 [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) JSON 응답을 통해 가져온 토큰은 ASCII 문자만 포함하는 UCS-2 문자열과 비슷하게 각 바이트 뒤에 0 패딩 바이트가 오도록 확장되어야 합니다. 그러나 토큰은 불투명 값이며 지정된 길이(바이트)는 null 종결자를 포함하지 않아야 합니다. 이 인증 방법은 매우 긴 길이와 형식 제약 조건 때문에 `SQL_COPT_SS_ACCESS_TOKEN` 연결 특성을 통해서만 프로그래밍 방식으로 사용할 수 있습니다. 해당하는 DSN 또는 연결 문자열 키워드가 없습니다. 연결 문자열에 `UID`, `PWD`, `Authentication` 또는 `Trusted_Connection` 키워드가 포함되면 안 됩니다.

> [!NOTE]
> ODBC 드라이버 버전 13.1은 _Windows_에서만 이 인증을 지원합니다.

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 인증 샘플 코드

다음 샘플에서는 연결 키워드와 Azure Active Directory를 사용하여 SQL Server에 연결하는 데 필요한 코드를 보여 줍니다. 애플리케이션 코드 자체를 변경할 필요는 없습니다. 연결 문자열 또는 DSN을 사용하는 경우 인증을 위해 AAD를 사용하는 데 필요한 유일한 수정 사항은 다음과 같습니다.
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);    
    ...
~~~
다음 샘플에서는 액세스 토큰 인증에 Azure Active Directory를 사용하여 SQL Server에 연결하는 데 필요한 코드를 보여 줍니다. 이 경우 액세스 토큰을 처리하고 관련 연결 특성을 설정하기 위해 애플리케이션 코드를 수정해야 합니다.
~~~
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server}"
    SQLCHAR accessToken[] = "eyJ0eXAiOi..."; // In the format extracted from an OAuth JSON response
    ...
    DWORD dataSize = 2 * strlen(accessToken);
    ACCESSTOKEN *pAccToken = malloc(sizeof(ACCESSTOKEN) + dataSize);
    pAccToken->dataSize = dataSize;
    // Expand access token with padding bytes
    for(int i = 0, j = 0; i < dataSize; i += 2, j++) {
        pAccToken->data[i] = accessToken[j];
        pAccToken->data[i+1] = 0;
    }
    ...
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_ACCESS_TOKEN, (SQLPOINTER)pAccToken, SQL_IS_POINTER);
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);        
    ...
    free(pAccToken);
~~~
다음은 Azure Active Directory 대화형 인증에 사용할 수 있는 샘플 연결 문자열입니다. Azure 인증 화면을 사용하여 암호를 입력하므로 PWD 필드는 포함되지 않습니다.
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~
다음은 Azure Active Directory 관리 서비스 ID 인증에 사용할 수 있는 샘플 연결 문자열입니다. 사용자 할당 ID의 경우 UID를 사용자 ID의 개체 ID로 설정합니다.
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="see-also"></a>참고 항목

[Azure AD 인증을 사용하는 Azure SQL DB에 대한 토큰 기반 인증 지원](/archive/blogs/sqlsecurity/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)
