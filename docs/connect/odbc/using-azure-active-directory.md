---
title: Azure Active Directory를 사용 하 여 ODBC 드라이버로 | SQL Server 용 Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 98f7e0ac3667bc8546a7bf7ce2d8036341bb2650
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206602"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>ODBC 드라이버에서 Azure Active Directory 사용
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>용도

Azure Active Directory에서 페더레이션된 id를 사용 하 여 사용자 이름/암호, Azure Active Directory 액세스 토큰, 또는 Windows를 사용 하 여 Microsoft ODBC Driver for SQL Server 버전 13.1 이상가 ODBC 응용 프로그램을 SQL Azure 인스턴스에 연결할 수 있습니다. 통합 인증 (_Windows 드라이버만_). ODBC 드라이버 버전 13.1 토큰 인증은 Azure Active Directory 액세스 _만 Windows_합니다. ODBC 드라이버 버전 17 및 위의 모든 플랫폼 (Windows, Linux 및 Mac)에서이 인증을 지원 합니다. 새 Azure Active Directory 대화형 인증 로그인 ID를 사용 하 여 Windows에 대 한 ODBC 드라이버 버전 17.1 도입 되었습니다. 이러한 모든 새 DSN 및 연결 문자열 키워드 및 연결 특성을 사용 하 여 수행 됩니다.

> [!NOTE]
> Linux 및 macOS에서 ODBC 드라이버는 Active Directory Federation Services를 지원 하지 않습니다. Linux에서 Azure Active Directory 사용자 이름/암호 인증을 사용 하는 또는 macOS 클라이언트와 Active Directory 구성에 페더레이션 서비스를 포함 하는 경우 인증이 실패할 수 있습니다.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>새롭거나 수정 된 DSN 및 연결 문자열 키워드

`Authentication` 키워드 수는 DSN 또는 연결 문자열을 사용 하 여 연결할 때 인증 모드를 제어 합니다. 연결 문자열에 설정 된 값 우선 하는 DSN에서 제공 합니다. _사전 값을 특성_ 의 `Authentication` 설정은 연결 문자열 및 DSN 값에서 계산 된 값입니다.

|속성|값|Default|설명|
|-|-|-|-|
|`Authentication`|(설정 안 함) (빈 문자열), `SqlPassword`하십시오 `ActiveDirectoryPassword`, `ActiveDirectoryIntegrated`, `ActiveDirectoryInteractive`|(설정 안 됨)|인증 모드를 제어합니다.<table><tr><th>값<th>설명<tr><td>(설정 안 됨)<td>다른 키워드 (기존 레거시 연결 옵션)에 의해 결정 되는 인증 모드<tr><td>(빈 문자열)<td>연결 문자열: "{0}" 재정의 설정 되지 않은 하 고는 `Authentication` 값이 DSN에서 설정 합니다.<tr><td>`SqlPassword`<td>사용자 이름 및 암호를 사용 하 여 SQL Server 인스턴스로 직접 인증 합니다.<tr><td>`ActiveDirectoryPassword`<td>사용자 이름 및 암호를 사용 하 여 Azure Active Directory id를 사용 하 여 인증 합니다.<tr><td>`ActiveDirectoryIntegrated`<td>_Windows 드라이버만_합니다. 통합된 인증을 사용 하 여 Azure Active Directory id를 사용 하 여 인증 합니다.<tr><td>`ActiveDirectoryInteractive`<td>_Windows 드라이버만_합니다. 대화형 인증을 사용 하 여 Azure Active Directory id를 사용 하 여 인증 합니다.</table>|
|`Encrypt`|(설정 안 됨), `Yes`, `No`|(설명 참조)|연결의 암호화를 제어합니다. 경우 사전 특성 값을 `Authentication` 설정이 잘못 되었습니다 _none_ DSN 또는 연결 문자열에서 기본값은 `Yes`합니다. 그렇지 않은 경우 기본값은 `No`입니다. 경우 특성 `SQL_COPT_SS_AUTHENTICATION` 사전 특성 값을 재정의 `Authentication`, 명시적으로 DSN 또는 연결 문자열이 나 연결 특성에서 암호화 값을 설정 합니다. 암호화 전 특성 값이 `Yes` 값 설정 된 경우 `Yes` DSN 또는 연결 문자열입니다.|

