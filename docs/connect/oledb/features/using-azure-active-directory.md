---
title: Azure Active Directory를 사용 하 여 | SQL Server 용 Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 44f92e782a497005ea47847301279e4341722d36
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744862"
---
# <a name="using-azure-active-directory"></a>Azure Active Directory 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>용도

18.2.1 버전부터 Microsoft OLE DB Driver for SQL Server OLE DB 응용 프로그램이 있습니다 Azure SQL Database 인스턴스에 연결 하려면 페더레이션된 id를 사용 하 여. 새 인증 방법은 다음과 같습니다.
- Azure Active Directory 로그인 ID 및 암호
- Azure Active Directory 액세스 토큰
- Azure Active Directory 통합 인증
- SQL 로그인 ID 및 암호

> [!NOTE]  
> OLE DB 드라이버를 사용 하 여 다음 Azure Active Directory 옵션을 사용 하는 경우에 있는지 확인 합니다 [SQL Server 용 Active Directory 인증 라이브러리](https://go.microsoft.com/fwlink/?LinkID=513072) 설치가 완료 된 후:
> - Azure Active Directory 로그인 ID 및 암호
> - Azure Active Directory 통합 인증
>
> ADAL는 다른 인증 방법 또는 OLE DB 작업에 필요 하지 않습니다.

> [!NOTE]
> 사용 하 여 다음과 같은 인증 모드를 사용 하 여 `DataTypeCompatibility` (또는 해당 속성)로 `80` 됩니다 **하지** 지원:
> - 로그인 ID 및 암호를 사용 하 여 azure Active Directory 인증
> - 액세스 토큰을 사용 하 여 azure Active Directory 인증
> - Azure Active Directory 통합 인증

## <a name="connection-string-keywords-and-properties"></a>연결 문자열 키워드 및 속성
Azure Active Directory 인증을 지원 하도록 연결 문자열 키워드 도입 되었습니다.

|연결 문자열 키워드|연결 속성|설명|
|---               |---                |---        |
|액세스 토큰|SSPROP_AUTH_ACCESS_TOKEN|Azure Active Directory에 인증 하기 위한 액세스 토큰을 지정 합니다. |
|인증|SSPROP_AUTH_MODE|사용할 인증 방법을 지정 합니다.|

새 키워드/속성에 대 한 자세한 내용은 다음 페이지를 참조 하세요.
- [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [초기화 및 권한 부여 속성](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>암호화 및 인증서 유효성 검사
이 섹션에서는 암호화 및 인증서 유효성 검사 동작의 변경 내용을 설명 합니다. 이러한 변경은 **만** 새 인증 또는 액세스 토큰 연결 문자열 키워드 (또는 해당 속성)를 사용 하는 경우 유효 합니다.

### <a name="encryption"></a>암호화
새 연결 속성/키워드를 사용할 때 보안을 향상을 위해 드라이버를 설정 하 여 기본 암호화 값을 재정의 `yes`합니다. 재정의 데이터 원본 개체 초기화 시 발생합니다. 암호화를 어떤 방법으로 초기화 하기 전에 설정에 값이 적용 하 고 재정의 되지 않은 합니다.

> [!NOTE]   
> ADO 응용 프로그램에 가져오는 응용 프로그램에는 `IDBInitialize` 를 통해 상호 작용 `IDataInitialize::GetDataSource`, 암호화의 기본값으로 설정 하는 핵심 구성 요소 인터페이스를 명시적으로 구현 `no`합니다. 새 인증 속성/키워드가이 설정 및 암호화 값을 준수 하는 결과적으로 **되지** 재정의 합니다. 따라서 **것이 좋습니다** 이러한 응용 프로그램에서 명시적으로 설정 된 `Use Encryption for Data=true` 기본값을 재정의 합니다.

### <a name="certificate-validation"></a>인증서의 유효성 검사
보안을 강화 하려면 새 연결 속성/키워드 존중 합니다 `TrustServerCertificate` 설정 (및 해당 연결 문자열 키워드/속성) **클라이언트 암호화 설정은 독립적으로**입니다. 결과적으로, 서버 인증서는 기본적으로 유효성이 검사 됩니다.

> [!NOTE]   
> 인증서 유효성 검사를 통해 제어할 수도 있습니다는 `Value` 필드는 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2` 레지스트리 항목입니다. 유효한 값은 `0` 또는 `1`입니다. OLE DB 드라이버는 레지스트리와 연결 속성/키워드 설정이 가장 안전한 옵션을 선택합니다. 즉, 드라이버는 서버 인증서 유효성 검사를 사용 하는 하나 이상의 레지스트리/연결 설정으로 서버 인증서를 확인 합니다.

## <a name="gui-additions"></a>GUI 추가
드라이버 그래픽 사용자 인터페이스를 Azure Active Directory 인증을 허용 하도록 향상 되었습니다. 참조 항목:
- [SQL Server 로그인 대화 상자](../help-topics/sql-server-login-dialog.md)
- [유니버설 데이터 링크 (UDL) 구성](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>연결 문자열 예
이 섹션에서는 신규 및 기존 연결의 예제와 함께 사용 될 문자열 키워드 `IDataInitialize::GetDataSource` 고 `DBPROP_INIT_PROVIDERSTRING` 속성입니다.

### <a name="sql-authentication"></a>SQL 인증
- `IDataInitialize::GetDataSource`사용:
    - 새 항목:
        > 공급자 = MSOLEDBSQL; 데이터 원본 [서버] =; Initial Catalog = [데이터베이스]; **Authentication = SqlPassword**; 사용자 ID = [username]; 암호 [password] =; 데이터에 대 한 암호화를 사용 하 여 = true
    - 사용되지 않음:
        > 공급자 = MSOLEDBSQL; 데이터 원본 [서버] =; Initial Catalog = [데이터베이스]; 사용자 ID = [username]; 암호 [password] =; 데이터에 대 한 암호화를 사용 하 여 = true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    - 새 항목:
        > Server=[server];Database=[database];**Authentication=SqlPassword**;UID=[username];PWD=[password];Encrypt=yes
    - 사용되지 않음:
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface--sspi"></a>보안 지원 공급자 인터페이스 (SSPI)를 사용 하 여 통합된 Windows 인증

- `IDataInitialize::GetDataSource`사용:
    - 새 항목:
        > 공급자 = MSOLEDBSQL; 데이터 원본 [서버] =; Initial Catalog = [데이터베이스]; **Authentication = ActiveDirectoryIntegrated**; 데이터에 대 한 암호화를 사용 하 여 = true
    - 사용되지 않음:
        > 공급자 = MSOLEDBSQL; 데이터 원본 [서버] =; Initial Catalog = [데이터베이스]; **Integrated Security = SSPI**; 데이터에 대 한 암호화를 사용 하 여 = true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    - 새 항목:
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes
    - 사용되지 않음:
        > Server=[server];Database=[database];**Trusted_Connection=yes**;Encrypt=yes

### <a name="aad-username-and-password-authentication-using-adal"></a>ADAL을 사용 하 여 AAD 사용자 이름 및 암호 인증

- `IDataInitialize::GetDataSource`사용:
    > 공급자 = MSOLEDBSQL; 데이터 원본 [서버] =; Initial Catalog = [데이터베이스]; **Authentication = ActiveDirectoryPassword**; 사용자 ID = [username]; 암호 [password] =; 데이터에 대 한 암호화를 사용 하 여 = true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-azure-active-directory-authentication-using-adal"></a>ADAL을 사용 하 여 통합된 Azure Active Directory 인증

- `IDataInitialize::GetDataSource`사용:
    > 공급자 = MSOLEDBSQL; 데이터 원본 [서버] =; Initial Catalog = [데이터베이스]; **Authentication = ActiveDirectoryIntegrated**; 데이터에 대 한 암호화를 사용 하 여 = true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>액세스 토큰을 사용 하 여 azure Active Directory 인증

- `IDataInitialize::GetDataSource`사용:
    > 공급자 = MSOLEDBSQL; 데이터 원본 [서버] =; Initial Catalog = [데이터베이스]; **액세스 토큰 [액세스 토큰] =**; 데이터에 대 한 암호화를 사용 하 여 = true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    > 통해 액세스 토큰을 제공 `DBPROP_INIT_PROVIDERSTRING` 지원 되지 않습니다

## <a name="code-samples"></a>코드 샘플

다음 샘플에서는 연결 키워드를 사용 하 여 Azure Active Directory에 연결 하는 데 필요한 코드를 보여 줍니다. 

### <a name="access-token"></a>액세스 토큰
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    wchar_t accessToken[] = L"eyJ0eXAiOi...";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Access Token=" + accessToken + L";Use Encryption for Data=true;";
    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```
### <a name="active-directory-integrated"></a>Active Directory 통합
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Authentication=ActiveDirectoryIntegrated;Use Encryption for Data=true;";

    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr)) 
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```

## <a name="next-steps"></a>다음 단계
- [Oauth2.0 코드 부여 흐름을 사용 하 여 Azure Active Directory 웹 응용 프로그램에 대 한 액세스 권한을 부여](https://go.microsoft.com/fwlink/?linkid=2072672)합니다.

- SQL Server에 대한 [Azure Active Directory 인증](https://go.microsoft.com/fwlink/?linkid=2073783)에 대해 자세히 알아보세요.

- 사용 하 여 드라이버 연결 구성 [연결 문자열 키워드](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md) OLE DB 드라이버 지원 합니다.
