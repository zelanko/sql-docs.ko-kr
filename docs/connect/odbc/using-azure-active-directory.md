---
title: "Azure Active Directory를 사용 하 여 ODBC 드라이버로 | Microsoft Docs"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 801f0ec683811776b7a249e4984030d3496e5a1e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Azure Active Directory를 사용 하 여 ODBC 드라이버
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>용도

사용자 이름/암호, Azure Active Directory 액세스 토큰 (Windows 드라이버만), 또는 Windows 통합으로 Azure Active Directory의 페더레이션된 id를 사용 하 여 ODBC Driver 13.1 for SQL Server가 ODBC 응용 프로그램을 SQL Azure 인스턴스에 연결할 수 있습니다. 인증 (Windows 드라이버에만 해당)입니다. 이 새 DSN 및 연결 문자열 키워드 및 연결 특성을 사용 하 여 수행 됩니다.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>새 또는 수정 된 DSN 및 연결 문자열 키워드

`Authentication` 키워드 인증 모드를 제어 하에 DSN 또는 연결 문자열과 연결할 때 사용할 수 있습니다. 연결 문자열에 설정 된 값 제공 하는 DSN에서 재정의 합니다. _미리 특성 값_ 의 `Authentication` 설정은 연결 문자열 및 DSN 값에서 계산 된 값입니다.

|이름|값|기본값|Description|
|-|-|-|-|
|`Authentication`|(설정 안 함) (빈 문자열), `SqlPassword`, `ActiveDirectoryPassword`,`ActiveDirectoryIntegrated`|(설정 안 됨)|인증 모드를 제어합니다.<table><tr><th>값<th>Description<tr><td>(설정 안 됨)<td>다른 모든 키워드 (기존 레거시 연결 옵션)에 의해 결정 되는 인증 모드<tr><td>(빈 문자열)<td>(연결 문자열만 합니다.) 재정의 설정을 해제 하 고는 `Authentication` 값이 DSN에서 설정 합니다.<tr><td>`SqlPassword`<td>사용자 이름 및 암호를 사용 하 여 SQL Server 인스턴스를 직접 인증 합니다.<tr><td>`ActiveDirectoryPassword`<td>사용자 이름 및 암호를 사용 하 여 Azure Active Directory id로 인증 합니다.<tr><td>`ActiveDirectoryIntegrated`<td>_Windows 드라이버만_합니다. 통합된 인증을 사용 하 여 Azure Active Directory id로 인증 합니다.</table>|
|`Encrypt`|(설정 안 함) `Yes`,`No`|(설명 참조)|연결의 암호화를 제어합니다. 하는 경우의 사전 특성 값은 `Authentication` 설정이 잘못 되었습니다 _none_, 기본값은 `Yes`합니다. 그렇지 않은 경우 기본값은 `No`합니다. 암호화 전 특성 값이 `Yes` 값으로 설정 되 면 `Yes` DSN 또는 연결 문자열에 있습니다.|

## <a name="new-andor-modified-connection-attributes"></a>새 또는 수정 된 연결 특성

다음 연결 특성 중 하나 도입 되거나 수정 되지 Azure Active Directory 인증을 지원 하기 위해 미리 연결 합니다. 연결 특성에 해당 연결 문자열 또는 DSN 키워드 설정 된 경우 연결 특성 우선적으로 적용 합니다.

