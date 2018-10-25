---
title: '자습서: SSMS를 사용하여 보안 Enclave를 사용한 Always Encrypted 시작 | Microsoft Docs'
ms.custom: ''
ms.date: 10/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 5a8f0b9a18627da1e7d407b396686cb756ca5a4b
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48852115"
---
# <a name="tutorial-getting-started-with-always-encrypted-with-secure-enclaves-using-ssms"></a>자습서: SSMS를 사용하여 보안 Enclave를 사용한 Always Encrypted 시작
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 [보안 Enclave를 사용한 Always Encrypted](encryption/always-encrypted-enclaves.md)를 시작하는 방법을 설명합니다. 다음이 설명됩니다.
- 보안 Enclave를 사용한 Always Encrypted를 테스트 및 평가하기 위한 단순 환경을 만드는 방법
- SSMS(SQL Server Management Studio)를 사용하여 암호화된 열에 대해 데이터를 미리 암호화하고 리치 쿼리를 실행하는 방법

## <a name="prerequisites"></a>사전 요구 사항

보안 Enclave를 사용한 Always Encrypted를 시작하려면 2대 이상의 컴퓨터(가상 머신 가능)가 필요합니다.

- SQL Server 및 SSMS를 호스트할 SQL Server 컴퓨터
- Enclave 증명에 필요한 호스트 보호 서비스를 실행할 HGS 컴퓨터

### <a name="sql-server-computer-requirements"></a>SQL Server 컴퓨터 요구 사항

- [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] 이상
- Windows 10 Enterprise 버전 1809 또는 Windows Server 2019 Datacenter
- [SSMS(SQL Server Management Studio) 18.0 이상](../../ssms/download-sql-server-management-studio-ssms.md).

또는 다른 머신에 SSMS를 설치할 수 있습니다.

>[!WARNING] 
>프로덕션 환경에서는 SSMS 또는 다른 도구를 사용하여 Always Encrypted 키를 확인하거나 SQL Server 컴퓨터에서 암호화된 데이터에 대해 쿼리를 실행하면 안 됩니다. 이렇게 하면 Always Encrypted를 사용하는 목적이 감소하거나 완전히 무산될 수 있기 때문입니다.

### <a name="hgs-computer-requirements"></a>HGS 컴퓨터 요구 사항

- Windows Server 2019 Standard 또는 Datacenter Edition
- CPU 2개
- 8GB RAM
- 100GB 저장소

>[!NOTE]
>시작하기 전에 HGS 컴퓨터를 도메인에 가입하면 안 됩니다.

## <a name="step-1-configure-the-hgs-computer"></a>1단계: HGS 컴퓨터 구성

이 단계에서는 호스트 키 증명을 지원하는 호스트 보호 서비스를 실행하도록 HGS 컴퓨터를 구성합니다.

1. 관리자(로컬 관리자) 권한으로 HGS 컴퓨터에 로그인하고, 관리자 권한의 Windows PowerShell 콘솔을 열고, 다음 명령을 실행하여 호스트 보호 서비스 역할을 추가합니다.

   ```powershell
   Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
   ```

2. HGS 컴퓨터가 다시 부팅되면 관리자 계정으로 다시 로그인하고, 관리자 권한의 Windows PowerShell 콘솔을 열고, 다음 명령을 실행하여 호스트 보호 서비스를 설치하고 해당 도메인을 구성합니다. 여기서 지정한 암호는 Active Directory의 디렉터리 서비스 복구 모드 암호에만 적용되며, 관리자 계정의 로그인 암호는 변경하지 않습니다. -HgsDomainName에 원하는 도메인 이름을 지정할 수 있습니다.

   ```powershell
   $adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force
   Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
   ```