## <a name="new-andor-modified-connection-attributes"></a>새롭거나 수정 된 연결 특성

다음 사전 연결 특성 중 도입 되거나 Azure Active Directory 인증을 지원 하도록 수정 합니다. 연결 특성에 해당 연결 문자열 또는 DSN 키워드를 설정 하는 경우 연결 특성을 우선적으로 적용 합니다.

|attribute|형식|값|Default|설명|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_RESET`|(설정 안 됨)|에 대 한 설명을 참조 하세요. `Authentication` 위의 키워드입니다. `SQL_AU_NONE` 집합을 명시적으로 재정의 하기 위해 제공 됩니다 `Authentication` DSN 및/또는 연결 문자열에 값 동안 `SQL_AU_RESET` DSN 또는 연결 문자열 값 보다 우선적으로 적용을 하도록 허용, 설정 된 경우 특성 unsets 합니다.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|에 대 한 포인터 `ACCESSTOKEN` 또는 NULL|NULL|Null이 아닌 경우 azure Ad 액세스 토큰을 사용 하 여 지정 합니다. 액세스 토큰을 지정 하면 오류가 발생 그리고 `UID`, `PWD`, `Trusted_Connection`, 또는 `Authentication` 연결 문자열 키워드 또는 해당 특성에 해당 합니다. <br> **참고:** ODBC 드라이버 13.1 버전에만 지원 이렇게 _Windows_합니다.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(설명 참조)|연결의 암호화를 제어합니다. `SQL_EN_OFF` 및 `SQL_EN_ON` 사용 하지 않도록 설정 하 고 각각의 암호화를 사용 하도록 설정 합니다. 경우 사전 특성 값을 `Authentication` 설정이 잘못 되었습니다 _none_ 또는 `SQL_COPT_SS_ACCESS_TOKEN` 설정 되어 및 `Encrypt` 기본값은 DSN 또는 연결 문자열에 지정 되지 않았습니다 `SQL_EN_ON`합니다. 그렇지 않은 경우 기본값은 `SQL_EN_OFF`입니다. 경우 연결 특성 `SQL_COPT_SS_AUTHENTICATION` 로 설정 되어 하지 _none_명시적으로 설정 합니다 `SQL_COPT_SS_ENCRYPT` 값을 원하는 값 경우 `Encrypt` DSN 또는 연결 문자열에 지정 되지 않았습니다. 이 특성을 제어의 유효 값 [연결에 대 한 암호화를 사용할지 여부입니다.](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|ODBC 연결을 통해 AAD 보안 주체에 대 한 암호 변경을 수행할 수 없는 하므로 Azure Active Directory를 사용 하 여 지원 되지 않습니다. <br><br>SQL Server 인증의 암호 만료가 SQL Server 2005에 도입되었습니다. `SQL_COPT_SS_OLDPWD` 클라이언트가 연결에 대 한 기존 및 새 암호를 제공할 수 있도록 특성이 추가 되었습니다. 이 속성을 설정하면 변경된 "이전 암호"가 연결 문자열에 포함되기 때문에 공급자가 첫 번째 연결 또는 이후 연결에 연결 풀을 사용하지 않습니다.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_사용 되지 않음_; 사용 `SQL_COPT_SS_AUTHENTICATION` 로 `SQL_AU_AD_INTEGRATED` 대신 합니다. <br><br>강제로 서버 로그인에 대 한 액세스 유효성 검사에 대 한 Windows 인증 (Kerberos Linux 및 macOS)를 사용합니다. 드라이버의 일부로 제공 되는 사용자 식별자와 암호 값을 무시 Windows 인증을 사용 하는 경우 `SQLConnect`하십시오 `SQLDriverConnect`, 또는 `SQLBrowseConnect` 처리 합니다.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Azure Active Directory (Windows 드라이버에만 해당)에 대 한 UI 추가

DSN 설정 및 드라이버의 Ui 연결을 Azure AD를 사용 하 여 인증을 사용 하는 데 필요한 추가 옵션을 사용 하 여 향상 되었습니다.

### <a name="creating-and-editing-dsns-in-the-ui"></a>만들기 및 편집 UI에서 Dsn

새 Azure AD 사용 하 여 인증 옵션을 만들 때 또는 드라이버의 설치 UI를 사용 하 여 기존 DSN을 편집 하는 것이 가능:

`Authentication=ActiveDirectoryIntegrated` SQL Azure에 대한 Azure Active Directory 통합 인증

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword` SQL Azure Azure Active Directory 사용자 이름/암호 인증

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` SQL Azure에 대한 Azure Active Directory 대화형 인증 지원

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` SQL server 사용자 이름/암호 인증에 대 한 (Azure 또는 기타)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` Windows에 대 한 레거시 SSPI 통합 인증

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

에 해당 하는 다섯 가지 옵션 `Trusted_Connection=Yes` (기존 레거시 Windows SSPI 전용 통합된 인증) 및 `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`에 `ActiveDirectoryPassword`, 및 `ActiveDirectoryInteractive`, 각각.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect 프롬프트 (Windows 드라이버에만 해당)

SQLDriverConnect 연결을 완료 하는 데 필요한 정보가 요청 될 때 표시 되는 메시지 대화 상자에 Azure AD 인증을 위한 세 가지 새로운 옵션

![ServerLogin.png](windows/ServerLogin.png)

이러한 옵션은 위의 UI DSN 설정에서 사용할 수 있는 동일한 5에 해당합니다.

### <a name="example-connection-strings"></a>연결 문자열 예
1. SQL Server 인증-레거시 구문 서버 인증서 유효성이 검사 되지 않습니다 하 고 서버에 적용 하는 경우에 암호화가 사용 됩니다. 사용자 이름/암호는 연결 문자열에 전달 됩니다.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 인증-새 구문입니다. 암호화를 요청 하는 클라이언트 (기본값인 `Encrypt` 됩니다 `true`) 유효성이 확인 되 고 암호화 설정에 관계 없이 서버 인증서를 가져옵니다 (경우가 아니면 `TrustServerCertificate` 로 설정 된 `true`). 사용자 이름/암호는 연결 문자열에 전달 됩니다.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. 통합 Windows 인증 (Kerberos Linux 및 macOS) 현재 구문을 SSPI (SQL Server 또는 SQL IaaS)를 사용 하 여 합니다. 서버 인증서 암호화가 사용 하지 않는 한 검증 되지 않은 합니다. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Windows 드라이버만_.) 통합 Windows 인증을 사용 하 여 SSPI (SQL Server 또는 SQL IaaS에서의 데이터베이스에서 대상 데이터베이스로 경우)-새 구문입니다. 암호화를 요청 하는 클라이언트 (기본값인 `Encrypt` 됩니다 `true`) 유효성이 확인 되 고 암호화 설정에 관계 없이 서버 인증서를 가져옵니다 (경우가 아니면 `TrustServerCertificate` 로 설정 된 `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD (Azure SQL db에서의 데이터베이스에서 대상 데이터베이스로 경우) 사용자 이름/암호 인증입니다. 서버 인증서 유효성을 검사, 암호화 설정에 관계 없이 (하지 않는 한 `TrustServerCertificate` 로 설정 된 `true`). 사용자 이름/암호는 연결 문자열에 전달 됩니다. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Windows 드라이버만_.) ADAL을 사용 하면 AAD에서 발급 한 액세스 토큰에 대 한 Windows 계정 자격 증명 사용을 포함 하는 대상 데이터베이스가 Azure SQL Database에서 가정 하 고 사용 하 여 Windows 인증을 통합 합니다. 서버 인증서 유효성을 검사, 암호화 설정에 관계 없이 (하지 않는 한 `TrustServerCertificate` 로 설정 된 `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Windows 드라이버만_.) AAD 대화형 인증 연결을 설정 하려면 Azure multi-factor Authentication 기술을 사용 합니다. 로그인 ID를 제공 하 여이 모드에서는 Windows Azure 인증 대화 상자가 트리거되고 연결을 완료 하기 위해 암호를 입력 하면 됩니다. 사용자는 연결 문자열에 전달 됩니다.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

> [!NOTE] 
>- Windows ODBC 드라이버를 사용 하 여 새 Active Directory 옵션을 사용 하는 경우에 있는지 확인 합니다 [SQL Server 용 Active Directory 인증 라이브러리](https://go.microsoft.com/fwlink/?LinkID=513072) 설치가 완료 된 후입니다. Linux 및 macOS 드라이버를 사용 하는 경우 확인 `libcurl` 가 설치 되었습니다. 다른 인증 방법이 나 ODBC 작업에 필요한 아니므로 드라이버 버전 17.2 이상에서 명시적 종속성 되지 않습니다.
>- SQL Server 계정 사용자 이름 및 암호를 사용 하 여 연결을 사용할 수 있습니다 새 `SqlPassword` 이 옵션을 사용 하면 더 안전한 연결 기본값 이므로 특히 SQL Azure 대 한 권장 되지 않는 옵션입니다.
>- 연결 하려면 Azure Active Directory 계정 사용자 이름 및 암호를 사용 하 여 지정 합니다 `Authentication=ActiveDirectoryPassword` 연결 문자열에는 `UID` 및 `PWD` 키워드의 사용자 이름 및 암호를 각각.
>- Windows 통합 인증 또는 Active Directory 통합 (Windows 드라이버에만 해당) 인증을 사용 하 여 연결할 지정 `Authentication=ActiveDirectoryIntegrated` 연결 문자열에 있습니다. 드라이버는 올바른 인증 모드를 자동으로 선택 됩니다. `UID` 및 `PWD` 지정 하면 안 됩니다.
>- Active Directory Interactive (Windows 드라이버에만 해당) 인증을 사용 하 여 연결할 `UID` 지정 해야 합니다.

## <a name="authenticating-with-an-access-token"></a>액세스 토큰을 사용 하 여 인증

`SQL_COPT_SS_ACCESS_TOKEN` 사전 연결 특성 대신 사용자 이름 및 암호 인증을 위해 Azure AD에서 얻은 액세스 토큰을 사용할 수 있습니다 및 협상 및 드라이버에서 액세스 토큰의 가져오기도 무시 합니다. 액세스 토큰을 사용 하려면 설정 합니다 `SQL_COPT_SS_ACCESS_TOKEN` 연결 특성에 대 한 포인터는 `ACCESSTOKEN` 구조:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

합니다 `ACCESSTOKEN` 는 4 바이트 이루어진 가변 길이 구조 _길이_ 뒤 _길이_ 액세스 토큰을 형성 하는 불투명 데이터의 바이트입니다. 그러나 SQL Server 액세스 토큰을 처리 하는 방법으로 인해을 통해 얻은 하나는 [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) 되도록 각 바이트는 바이트를 ASCII 문자만 포함 하는 ucs-2 문자열 비슷합니다 안쪽 여백을 0으로 JSON 응답을 확장할 수 있어야 합니다; 토큰은 불투명 값 및 길이 (바이트)에 지정 된 null 종결자를 포함 하지 해야 합니다. 해당 상당한 길이 및 형식 제약 조건으로 인해이 인증 방법은을 통해 프로그래밍 방식으로 사용할 수는 `SQL_COPT_SS_ACCESS_TOKEN` 연결 특성; 해당 DSN 또는 연결 문자열 키워드가 필요 하지 않습니다. 연결 문자열 없어야 `UID`, `PWD`를 `Authentication`, 또는 `Trusted_Connection` 키워드입니다.

> [!NOTE]
> ODBC 드라이버 버전 13.1이이 인증에만 지원 _Windows_합니다.

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 인증 샘플 코드

다음 샘플 연결 키워드를 사용 하 여 Azure Active Directory를 사용 하 여 SQL Server에 연결 하는 데 필요한 코드를 보여 줍니다. 자체 응용 프로그램 코드를 변경할 필요가 없습니다 연결 문자열 또는 DSN을 사용 하는 경우 다음과 같습니다. AAD를 사용 하 여 인증 하는 데 필요한 유일한 수정
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
다음 샘플 Azure Active Directory를 사용 하 여 액세스 토큰 인증을 사용 하 여 SQL Server에 연결 하는 데 필요한 코드를 보여 줍니다. 이 경우 액세스 토큰을 처리 하 고 연결 특성을 설정 하는 응용 프로그램 코드를 수정 해야 할 것입니다.
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
다음은 Azure Active Directory 대화형 인증 사용에 대 한 샘플 연결 문자열입니다. 참고는 없습니다 PWD 필드 처럼 Windows Azure 인증 화면을 사용 하 여 암호를 입력 해야 합니다.
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~

## <a name="see-also"></a>참고 항목
[Azure AD 인증을 사용 하 여 Azure SQL DB에 대 한 토큰 기반 인증 지원](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

