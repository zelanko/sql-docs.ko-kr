---
title: Azure Active Directory 사용
description: Azure SQL 데이터베이스에 연결하기 위해 Microsoft OLE DB Driver for SQL Server에서 사용할 수 있는 Azure Active Directory 인증 방법을 알아봅니다.
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: bace88bd8ccf42cbef96a34ddb2af2593cedd7be
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727302"
---
# <a name="using-azure-active-directory"></a>Azure Active Directory 사용
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>목적

버전 18.2.1부터 Microsoft OLE DB Driver for SQL Server를 사용하면 OLE DB 애플리케이션에서 페더레이션 ID를 사용하여 Azure SQL Database 인스턴스에 연결할 수 있습니다. 새 인증 방법에는 다음이 포함됩니다.
- Azure Active Directory 로그인 ID 및 암호
- Azure Active Directory 액세스 토큰
- Azure Active Directory 통합 인증
- SQL 로그인 ID 및 암호

버전 18.3에는 다음 인증 방법에 대한 지원이 추가되었습니다.
- Azure Active Directory 대화형 인증
- Azure Active Directory 관리 ID 인증

> [!NOTE]
> `DataTypeCompatibility`(또는 해당 속성)를 `80`으로 설정하면 다음 인증 모드가 지원되지 **않습니다**.
> - 로그인 ID 및 암호를 사용하여 Azure Active Directory 인증
> - 액세스 토큰을 사용하여 Azure Active Directory 인증
> - Azure Active Directory 통합 인증
> - Azure Active Directory 대화형 인증
> - Azure Active Directory 관리 ID 인증

## <a name="connection-string-keywords-and-properties"></a>연결 문자열 키워드 및 속성
Azure Active Directory 인증을 지원하기 위해 다음과 같은 연결 문자열 키워드가 도입되었습니다.

|연결 문자열 키워드|Connection 속성|설명|
|---               |---                |---        |
|액세스 토큰|SSPROP_AUTH_ACCESS_TOKEN|Azure Active Directory에 인증할 액세스 토큰을 지정합니다. |
|인증|SSPROP_AUTH_MODE|사용할 인증 방법을 지정합니다.|