3. 컴퓨터가 다시 부팅되면 관리자 계정(이제 도메인 관리자임)으로 로그인하고, 관리자 권한의 Windows PowerShell 콘솔을 연 다음, HGS 인스턴스의 호스트 키 증명을 구성합니다. 

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey  
   ```

4. 다음 명령을 실행하여 HGS 컴퓨터의 IP 주소를 찾습니다. 이후 단계에 사용할 수 있게 이 IP 주소를 저장합니다.

   ```powershell
   Get-NetIPAddress  
   ```

>[!NOTE]
>또는 DNS 이름으로 HGS 컴퓨터를 참조하려는 경우 회사 DNS 서버에서 새 HGS 도메인 컨트롤러로 전달자를 설정할 수 있습니다.  

## <a name="step-2-configure-the-sql-server-computer-as-a-guarded-host"></a>2단계: SQL Server 컴퓨터를 보호된 호스트로 구성
이 단계에서는 호스트 키 증명을 사용하여 SQL Server 컴퓨터를 HGS에 등록된 보호된 호스트로 구성합니다.
>[!NOTE]
>호스트 키 증명은 테스트 환경에서만 사용하는 것이 좋습니다. 프로덕션 환경에서는 TPM 증명을 사용해야 합니다.

1. 관리자 권한으로 SQL Server 컴퓨터에 로그인하고, 관리자 권한의 Windows PowerShell 콘솔을 연 다음, 보호된 호스트 기능을 설치하고 Hyper-V(아직 설치되지 않은 경우)도 설치합니다.

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
   ```

2. Hyper-V 설치를 완료하라는 메시지가 표시되면 SQL Server 컴퓨터를 다시 시작합니다.
3. 아래 변수 값을 검색하여 SQL Server 컴퓨터의 이름을 확인합니다.

   ```powershell
   $env:computername 
   ```

4. SQL Server 컴퓨터에 관리자 권한으로 다시 로그인하고, 관리자 권한의 Windows PowerShell 콘솔을 열고 고유한 호스트 키를 생성한 다음, 결과 공개 키를 파일로 내보냅니다.

   ```powershell
   Set-HgsClientHostKey 
   Get-HgsClientHostKey -Path $HOME\Desktop\hostkey.cer
   ```

5. 이전 단계에서 생성한 호스트 키 파일을 HGS 머신에 복사합니다. 아래 지침에서는 파일 이름이 hostkey.cer이고 HGS 머신의 데스크톱으로 복사 중이라고 가정합니다.
6. HGS 컴퓨터에서 관리자 권한의 Windows PowerShell 콘솔을 열고 HGS에 SQL Server 컴퓨터의 호스트 키를 등록합니다.

   ```powershell
   Add-HgsAttestationHostKey -Name <your SQL Server computer name> -Path $HOME\Desktop\hostkey.cer
   ```

7. SQL Server 컴퓨터의 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행하여 증명할 위치를 SQL Server 컴퓨터에 알려 줍니다. HGS 컴퓨터의 IP 주소 또는 DNS 이름을 지정해야 합니다. 

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl http://<IP address or DNS name>/Attestation -KeyProtectionServerUrl http://<IP address or DNS name>/KeyProtection/  
   ```

위 명령의 결과는 AttestationStatus = Passed를 표시해야 합니다.

HostUnreachable 오류가 발생하면 SQL Server 컴퓨터가 HGS와 통신할 수 없음을 의미합니다. HGS 컴퓨터를 ping할 수 있는지 확인합니다.

UnauthorizedHost 오류는 공개 키가 HGS 서버에 등록되지 않았음을 나타냅니다. 5단계와 6단계를 반복하여 이 오류를 해결하세요.

모든 방법이 실패하면 Clear-HgsClientHostKey를 실행하고 4-7단계를 반복합니다.

## <a name="step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server"></a>3단계: SQL Server에서 보안 Enclave를 사용한 Always Encrypted 사용

이 단계에서는 SQL Server 인스턴스에서 보안 Enclave를 사용한 Always Encrypted 기능을 사용하도록 설정합니다.

1. SSMS를 열고 SQL Server 인스턴스에 sysadmin으로 연결한 다음, 새 쿼리 창을 엽니다.
2. 보안 Enclave 형식을 VBS로 구성합니다.

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1
   RECONFIGURE
   ```

3. 이전 변경 내용을 적용하려면 SQL Server 인스턴스를 다시 시작합니다. 개체 탐색기에서 인스턴스를 마우스 오른쪽 단추로 클릭하고 다시 시작을 선택하여 SSMS에서 해당 인스턴스를 다시 시작합니다. 인스턴스가 다시 시작되면 다시 연결합니다.

