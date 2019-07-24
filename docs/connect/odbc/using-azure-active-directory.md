---
title: ODBC 드라이버에서 Azure Active Directory 사용 | SQL Server에 대 한 Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9e60c376e0bced63241674b82d05700281a06ad3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008491"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>ODBC 드라이버에서 Azure Active Directory 사용
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>용도

13.1 이상 버전을 사용 하는 Microsoft ODBC Driver for SQL Server ODBC 응용 프로그램은 사용자 이름/암호, Azure Active Directory 액세스 토큰, Azure Active 등을 사용 하 여 Azure Active Directory의 페더레이션 id를 사용 하 여 SQL Azure 인스턴스에 연결할 수 있습니다. 디렉터리 관리 서비스 id 또는 Windows 통합 인증 (_windows 드라이버만_해당) ODBC 드라이버 버전 13.1의 경우 Azure Active Directory 액세스 토큰 인증은 _Windows 전용_입니다. ODBC 드라이버 버전 17 이상에서는 모든 플랫폼 (Windows, Linux 및 Mac)에서이 인증을 지원 합니다. 로그인 ID를 사용 하는 새로운 Azure Active Directory 대화형 인증은 Windows 용 ODBC 드라이버 버전 17.1에서 도입 되었습니다. 시스템 할당 id와 사용자 할당 id 모두에 대해 새로운 Azure Active Directory 관리 서비스 id 인증 방법이 ODBC 드라이버 버전 17.3.1.1에 추가 되었습니다. 이러한 모든 기능은 새 DSN 및 연결 문자열 키워드를 사용 하 고 연결 특성을 사용 하 여 수행 됩니다.

> [!NOTE]
> Linux 및 macOS의 ODBC 드라이버는 Active Directory Federation Services을 지원 하지 않습니다. Linux 또는 macOS 클라이언트에서 Azure Active Directory 사용자 이름/암호 인증을 사용 하는 경우 Active Directory 구성에 페더레이션된 서비스가 포함 되 면 인증에 실패할 수 있습니다.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>새 및/또는 수정 된 DSN 및 연결 문자열 키워드

키워드 `Authentication` 는 인증 모드를 제어 하기 위해 DSN 또는 연결 문자열과 연결할 때 사용할 수 있습니다. 제공 된 경우 연결 문자열에 설정 된 값이 DSN에서이를 재정의 합니다. `Authentication` 설정의 _사전 특성 값_ 은 연결 문자열 및 DSN 값에서 계산 된 값입니다.

|속성|값|Default|설명|
|-|-|-|-|
|`Authentication`|(설정 안 함), (빈 문자열) `SqlPassword`, `ActiveDirectoryPassword` `ActiveDirectoryIntegrated`, `ActiveDirectoryInteractive`,,,`ActiveDirectoryMsi` |(설정 안 됨)|인증 모드를 제어 합니다.<table><tr><th>값<th>설명<tr><td>(설정 안 됨)<td>다른 키워드에 의해 결정 되는 인증 모드입니다 (기존 레거시 연결 옵션).<tr><td>(빈 문자열)<td>연결 문자열 이름 DSN에서 설정 된 `Authentication` 값을 재정의 하 고 설정 해제 합니다.<tr><td>`SqlPassword`<td>사용자 이름 및 암호를 사용 하 여 SQL Server 인스턴스에 직접 인증 합니다.<tr><td>`ActiveDirectoryPassword`<td>사용자 이름 및 암호를 사용 하 여 Azure Active Directory id를 사용 하 여 인증 합니다.<tr><td>`ActiveDirectoryIntegrated`<td>_Windows 드라이버만_해당 됩니다. 통합 인증을 사용 하 여 Azure Active Directory id를 사용 하 여 인증 합니다.<tr><td>`ActiveDirectoryInteractive`<td>_Windows 드라이버만_해당 됩니다. 대화형 인증을 사용 하 여 Azure Active Directory id를 사용 하 여 인증 합니다.<tr><td>`ActiveDirectoryMsi`<td>관리 서비스 id 인증을 사용 하 여 Azure Active Directory id로 인증 합니다. 사용자 할당 ID의 경우 UID를 사용자 ID의 개체 ID로 설정합니다.</table>|
|`Encrypt`|(설정 안 됨), `Yes`, `No`|(설명 참조)|연결의 암호화를 제어합니다. DSN 또는 연결 문자열에서 `Authentication` 설정의 사전 특성 값이 _none_ 이 아닌 경우 기본값 `Yes`은입니다. 그렇지 않은 경우 기본값은 `No`입니다. 특성이 `SQL_COPT_SS_AUTHENTICATION` 의`Authentication`사전 특성 값을 재정의 하는 경우 DSN 또는 연결 문자열 또는 연결 특성에 암호화 값을 명시적으로 설정 합니다. 암호화의 사전 특성 값은 DSN 또는 `Yes` 연결 문자열에서 값이로 `Yes` 설정 된 경우입니다.|