|Attribute|형식|값|기본값|Description|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_RESET`|(설정 안 됨)|설명을 참조 `Authentication` 위의 키워드입니다. `SQL_AU_NONE`집합을 명시적으로 재정의 하기 위해 제공 됩니다 `Authentication` DSN 및/또는 연결 문자열의 값 동안 `SQL_AU_RESET` DSN 또는 연결 문자열 값 보다 우선 적용을 허용, 설정 된 경우 특성 설정이 해제 합니다.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|에 대 한 포인터 `ACCESSTOKEN` 또는 NULL|NULL|_Windows 드라이버만_합니다. Null이 아닌 경우 azure Ad 액세스 토큰을 사용 하 여 지정 합니다. 액세스 토큰을 지정 하려면 오류가 발생 그리고 `UID`, `PWD`, `Trusted_Connection`, 또는 `Authentication` 연결 문자열 키워드 또는 해당 하는 특성입니다.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(설명 참조)|연결의 암호화를 제어합니다. `SQL_EN_OFF`및 `SQL_EN_ON` 각각 암호화를 활성화 및 비활성화 합니다. 하는 경우의 사전 특성 값은 `Authentication` 설정이 잘못 되었습니다 _none_ 또는 `SQL_COPT_SS_ACCESS_TOKEN` 설정 되어 및 `Encrypt` 기본값은 DSN 또는 연결 문자열에 지정 되지 않았습니다 `SQL_EN_ON`합니다. 그렇지 않은 경우 기본값은 `SQL_EN_OFF`합니다. 이 특성에 따라 제어의 유효 값 [연결에 암호화를 사용할지 여부입니다.](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|ODBC 연결을 통해 AAD 보안 주체에 암호 변경 내용을 정의할 수 없는 이후 Azure Active Directory와 지원 되지 않습니다. <br><br>SQL Server 인증에 대 한 암호 만료 SQL Server 2005에서 도입 되었습니다. `SQL_COPT_SS_OLDPWD` 특성이 연결에 대 한 이전 및 새 암호를 모두 제공 하는 클라이언트에 추가 되었습니다. 이 속성을 설정하면 변경된 "이전 암호"가 연결 문자열에 포함되기 때문에 공급자가 첫 번째 연결 또는 이후 연결에 연결 풀을 사용하지 않습니다.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_사용 되지 않는_; 사용 하 여 `SQL_COPT_SS_AUTHENTICATION` 로 설정 `SQL_AU_AD_INTEGRATED` 대신 합니다. <br><br>서버 로그인에 대 한 액세스 유효성 검사를 위한 강제로 Windows 인증 (Linux와 macOS에서 Kerberos)의 사용합니다. 드라이버의 일부로 제공 된 사용자 식별자와 암호 값을 무시 Windows 인증을 사용 하는 경우 `SQLConnect`, `SQLDriverConnect`, 또는 `SQLBrowseConnect` 처리 합니다.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Azure Active Directory (Windows 드라이버)에 대 한 UI 추가

DSN 설정 및 연결 Ui 드라이버의 Azure AD에 인증을 사용 하는 데 필요한 추가 옵션으로 향상 되었습니다.

### <a name="creating-and-editing-dsns-in-the-ui"></a>만들기 및 Dsn UI에서 편집

새 Azure AD 사용 하 여 인증 옵션을 만들 때 또는 드라이버의 설치 프로그램 UI를 사용 하 여 기존의 DSN을 편집 하는 것이 불가능:

`Authentication=ActiveDirectoryIntegrated`SQL Azure에 Azure Active Directory 통합 인증을 위해

![CreateNewDSN3.png](windows/CreateNewDSN3.png)

`Authentication=ActiveDirectoryPassword`SQL Azure에 Azure Active Directory 사용자 이름/암호 인증

![CreateNewDSN4.png](windows/CreateNewDSN4.png)

`Authentication=SqlPassword`SQL Server에 사용자 이름/암호 인증 (Azure 또는 기타)

![CreateNewDSN.png](windows/CreateNewDSN.png)

`Trusted_Connection=Yes`Windows 용 레거시 SSPI 통합 인증

![CreateNewDSN2.png](windows/CreateNewDSN2.png)

에 해당 하는 네 가지 옵션 `Trusted_Connection=Yes` (기존 레거시 Windows SSPI 전용 통합된 인증) 및 `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`, 및 `ActiveDirectoryPassword`각각.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect 프롬프트 (Windows 드라이버)

연결을 완료 하는 데 필요한 정보를 요청할 때 SQLDriverConnect 하 여 표시 되는 메시지 대화 상자에 Azure AD 인증에 대 한 두 개의 새 옵션이 있습니다.

![SQLServerLogin.png](windows/SQLServerLogin.png)

이러한 옵션은 DSN 설치 위의 UI에서에서 사용할 수 있는 동일한 4에 해당합니다.

### <a name="example-connection-strings"></a>연결 문자열 예
1. SQL Server 인증-레거시 구문입니다. 서버 인증서 유효성이 검사 되지 않습니다 및 서버에 적용 하는 경우에 암호화가 사용 됩니다. 사용자 이름/암호는 연결 문자열에 전달 됩니다.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL 인증-새로운 구문입니다. 클라이언트에서 암호화를 요청 (의 기본값 `Encrypt` 은 `true`) 유효성을 검사, 암호화 설정에 관계 없이 서버 인증서를 가져옵니다 (하지 않는 한 `TrustServerCertificate` 로 설정 된 `true`). 사용자 이름/암호는 연결 문자열에 전달 됩니다.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Windows 통합 인증 (Kerberos Linux와 macOS에서) SQL Server 또는 SQL IaaS) – (에 SSPI 현재 구문을 사용 하 여 합니다. 암호화가 사용 하지 않는 한 서버 인증서 확인 되지 않습니다. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Windows 드라이버만_.) Windows 통합 인증을 사용 하 여 SSPI (SQL Server 또는 SQL IaaS에서의 데이터베이스에서 대상 데이터베이스로 경우) – 새 구문입니다. 클라이언트에서 암호화를 요청 (의 기본값 `Encrypt` 은 `true`) 유효성을 검사, 암호화 설정에 관계 없이 서버 인증서를 가져옵니다 (하지 않는 한 `TrustServerCertificate` 로 설정 된 `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD (Azure SQL DB에서의 데이터베이스에서 대상 데이터베이스로 경우) 사용자 이름/암호 인증입니다. 암호화 설정에 관계 없이 서버 인증서 확인을 가져옵니다 (하지 않는 한 `TrustServerCertificate` 로 설정 된 `true`). 사용자 이름/암호는 연결 문자열에 전달 됩니다. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Windows 드라이버만_.) Windows 통합된 인증 ADAL 사용 하 여, 교환 액세스 AAD에서 발급 한 토큰에 대 한 Windows 계정 자격 증명을 포함 되는 Azure SQL 데이터베이스에서 대상 데이터베이스 라고 가정 합니다. 암호화 설정에 관계 없이 서버 인증서 확인을 가져옵니다 (하지 않는 한 `TrustServerCertificate` 로 설정 된 `true`). 
`server=Server;database=Database; Authentication=ActiveDirectoryIntegrated;`

