---
title: '자습서: 보안 Enclave를 사용한 Always Encrypted로 .NET 애플리케이션 개발 | Microsoft Docs'
ms.custom: ''
ms.date: 10/18/2019
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: 82ecd3fa04bbab0a1512ede08ebbc8bfaa3011f9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75244047"
---
# <a name="tutorial-develop-a-net-application-using-always-encrypted-with-secure-enclaves"></a>자습서: 보안 Enclave를 사용한 Always Encrypted로 .NET 애플리케이션 개발

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

이 자습서에서는 [보안 enclave를 사용한 Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-enclaves.md)에 대해 서버 쪽 보안 enclave를 사용하는 데이터베이스 쿼리를 실행하는 간단한 애플리케이션을 개발하는 방법을 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서는 [자습서: SSMS를 사용하여 보안 enclave를 사용한 Always Encrypted 시작](../../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md)에서 이어집니다. 해당 자습서를 완료한 후에 아래 단계를 수행해야 합니다.

또한 Visual Studio(버전 2019 권장)가 필요합니다([https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com)에서 다운로드할 수 있음). 애플리케이션 개발 환경에서 .NET Framework 4.6 이상 또는 .NET Core 2.1 이상을 사용해야 합니다.

## <a name="step-1-set-up-your-visual-studio-project"></a>1단계: Visual Studio 프로젝트 설정

.NET Framework 애플리케이션에서 보안 enclave를 사용한 Always Encrypted를 이용하려면 애플리케이션이 .NET Framework 4.6 이상인지 확인해야 합니다. .NET Core 애플리케이션에서 보안 enclave를 사용한 Always Encrypted를 이용하려면 애플리케이션이 .NET Core 2.1 이상을 대상으로 하는지 확인해야 합니다.

또한 열 마스터 키를 Azure Key Vault에 저장하는 경우에도 애플리케이션을 [Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider NuGet](https://www.nuget.org/packages/Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider)에 통합해야 합니다.

1. Visual Studio를 엽니다.

2. 새 C\# 콘솔 앱(.NET Framework/Core) 프로젝트를 만듭니다.

3. 프로젝트가 .NET Framework 4.6 또는 .NET Core 2.1 이상을 대상으로 하는지 확인합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 속성을 선택한 후 대상 프레임워크를 설정합니다.

4. **도구** (주 메뉴) > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**로 이동하여 다음 NuGet 패키지를 설치합니다. 패키지 관리자 콘솔에서 다음 코드를 실행합니다.

   ```powershell
   Install-Package Microsoft.Data.SqlClient -Version 1.1.0
   ```

5. 열 마스터 키를 저장하는 데 Azure Key Vault를 사용하는 경우 **도구** (주 메뉴) > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**로 이동하여 다음 NuGet 패키지를 설치합니다. 패키지 관리자 콘솔에서 다음 코드를 실행합니다.

   ```powershell
   Install-Package Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider -Version 1.0.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

6. 연결 문자열에서 애플리케이션이 SQL Server와 통신하는 데 사용할 `Attestation Protocol` 및 `Enclave Attestation Url`을 지정합니다.

  ```cs
   Attestation Protocol = HGS; Enclave Attestation Url = http://hgs.bastion.local/Attestation; Column Encryption Setting = Enabled
   ```

## <a name="step-2-implement-your-application-logic"></a>2단계: 애플리케이션 논리 구현

애플리케이션은 **ContosoHR** 데이터베이스([자습서: SSMS를 이용하여 보안 enclave를 사용한 Always Encrypted 시작](../../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md))에 연결되고, **SSN** 열에서 `LIKE` 조건자를 포함하는 쿼리를 실행하고 **Salary** 열에서 범위 비교를 실행합니다.

1. Visual Studio에 의해 생성된 Program.cs 파일의 내용을 다음 코드로 바꿉니다. 사용자 환경의 서버 이름 및 enclave 증명 URL을 사용하여 데이터베이스 연결 문자열을 업데이트합니다. 데이터베이스 인증 설정을 업데이트할 수도 있습니다.

    ```cs
    using System;
    using Microsoft.Data.SqlClient;
    using System.Data;

    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {

                string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Attestation Protocol = HGS; Enclave Attestation Url = http://hgs.bastion.local/Attestation; Integrated Security = true";

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

- [Microsoft .NET Data Provider for SQL Server와 Always Encrypted 사용](sqlclient-support-always-encrypted.md)
- [Always Encrypted를 이용한 Azure Key Vault 공급자 사용을 보여 주는 예제](azure-key-vault-example.md)
- [보안 Enclave가 사용된 Always Encrypted를 이용한 Azure Key Vault 공급자 사용을 보여 주는 예제](azure-key-vault-enclave-example.md)