새 키워드/속성에 대한 자세한 내용은 다음 페이지를 참조하세요.
- [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [초기화 및 권한 부여 속성](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>암호화 및 인증서 유효성 검사
이 섹션에서는 암호화 및 인증서 유효성 검사 동작의 변경 내용에 대해 설명합니다. 이러한 변경 내용은 새 인증 또는 액세스 토큰 연결 문자열 키워드(또는 해당 속성)를 사용하는 경우에만 **적용**됩니다.

### <a name="encryption"></a>암호화
보안을 개선하기 위해 새 연결 속성/키워드가 사용되는 경우 드라이버는 `yes`로 설정하여 기본 암호화 값을 재정의합니다. 재정의는 데이터 원본 개체 초기화 시 이루어집니다. 초기화 전에 암호화가 설정되면 값이 적용되고 재정의되지 않습니다.

> [!NOTE]   
> ADO 애플리케이션 및 `IDataInitialize::GetDataSource`를 통해 `IDBInitialize` 인터페이스를 가져오는 애플리케이션에서는 인터페이스를 구현하는 핵심 구성 요소가 명시적으로 암호화를 기본값 `no`로 설정합니다. 따라서 새 인증 속성/키워드가 이 설정을 준수하고 암호화 값이 재정의되지 **않습니다**. 따라서 이러한 애플리케이션이 명시적으로 `Use Encryption for Data=true`를 설정하여 기본값을 재정의할 것을 **권장**합니다.

### <a name="certificate-validation"></a>인증서의 유효성 검사
보안을 개선하기 위해 새 연결 속성/키워드는 **클라이언트 암호화 설정과 관계없이**`TrustServerCertificate` 설정(및 해당 연결 문자열 키워드/속성)을 준수합니다. 따라서 서버 인증서는 기본적으로 유효성이 검사됩니다.

> [!NOTE]   
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2` 레지스트리 항목의 `Value` 필드를 통해 인증서 유효성 검사를 제어할 수도 있습니다. 유효한 값은 `0` 또는 `1`입니다. OLE DB 드라이버는 레지스트리와 연결 속성/키워드 설정 사이에서 가장 안전한 옵션을 선택합니다. 즉, 레지스트리/연결 설정 중 하나 이상에서 서버 인증서 유효성 검사를 사용하도록 설정하면 드라이버가 서버 인증서의 유효성을 검사합니다.

## <a name="gui-additions"></a>GUI 추가
Azure Active Directory 인증을 허용하도록 드라이버 그래픽 사용자 인터페이스가 향상되었습니다. 자세한 내용은 다음을 참조하세요.
- [SQL Server 로그인 대화 상자](../help-topics/sql-server-login-dialog.md)
- [UDL(유니버설 데이터 링크) 구성](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>연결 문자열 예
이 섹션에서는 `IDataInitialize::GetDataSource` 및 `DBPROP_INIT_PROVIDERSTRING` 속성과 함께 사용되는 신규 및 기존 연결 문자열 키워드의 예를 보여 줍니다.

### <a name="sql-authentication"></a>SQL 인증
- `IDataInitialize::GetDataSource`사용:
    - 새 항목:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=SqlPassword**;User ID=[username];Password=[password];Use Encryption for Data=true
    - 사용되지 않음:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];User ID=[username];Password=[password];Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    - 새 항목:
        > Server=[server];Database=[database];**Authentication=SqlPassword**;UID=[username];PWD=[password];Encrypt=yes
    - 사용되지 않음:
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface-sspi"></a>SSPI(Security Support Provider Interface)를 사용하는 Windows 통합 인증

- `IDataInitialize::GetDataSource`사용:
    - 새 항목:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
    - 사용되지 않음:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Integrated Security=SSPI**;Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    - 새 항목:
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes
    - 사용되지 않음:
        > Server=[server];Database=[database];**Trusted_Connection=yes**;Encrypt=yes

### <a name="azure-active-directory-username-and-password-authentication"></a>Azure Active Directory 사용자 이름 및 암호 인증

- `IDataInitialize::GetDataSource`사용:
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryPassword**;User ID=[username];Password=[password];Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="azure-active-directory-integrated-authentication"></a>Azure Active Directory 통합 인증

- `IDataInitialize::GetDataSource`사용:
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>액세스 토큰을 사용하여 Azure Active Directory 인증

- `IDataInitialize::GetDataSource`사용:
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Access Token=[access token]**;Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    > `DBPROP_INIT_PROVIDERSTRING`를 통해 액세스 토큰을 제공하는 것은 지원되지 않습니다.

### <a name="azure-active-directory-interactive-authentication"></a>Azure Active Directory 대화형 인증

- `IDataInitialize::GetDataSource`사용:
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryInteractive**;User ID=[username];Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryInteractive**;UID=[username];Encrypt=yes

### <a name="azure-active-directory-managed-identity-authentication"></a>Azure Active Directory 관리 ID 인증

- `IDataInitialize::GetDataSource`사용:
    - 사용자가 할당한 관리형 ID:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryMSI**;User ID=[Object ID];Use Encryption for Data=true
    - 시스템이 할당한 관리형 ID:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryMSI**;Use Encryption for Data=true
- `DBPROP_INIT_PROVIDERSTRING`사용:
    - 사용자가 할당한 관리형 ID:
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryMSI**;UID=[Object ID];Encrypt=yes
    - 시스템이 할당한 관리형 ID:
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryMSI**;Encrypt=yes

## <a name="code-samples"></a>코드 샘플

다음 샘플에서는 연결 키워드를 사용하여 Azure Active Directory에 연결하는 데 필요한 코드를 보여 줍니다. 

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
- [OAuth 2.0 코드 권한 부여 흐름을 사용하여 Azure Active Directory 웹 애플리케이션에 대한 액세스 권한을 부여합니다](/azure/active-directory/azuread-dev/v1-protocols-oauth-code).

- SQL Server에 대한 [Azure Active Directory 인증](/azure/azure-sql/database/authentication-aad-overview)에 대해 자세히 알아보세요.

- OLE DB 드라이버에서 지원하는 [연결 문자열 키워드](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)를 사용하여 드라이버 연결을 구성합니다.