4. 이제 다음 쿼리를 실행하여 보안 Enclave가 로드되는지 확인합니다.

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type'
   ```

    쿼리는 다음과 같은 행을 반환해야 합니다.  

    | NAME                           | value | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | 열 암호화 Enclave 형식 | 1     | 1              |

5. 암호화된 열에 대해 리치 계산을 사용하도록 설정하려면 다음 쿼리를 실행합니다.

   ```sql
   DBCC traceon(127,-1)
   ```

    > [!NOTE]
    > 리치 계산은 [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)]에서 기본적으로 사용되지 않도록 설정됩니다. SQL Server 인스턴스를 다시 시작한 후에 매번 위의 문을 사용하여 리치 계산을 사용하도록 설정해야 합니다.

## <a name="step-4-create-a-sample-database"></a>4단계: 예제 데이터베이스 만들기
이 단계에서는 나중에 암호화할 일부 예제 데이터가 포함된 데이터베이스를 만듭니다.

1. SSMS를 사용하여 SQL Server 인스턴스에 연결합니다.
2. 이름이 ContosoHR인 새 데이터베이스를 만듭니다.

    ```sql
    CREATE DATABASE [ContosoHR] COLLATE Latin1_General_BIN2
    ```

3. 새로 만든 데이터베이스에 연결되어 있는지 확인합니다. 이름이 Employees인 새 테이블을 만듭니다.

    ```sql
    CREATE TABLE [dbo].[Employees]
    (
        [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
        [SSN] [char](11) NOT NULL,
        [FirstName] [nvarchar](50) NOT NULL,
        [LastName] [nvarchar](50) NOT NULL,
        [Salary] [money] NOT NULL
    ) ON [PRIMARY]
    GO
    ```

4. Employees 테이블에 몇 개의 직원 레코드를 추가합니다.

    ```sql
    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('795-73-9838'
            , N'Catherine'
            , N'Abel'
            , $31692)
    GO

    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('990-00-6818'
            , N'Kim'
            , N'Abercrombie'
            , $55415)
    GO
    ```

## <a name="step-5-provision-enclave-enabled-keys"></a>5단계: Enclave 사용 키 프로비전

이 단계에서는 Enclave 계산을 허용하는 열 마스터 키 및 열 암호화 키를 만듭니다.

1. SSMS를 사용하여 데이터베이스에 연결합니다.
2. **개체 탐색기**에서 데이터베이스를 확장하고 **보안** > **Always Encrypted 키**로 이동합니다.
3. 새 Enclave 사용 열 마스터 키를 프로비전합니다.
    1. **Always Encrypted 키**를 마우스 오른쪽 단추로 클릭하고 **새 열 마스터 키...** 를 선택합니다.
    2. 열 마스터 키 이름 CMK1을 선택합니다.
    3. **Windows 인증서 저장소(현재 사용자 또는 로컬 컴퓨터)** 또는 **Azure Key Vault**를 선택해야 합니다.
    4. **Enclave 계산 허용**을 선택합니다.
    5. Azure Key Vault를 선택한 경우 Azure에 로그인하고 Key Vault를 선택합니다. Always Encrypted용 Key Vault를 만드는 방법에 대한 자세한 내용은 [Azure Portal에서 Key Vault 관리](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/)를 참조하세요.
    6. 키가 이미 있는 경우 선택하고, 없는 경우 양식의 지침에 따라 새 키를 만듭니다.
    7. **확인**을 선택합니다.

        ![Enclave 계산 허용](encryption/media/always-encrypted-enclaves/allow-enclave-computations.png)

4. 새 Enclave 사용 열 암호화 키를 만듭니다.

    1. **Always Encrypted 키**를 마우스 오른쪽 단추로 클릭하고 **새 열 암호화 키**를 선택합니다.
    2. 새 열 암호화 키의 이름으로 CEK1을 입력합니다.
    3. **열 마스터 키** 드롭다운에서 이전 단계에서 만든 열 마스터 키를 선택합니다.
    4. **확인**을 선택합니다.

## <a name="step-6-encrypt-some-columns-in-place"></a>6단계: 일부 열 미리 암호화

이 단계에서는 서버 쪽 Enclave 내에서 SSN 및 Salary 열에 저장된 데이터를 암호화한 다음, 데이터의 SELECT 쿼리를 테스트합니다.

1. SSMS에서 데이터베이스 연결에 대해 Always Encrypted를 설정한 상태로 새 쿼리 창을 구성합니다.
    1. SSMS에서 새 쿼리 창을 엽니다.
    2. 새 쿼리 창의 아무 곳이나 마우스 오른쪽 단추로 클릭합니다.
    3. 연결 \> 연결 변경을 선택합니다.
    4. **옵션**을 선택합니다. **Always Encrypted** 탭으로 이동한 후 **Always Encrypted 사용**을 선택하고 Enclave 증명 URL을 지정합니다.
    5. **연결**을 선택합니다.
2. SSMS에서 데이터베이스 연결에 대해 Always Encrypted가 해제된 상태로 다른 쿼리 창을 구성합니다.
    1. SSMS에서 새 쿼리 창을 엽니다.
    2. 새 쿼리 창의 아무 곳이나 마우스 오른쪽 단추로 클릭합니다.
    3. 연결 \> 연결 변경을 선택합니다.
    4. **옵션**을 선택합니다. **Always Encrypted** 탭으로 이동한 후 **Always Encrypted 사용**이 선택되어 있지 않은지 확인합니다.
    5. **연결**을 선택합니다.
3. SSN 및 Salary 열을 암호화합니다. Always Encrypted가 설정된 쿼리 창에서 다음 문을 붙여넣고 실행합니다.

    ```sql
    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [SSN] [char] (11)
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON)
    GO
    DBCC FREEPROCCACHE
    GO

    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [Salary] [money]
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON)
    GO
    DBCC FREEPROCCACHE
    GO
    ```

4. SSN 및 Salary 열이 지금 암호화되었는지 확인하려면 Always Encrypted가 해제된 쿼리 창에서 아래 문을 붙여넣고 실행합니다. 쿼리 창은 SSN 및 Salary 열의 암호화된 값을 반환해야 합니다. Always Encrypted가 설정된 쿼리 창에서 동일한 쿼리를 시도하여 데이터가 암호 해독되어 있는지 확인합니다.

    ```sql
    SELECT * FROM [dbo].[Employees]
    ```

## <a name="step-7-run-rich-queries-against-encrypted-columns"></a>7단계: 암호화된 열에 대해 리치 쿼리 실행

이제 암호화된 열에 대해 리치 조회를 실행할 수 있습니다. 일부 쿼리 처리는 서버 쪽 Enclave 내에서 수행됩니다. 

1. Always Encrypted에 대해 매개 변수화 사용
    1. SSMS의 주 메뉴에서 **쿼리**를 선택합니다.
    2. **쿼리 옵션...** 을 선택합니다.
    3. **실행** > **고급**으로 이동합니다.
    4. Always Encrypted에 대해 매개 변수화 사용을 선택하거나 선택 취소합니다.
    5. 확인을 선택합니다.
2. Always Encrypted가 설정된 쿼리 창에서 다음 쿼리를 붙여넣고 실행합니다. 이 쿼리는 지정된 검색 기준에 맞는 일반 텍스트 값 및 행을 반환해야 합니다.

    ```sql
    DECLARE @SSNPattern [char](11) = '%6818'
    DECLARE @MinSalary [money] = $1000
    SELECT * FROM [dbo].[Employees]
    WHERE SSN LIKE @SSNPattern AND [Salary] >= @MinSalary;
    ```

## <a name="next-steps"></a>Next Steps
다른 사용 사례에 대한 내용은 [보안 Enclave를 사용한 Always Encrypted 구성](encryption/configure-always-encrypted-enclaves.md)을 참조하세요. 다음을 수행해 볼 수도 있습니다.

- [TPM 증명 구성](https://docs.microsoft.com/en-us/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode)
- [HGS 인스턴스에 대해 HTTPS 구성](https://docs.microsoft.com/en-us/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-https)
- 암호화된 열에 대해 리치 쿼리를 실행하는 응용 프로그램 개발
