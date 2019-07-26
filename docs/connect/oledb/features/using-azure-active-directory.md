---
title: Azure Active Directory | 사용 SQL Server에 대 한 Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68213551"
---
# <a name="using-azure-active-directory"></a>Azure Active Directory 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>용도

버전 18.2.1부터 SQL Server 용 Microsoft OLE DB Driver를 사용 하면 OLE DB 응용 프로그램에서 페더레이션 id를 사용 하 여 Azure SQL Database 인스턴스에 연결할 수 있습니다. 새 인증 방법에는 다음이 포함 됩니다.
- Azure Active Directory 로그인 ID 및 암호
- Azure Active Directory 액세스 토큰
- Azure Active Directory 통합 인증
- SQL 로그인 ID 및 암호

> [!NOTE]  
> 다음 Azure Active Directory 옵션을 OLE DB 드라이버와 함께 사용 하는 경우 [SQL Server에 대 한 Active Directory 인증 라이브러리](https://go.microsoft.com/fwlink/?LinkID=513072) 를 설치 했는지 확인 합니다.
> - Azure Active Directory 로그인 ID 및 암호
> - Azure Active Directory 통합 인증
>
> ADAL은 다른 인증 방법이 나 OLE DB 작업에 필요 하지 않습니다.

> [!NOTE]
> `DataTypeCompatibility` (또는 해당 속성)를 `80` 로 설정 하 여 다음과 같은 인증 모드를 사용할 수 **없습니다** .
> - 로그인 ID 및 암호를 사용 하 여 인증 Azure Active Directory
> - 액세스 토큰을 사용 하 여 인증 Azure Active Directory
> - Azure Active Directory 통합 인증

## <a name="connection-string-keywords-and-properties"></a>연결 문자열 키워드 및 속성
Azure Active Directory 인증을 지원 하기 위해 다음과 같은 연결 문자열 키워드가 도입 되었습니다.

|연결 문자열 키워드|연결 속성|설명|
|---               |---                |---        |
|액세스 토큰|SSPROP_AUTH_ACCESS_TOKEN|Azure Active Directory에 인증할 액세스 토큰을 지정 합니다. |
|인증|SSPROP_AUTH_MODE|사용할 인증 방법을 지정합니다.|

새 키워드/속성에 대 한 자세한 내용은 다음 페이지를 참조 하세요.
- [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [초기화 및 권한 부여 속성](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>암호화 및 인증서 유효성 검사
이 섹션에서는 암호화 및 인증서 유효성 검사 동작의 변경 내용에 대해 설명 합니다. 이러한 변경 내용은 새 인증 또는 액세스 토큰 연결 문자열 키워드 (또는 해당 속성)를 사용 하는 경우에 **만** 적용 됩니다.

### <a name="encryption"></a>암호화
보안을 개선 하기 위해 새 연결 속성/키워드가 사용 되는 경우 드라이버는 기본 암호화 값을로 `yes`설정 하 여 재정의 합니다. 재정의는 데이터 원본 개체 초기화 시에 발생 합니다. 암호화가 모든 방법으로 초기화 되기 전에 설정 된 경우 값이 적용 되 고 재정의 되지 않습니다.

> [!NOTE]   
> 를 통해 `IDBInitialize` `IDataInitialize::GetDataSource`인터페이스를 가져오는 응용 프로그램 및 ADO 응용 프로그램에서 인터페이스를 구현 하는 핵심 구성 요소는 명시적으로 암호화 `no`를 기본값인로 설정 합니다. 따라서 새 인증 속성/키워드가이 설정을 준수 하 고 암호화 값은 재정의 **되지 않습니다** . 따라서 이러한 응용 프로그램  을 명시적으로 설정 `Use Encryption for Data=true` 하 여 기본값을 재정의 하는 것이 **좋습니다**.

### <a name="certificate-validation"></a>인증서의 유효성 검사
보안을 개선 하기 위해 새 연결 속성/키워드는 `TrustServerCertificate` **클라이언트 암호화 설정과 별개로**설정 (및 해당 하는 연결 문자열 키워드/속성)을 고려 합니다. 따라서 서버 인증서는 기본적으로 유효성이 검사 됩니다.

> [!NOTE]   
> 레지스트리`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2` 항목의 필드를 `Value` 통해 인증서 유효성 검사를 제어할 수도 있습니다. 유효한 값은 `0` 또는 `1`입니다. OLE DB 드라이버는 레지스트리와 연결 속성/키워드 설정 사이에서 가장 안전한 옵션을 선택 합니다. 즉, 레지스트리/연결 설정 중 하나 이상에서 서버 인증서 유효성 검사를 사용 하도록 설정 하면 드라이버에서 서버 인증서의 유효성을 검사 합니다.

## <a name="gui-additions"></a>GUI 추가
Azure Active Directory 인증을 허용 하도록 드라이버 그래픽 사용자 인터페이스가 향상 되었습니다. 참조 항목:
- [SQL Server 로그인 대화 상자](../help-topics/sql-server-login-dialog.md)
- [UDL(유니버설 데이터 링크) 구성](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>연결 문자열 예
이 섹션에서는 및 `IDataInitialize::GetDataSource` `DBPROP_INIT_PROVIDERSTRING` 속성과 함께 사용할 새로운 및 기존 연결 문자열 키워드의 예를 보여 줍니다.

### <a name="sql-authentication"></a>SQL 인증
- `IDataInitialize::GetDataSource`사용:
    - 새 항목:
        > Provider = MSOLEDBSQL; Data Source = [server]; 초기 카탈로그 = [데이터베이스]; **인증 = SqlPassword**; 사용자 ID = [사용자 이름]; Password = [password]; Data = true에 대 한 암호화 사용
    - 사용되지 않음:
        > Provider = MSOLEDBSQL; Data Source = [server]; 초기 카탈로그 = [데이터베이스]; 사용자 ID = [사용자 이름]; Password = [password]; Data = true에 대 한 암호화 사용
- `DBPROP_INIT_PROVIDERSTRING`사용:
    - 새 항목:
        > Server=[server];Database=[database];**Authentication=SqlPassword**;UID=[username];PWD=[password];Encrypt=yes
    - 사용되지 않음:
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface--sspi"></a>SSPI (Security Support Provider Interface)를 사용 하는 Windows 통합 인증

- `IDataInitialize::GetDataSource`사용:
    - 새 항목:
        > Provider = MSOLEDBSQL; Data Source = [server]; 초기 카탈로그 = [데이터베이스]; **인증 = ActiveDirectoryIntegrated**; Data = true에 대 한 암호화 사용
    - 사용되지 않음:
        > Provider = MSOLEDBSQL; Data Source = [server]; 초기 카탈로그 = [데이터베이스]; **Integrated Security = SSPI**; Data = true에 대 한 암호화 사용
- `DBPROP_INIT_PROVIDERSTRING`사용:
    - 새 항목:
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes
    - 사용되지 않음:
        > Server=[server];Database=[database];**Trusted_Connection=yes**;Encrypt=yes

### <a name="aad-username-and-password-authentication-using-adal"></a>ADAL을 사용 하 여 AAD 사용자 이름 및 암호 인증

- `IDataInitialize::GetDataSource`사용:
    > Provider = MSOLEDBSQL; Data Source = [server]; 초기 카탈로그 = [데이터베이스]; **인증 = ActiveDirectoryPassword**; 사용자 ID = [사용자 이름]; Password = [password]; Data = true에 대 한 암호화 사용
- `DBPROP_INIT_PROVIDERSTRING`사용:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-azure-active-directory-authentication-using-adal"></a>ADAL을 사용 하 여 통합 Azure Active Directory 인증

- `IDataInitialize::GetDataSource`사용:
    > Provider = MSOLEDBSQL; Data Source = [server]; 초기 카탈로그 = [데이터베이스]; **인증 = ActiveDirectoryIntegrated**; Data = true에 대 한 암호화 사용
- `DBPROP_INIT_PROVIDERSTRING`사용:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>액세스 토큰을 사용 하 여 인증 Azure Active Directory

- `IDataInitialize::GetDataSource`사용:
    > Provider = MSOLEDBSQL; Data Source = [server]; 초기 카탈로그 = [데이터베이스]; **액세스 토큰 = [액세스 토큰]** ; Data = true에 대 한 암호화 사용
- `DBPROP_INIT_PROVIDERSTRING`사용:
    > 액세스 토큰 `DBPROP_INIT_PROVIDERSTRING` 제공은 지원 되지 않습니다.

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
- [OAuth 2.0 코드 부여 흐름을 사용 하 여 Azure Active Directory 웹 응용 프로그램에 대 한 액세스 권한을 부여](https://go.microsoft.com/fwlink/?linkid=2072672)합니다.

- SQL Server에 대한 [Azure Active Directory 인증](https://go.microsoft.com/fwlink/?linkid=2073783)에 대해 자세히 알아보세요.

- OLE DB 드라이버에서 지 원하는 [연결 문자열 키워드](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md) 를 사용 하 여 드라이버 연결을 구성 합니다.