## <a name="new-andor-modified-connection-attributes"></a>새 연결 특성 및/또는 수정 된 연결 특성

다음 연결 전 연결 특성이 Azure Active Directory 인증을 지원 하도록 도입 되었거나 수정 되었습니다. 연결 특성에 해당 하는 연결 문자열 또는 DSN 키워드가 있고가 설정 된 경우 connection 특성이 우선적으로 적용 됩니다.

|attribute|형식|값|Default|설명|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_AD_MSI`, `SQL_AU_RESET`|(설정 안 됨)|위의 키워드 설명 `Authentication` 을 참조 하세요. `SQL_AU_NONE`는 dsn 및/또는 연결 문자열 `Authentication` `SQL_AU_RESET` 의 설정 값을 명시적으로 재정의 하기 위해 제공 되며, 특성이 설정 된 경우에는 특성을 설정 하지 않으므로 dsn 또는 연결 문자열 값이 우선 적용 될 수 있습니다.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|또는 NULL `ACCESSTOKEN` 에 대 한 포인터|NULL|Null이 아닌 경우 사용할 AzureAD 액세스 토큰을 지정 합니다. `UID`액세스 토큰과 `PWD` ,,`Authentication` 또는 연결 문자열 키워드 또는 해당 하는 특성을 지정 하는 것은 오류입니다. `Trusted_Connection` <br> **참고:** ODBC 드라이버 버전 13.1은 _Windows_에서만이를 지원 합니다.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(설명 참조)|연결의 암호화를 제어합니다. `SQL_EN_OFF`및 `SQL_EN_ON` 는 각각 암호화를 사용 하지 않도록 설정 하 고 사용 하도록 설정 합니다. `Authentication` 설정의 사전 특성 값이 _none_ `SQL_COPT_SS_ACCESS_TOKEN` 이 아니거나 설정 되어 있고 `Encrypt` DSN 또는 연결 문자열에 지정 되지 않은 경우 기본값 `SQL_EN_ON`은입니다. 그렇지 않은 경우 기본값은 `SQL_EN_OFF`입니다. `SQL_COPT_SS_AUTHENTICATION` 연결 특성이 _없음_으로 설정 된 경우 DSN 또는 연결 문자열에 `SQL_COPT_SS_ENCRYPT` 가 지정 되지 않은 경우 `Encrypt` 을 원하는 값으로 명시적으로 설정 합니다. 이 특성의 유효 값은 [암호화가 연결에 사용 되는지 여부를](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation) 제어 합니다.|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|ODBC 연결을 통해 AAD 보안 주체에 대 한 암호 변경을 수행할 수 없으므로 Azure Active Directory에서는 지원 되지 않습니다. <br><br>SQL Server 인증의 암호 만료가 SQL Server 2005에 도입되었습니다. 클라이언트에서 연결에 대 한 기존 암호와 새 암호를 모두 제공할 수 있도록 특성이추가되었습니다.`SQL_COPT_SS_OLDPWD` 이 속성을 설정하면 변경된 "이전 암호"가 연결 문자열에 포함되기 때문에 공급자가 첫 번째 연결 또는 이후 연결에 연결 풀을 사용하지 않습니다.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_사용 되지 않음_ 대신를로 `SQL_AU_AD_INTEGRATED` 설정합니다.`SQL_COPT_SS_AUTHENTICATION` <br><br>서버 로그인에 대 한 액세스 유효성 검사에 Windows 인증 (Linux 및 macOS의 Kerberos)을 강제로 사용 합니다. Windows 인증을 사용 하는 경우 드라이버는, `SQLConnect` `SQLDriverConnect`또는 `SQLBrowseConnect` 처리의 일부로 제공 된 사용자 식별자 및 암호 값을 무시 합니다.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Azure Active Directory에 대 한 UI 추가 (Windows 드라이버만 해당)

Azure AD에서 인증을 사용 하는 데 필요한 추가 옵션을 사용 하 여 드라이버의 DSN 설정 및 연결 Ui가 향상 되었습니다.

### <a name="creating-and-editing-dsns-in-the-ui"></a>UI에서 Dsn 만들기 및 편집

드라이버의 설치 UI를 사용 하 여 기존 DSN을 만들거나 편집할 때 새로운 Azure AD 인증 옵션을 사용할 수 있습니다.

`Authentication=ActiveDirectoryIntegrated` SQL Azure에 대한 Azure Active Directory 통합 인증

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword`Azure Active Directory에 대 한 사용자 이름/암호 인증 SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` SQL Azure에 대한 Azure Active Directory 대화형 인증 지원

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword`SQL Server에 대 한 사용자 이름/암호 인증 (Azure 또는 그렇지 않은 경우)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes`Windows 레거시 SSPI 통합 인증의 경우

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

5 가지 옵션은 `Trusted_Connection=Yes` (기존 레거시 Windows SSPI 전용 통합 인증) 및 `Authentication=` `ActiveDirectoryPassword` `ActiveDirectoryIntegrated`, `SqlPassword`, 및 `ActiveDirectoryInteractive`에 해당 합니다.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect Prompt (Windows 드라이버만 해당)

SQLDriverConnect에서 연결을 완료 하는 데 필요한 정보를 요청할 때 표시 되는 프롬프트 대화 상자에는 Azure AD 인증을 위한 세 가지 새로운 옵션이 포함 되어 있습니다.

![ServerLogin.png](windows/ServerLogin.png)

이러한 옵션은 위의 DSN setup UI에서 사용할 수 있는 것과 동일한 5 가지 옵션에 해당 합니다.

### <a name="example-connection-strings"></a>연결 문자열 예
1. SQL Server 인증-레거시 구문입니다. 서버 인증서의 유효성을 검사 하지 않고 암호화는 서버에서 적용 하는 경우에만 사용 됩니다. 사용자 이름/암호가 연결 문자열에 전달 됩니다.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 인증-새 구문입니다. 클라이언트는 암호화 설정 ( `Encrypt` 가로 `true`설정 되지 않은 `true`경우 `TrustServerCertificate` )을 요청 하 고 암호화 설정에 관계 없이 서버 인증서의 유효성을 검사 합니다. 사용자 이름/암호가 연결 문자열에 전달 됩니다.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. SSPI를 사용 하는 Windows 통합 인증 (Linux 및 macOS의 Kerberos)-현재 구문 (SQL Server 또는 SQL IaaS) 암호화를 사용 하지 않는 한 서버 인증서의 유효성이 검사 되지 않습니다. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. _Windows 드라이버만_해당 됩니다. SSPI를 사용 하는 Windows 통합 인증 (대상 데이터베이스가 SQL Server 또는 SQL IaaS)-새 구문입니다. 클라이언트는 암호화 설정 ( `Encrypt` 가로 `true`설정 되지 않은 `true`경우 `TrustServerCertificate` )을 요청 하 고 암호화 설정에 관계 없이 서버 인증서의 유효성을 검사 합니다. 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD 사용자 이름/암호 인증 (대상 데이터베이스가 Azure SQL DB에 있는 경우) 가로 `TrustServerCertificate` `true`설정 되지 않은 경우 암호화 설정에 관계 없이 서버 인증서의 유효성을 검사 합니다. 사용자 이름/암호가 연결 문자열에 전달 됩니다. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. _Windows 드라이버만_해당 됩니다. 교환를 사용 하는 Windows 계정 자격 Azure SQL Database 증명을 사용 하는 Windows 통합 인증을 사용 합니다. 가로 `TrustServerCertificate` `true`설정 되지 않은 경우 암호화 설정에 관계 없이 서버 인증서의 유효성을 검사 합니다. 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. _Windows 드라이버만_해당 됩니다. AAD 대화형 인증은 Azure Multi-factor Authentication 기술을 사용 하 여 연결을 설정 합니다. 이 모드에서 로그인 ID를 제공 하면 Windows Azure 인증 대화 상자가 트리거되고 사용자가 암호를 입력 하 여 연결을 완료할 수 있습니다. 사용자 이름은 연결 문자열에 전달 됩니다.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. AAD 관리 서비스 ID 인증은 인증에 시스템 할당 또는 사용자 할당 id를 사용 하 여 연결을 설정 합니다. 사용자 할당 ID의 경우 UID를 사용자 ID의 개체 ID로 설정합니다.<br>
시스템 할당 ID의 경우<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
개체 ID가 myObjectId와 같은 사용자 할당 id의 경우<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE] 
>- 새 Active Directory 옵션을 Windows ODBC 드라이버와 함께 사용 하는 경우 [SQL Server Active Directory 인증 라이브러리](https://go.microsoft.com/fwlink/?LinkID=513072) 를 설치 했는지 확인 합니다. Linux 및 macos 드라이버를 사용 하는 경우 `libcurl` 가 설치 되어 있는지 확인 합니다. 드라이버 버전 17.2 이상에서는 다른 인증 방법이 나 ODBC 작업에 필요 하지 않으므로 명시적 종속성이 아닙니다.
>- SQL Server 계정 사용자 이름 및 암호를 사용 하 여 연결 하려면 이제 새 `SqlPassword` 옵션을 사용할 수 있습니다 .이 옵션을 사용 하면 보다 안전한 연결 기본값을 사용할 수 있으므로 SQL Azure에 특히 권장 됩니다.
>- Azure Active Directory 계정 사용자 이름 및 암호를 사용 하 여 연결 `Authentication=ActiveDirectoryPassword` 하려면 연결 문자열과 `UID` 및 `PWD` 키워드에 각각 사용자 이름과 암호를 지정 합니다.
>- Windows 통합 또는 Active Directory 통합 (windows 드라이버만) 인증을 사용 하 여 연결 하려면 `Authentication=ActiveDirectoryIntegrated` 연결 문자열에를 지정 합니다. 드라이버에서 자동으로 올바른 인증 모드를 선택 합니다. `UID`및 `PWD` 는 지정 하지 않아야 합니다.
>- Active Directory 대화형 (Windows 드라이버만) 인증을 사용 하 여 연결 `UID` 하려면를 지정 해야 합니다.

## <a name="authenticating-with-an-access-token"></a>액세스 토큰을 사용 하 여 인증

`SQL_COPT_SS_ACCESS_TOKEN` 사전 연결 특성을 사용 하면 사용자 이름 및 암호 대신 인증을 위해 Azure AD에서 얻은 액세스 토큰을 사용할 수 있으며, 드라이버에의 한 액세스 토큰 협상 및 가져오기를 무시 합니다. 액세스 토큰을 사용 하려면 연결 특성을 `SQL_COPT_SS_ACCESS_TOKEN` `ACCESSTOKEN` 구조체에 대 한 포인터로 설정 합니다.

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

는 `ACCESSTOKEN` 4 바이트 _길이로_ 이루어진 가변 길이 구조체로, 액세스 토큰을 구성 하는 불투명 데이터의 _길이가_ 바이트입니다. SQL Server에서 액세스 토큰을 처리 하는 방법 때문에 [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) JSON 응답을 통해 가져온 하나를 확장 하 여 각 바이트 뒤에 0 패딩 바이트가 오도록 해야 합니다 .이는 ASCII 문자만 포함 하는 UCS-2 문자열과 유사 합니다. 그러나 토큰은 불투명 값 이며 지정 된 길이 (바이트)는 null 종결자를 포함 하지 않아야 합니다. 이 인증 방법은 유효 길이와 형식 제약 조건 때문에 `SQL_COPT_SS_ACCESS_TOKEN` 연결 특성을 통해서만 프로그래밍 방식으로 사용할 수 있습니다. 해당 하는 DSN 또는 연결 문자열 키워드는 없습니다. `UID`연결 문자열에는 `PWD` `Trusted_Connection` ,, 또는 키워드를 사용할수없습니다.`Authentication`

> [!NOTE]
> ODBC 드라이버 버전 13.1은 _Windows_에서만이 인증을 지원 합니다.

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 인증 샘플 코드

다음 샘플에서는 연결 키워드와 Azure Active Directory를 사용 하 여 SQL Server에 연결 하는 데 필요한 코드를 보여 줍니다. 응용 프로그램 코드 자체를 변경할 필요는 없습니다. 연결 문자열 또는 DSN을 사용 하는 경우 인증을 위해 AAD를 사용 하는 데 필요한 유일한 수정 사항은 다음과 같습니다.
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
다음 샘플에서는 액세스 토큰 인증에 Azure Active Directory를 사용 하 여 SQL Server에 연결 하는 데 필요한 코드를 보여 줍니다. 이 경우 액세스 토큰을 처리 하 고 관련 연결 특성을 설정 하기 위해 응용 프로그램 코드를 수정 해야 합니다.
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
다음은 Azure Active Directory 대화형 인증에 사용할 수 있는 샘플 연결 문자열입니다. Windows Azure 인증 화면을 사용 하 여 암호를 입력 하므로 PWD 필드는 포함 되지 않습니다.
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
[Azure AD 인증을 사용 하 여 Azure SQL DB에 대 한 토큰 기반 인증 지원](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