> [!NOTE] 
>- 새 Active Directory 옵션와 Windows ODBC 드라이버를 사용 하는 경우는 [SQL Server 용 Active Directory 인증 라이브러리](http://go.microsoft.com/fwlink/?LinkID=513072) 가 설치 되어 있습니다. Linux와 macOS 드라이버에는 Azure Active Directory에 인증 하기 위해 추가 종속성이 필요 하지 않습니다.
>- SQL Server 계정 사용자 이름 및 암호를 사용 하 여 연결을 사용할 수도 있습니다 이제 새 `SqlPassword` 연결 기본값 보다 안전한이 옵션을 사용 하므로 SQL Azure를 위해 특별히 권장 옵션입니다.
>- Azure Active Directory 계정 사용자 이름 및 암호를 사용 하 여 연결할 지정 `Authentication=ActiveDirectoryPassword` 연결 문자열에 및 `UID` 및 `PWD` 키워드와 사용자 이름 및 암호를 각각.
>- Windows 통합 인증 또는 Active Directory 통합 (Windows 드라이버) 인증을 사용 하 여 연결할 지정 `Authentication=ActiveDirectoryIntegrated` 연결 문자열에 있습니다. 드라이버는 자동으로 올바른 인증 모드를 선택 합니다. `UID`및 `PWD` 지정 하면 안 됩니다.

## <a name="authenticating-with-an-access-token-windows-driver-only"></a>액세스 토큰 (Windows 드라이버)를 사용 하 여 인증

`SQL_COPT_SS_ACCESS_TOKEN` 사전 연결 특성 대신 사용자 이름과 암호를 인증에 대 한 Azure AD에서 가져온 액세스 토큰을 사용할 수 있습니다 및 협상 하 고 드라이버에서 액세스 토큰의 가져오기도 무시 합니다. 액세스 토큰을 사용 하려면 설정는 `SQL_COPT_SS_ACCESS_TOKEN` 연결 특성에 대 한 포인터로 `ACCESSTOKEN` 구조:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

`ACCESSTOKEN` 4 바이트의 구성 된 가변 길이 구조 _길이_ 이어서 _길이_ 액세스 토큰을 형성 하는 불투명 한 데이터의 바이트입니다. 통해 얻은 하나는 SQL Server 액세스 토큰 처리 하는 방법을, 인해는 [OAuth 2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios) JSON 응답 각 바이트 다음에 바이트를 ASCII 문자만 포함 하는 ucs-2 문자열 비슷합니다 패딩 0 확장 해야 합니다; 그러나 토큰 불투명 값 및를 바이트 단위로 지정 된 길이 null 종결자를 포함 하지 않아야 합니다. 자신의 상당한 길이 형식 제약 조건으로 인해이 인증 방법은을 통해 프로그래밍 방식으로 사용할 수는 `SQL_COPT_SS_ACCESS_TOKEN` coonnection 특성; 해당 DSN 또는 연결 문자열 키워드에 없습니다. 연결 문자열 없어야 `UID`, `PWD`, `Authentication`, 또는 `Trusted_Connection` 키워드입니다.

## <a name="azure-active-directory-authentication-sample-code"></a>Azure Active Directory 인증 예제 코드

다음 샘플 연결 키워드와 Azure Active Directory를 사용 하 여 SQL Server에 연결 하는 데 필요한 코드를 보여 줍니다. 자체 응용 프로그램 코드를 변경할 필요가 없습니다 연결 문자열 또는 DSN을 사용 하는 경우 인증을 위해 AAD를 사용 하는 데 필요한 유일한 수정입니다.
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
다음 샘플 액세스 토큰 인증와 Azure Active Directory를 사용 하 여 SQL Server에 연결 하는 데 필요한 코드를 보여 줍니다. 이 경우 액세스 토큰을 처리 하 고 관련된 연결 특성을 설정 하도록 응용 프로그램 코드를 수정 하는 데 필요한입니다.
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

## <a name="see-also"></a>관련 항목:
[Azure AD 인증을 사용 하 여 Azure SQL DB에 대 한 토큰 기반 인증 지원](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)


