---
description: '자습서: 보안 enclave를 사용한 Always Encrypted를 이용하여 .NET Framework 애플리케이션 개발'
title: '자습서: 보안 enclave를 사용한 Always Encrypted를 이용하여 .NET Framework 애플리케이션 개발 | Microsoft Docs'
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: cd75e0a63ebbfbf6a5749939442b8b8a2e964d92
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88403799"
---
# <a name="tutorial-develop-a-net-framework-application-using-always-encrypted-with-secure-enclaves"></a>자습서: 보안 enclave를 사용한 Always Encrypted를 이용하여 .NET Framework 애플리케이션 개발
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

이 자습서에서는 [보안 enclave를 사용한 Always Encrypted](encryption/always-encrypted-enclaves.md)에 대해 서버 쪽 보안 enclave를 사용하는 데이터베이스 쿼리를 실행하는 간단한 애플리케이션을 개발하는 방법을 알아봅니다. 

## <a name="prerequisites"></a>필수 구성 요소
이 자습서는 [자습서: SSMS를 사용하여 보안 enclave를 사용한 Always Encrypted 시작](./tutorial-getting-started-with-always-encrypted-enclaves.md)에서 이어집니다. 해당 자습서를 완료한 후에 아래 단계를 수행해야 합니다.

또한 Visual Studio(버전 2019 권장)가 필요합니다([https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com)에서 다운로드할 수 있음). 애플리케이션 개발 컴퓨터가 .NET Framework 4.7.2 이상을 실행해야 합니다.

## <a name="step-1-set-up-your-visual-studio-project"></a>1단계: Visual Studio 프로젝트 설정

.NET Framework 애플리케이션에서 보안 Enclave를 사용한 Always Encrypted를 사용하려면 .NET Framework 4.7.2에서 애플리케이션을 빌드하고 [Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders)에 통합해야 합니다. 또한 열 마스터 키를 Azure Key Vault에 저장하는 경우에도 애플리케이션을 [Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider) 버전 2.2.0 이상에 통합해야 합니다. 

1. Visual Studio를 엽니다.

2. 새 C\# 콘솔 앱(.NET Framework) 프로젝트를 만듭니다.

3. 프로젝트가 .NET Framework 4.7.2 이상을 대상으로 하는지 확인합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 속성을 선택한 후 대상 프레임워크를 .NET Framework 4.7.2로 설정합니다.

4. **도구** (주 메뉴) > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**로 이동하여 다음 NuGet 패키지를 설치합니다. 패키지 관리자 콘솔에서 다음 코드를 실행합니다.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. 열 마스터 키를 저장하는 데 Azure Key Vault를 사용하는 경우 **도구** (주 메뉴) > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**로 이동하여 다음 NuGet 패키지를 설치합니다. 패키지 관리자 콘솔에서 다음 코드를 실행합니다.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

7. 프로젝트의 App.config 파일을 엽니다.

8. \<configuration\> 섹션을 찾아 \<configSections\> 섹션을 추가하거나 업데이트합니다.

   a. \<configuration\> 섹션에 \<configSections\> 섹션이 포함되어 있지 **않는** 경우 \<configuration\> 바로 아래에 다음 콘텐츠를 추가합니다.
   
      ```xml
      <configSections>
         <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </configSections>
      ```
   b. \<configruation\> 섹션에 이미 \<configSections\> 섹션이 있는 경우 \<configSections\> 내에 다음 줄을 추가합니다.

   ```xml
   <section name="SqlColumnEncryptionEnclaveProviders"  type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data,  Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" /\>
   ```

9. 구성 섹션 내의 \<configSections\> 아래에서 VBS Enclave를 증명하고 상호 작용하는 데 사용할 Enclave 공급자를 지정하는 다음 섹션을 추가합니다.

   ```xml
   <SqlColumnEncryptionEnclaveProviders>
       <providers>
           <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
       </providers>
   </SqlColumnEncryptionEnclaveProviders>
   ```

다음은 간단한 콘솔 애플리케이션에 대한 app.config 파일의 전체 예제입니다.
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
  </configSections>
  <SqlColumnEncryptionEnclaveProviders>
    <providers>
      <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
    </providers>
  </SqlColumnEncryptionEnclaveProviders>
  <startup> 
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
  </startup>
</configuration>
```
## <a name="step-2-implement-your-application-logic"></a>2단계: 애플리케이션 논리 구현
애플리케이션은 **ContosoHR** 데이터베이스([자습서: SSMS를 사용하여 보안 enclave를 사용한 Always Encrypted 시작](tutorial-getting-started-with-always-encrypted-enclaves.md))에 연결되고, **SSN** 열에서 `LIKE` 조건자를 포함하는 쿼리를 실행하고 **Salary** 열에서 범위 비교를 실행합니다.

1. Visual Studio에 의해 생성된 Program.cs 파일의 내용을 아래 코드로 바꿉니다. 사용자 환경의 서버 이름 및 enclave 증명 URL을 사용하여 데이터베이스 연결 문자열을 업데이트합니다. 데이터베이스 인증 설정을 업데이트할 수도 있습니다.

    ```cs
    using System;
    using System.Data.SqlClient;
    using System.Data;

    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {
    
                string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = http://hgs.bastion.local/Attestation; Integrated Security = true";

                using (SqlConnection connection = new SqlConnection(connectionString))
                {
                    connection.Open();

                    SqlCommand cmd = connection.CreateCommand();
                    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [dbo].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";

                    SqlParameter paramSSNPattern = cmd.CreateParameter();

                    paramSSNPattern.ParameterName = @"@SSNPattern";
                    paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
                    paramSSNPattern.Direction = ParameterDirection.Input;
                    paramSSNPattern.Value = "%1111";
                    paramSSNPattern.Size = 11;

                    cmd.Parameters.Add(paramSSNPattern);

                    SqlParameter MinSalary = cmd.CreateParameter();

                    MinSalary.ParameterName = @"@MinSalary";
                    MinSalary.DbType = DbType.Currency;
                    MinSalary.Direction = ParameterDirection.Input;
                    MinSalary.Value = 900;

                    cmd.Parameters.Add(MinSalary);
                    cmd.ExecuteNonQuery();
    
                    SqlDataReader reader = cmd.ExecuteReader();
                    while (reader.Read())

                    {
                        Console.WriteLine(reader);
                        Console.WriteLine(reader[0] + ", " + reader[1] + ", " + reader[2] + ", " + reader[3]);
                    }   
                    Console.ReadKey();
                }
            }
        }
    }
    ```
2. 애플리케이션을 빌드 및 실행합니다.  

## <a name="see-also"></a>참고 항목
- [.NET Framework Data Provider for SQL Server와 Always Encrypted 사용](encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
