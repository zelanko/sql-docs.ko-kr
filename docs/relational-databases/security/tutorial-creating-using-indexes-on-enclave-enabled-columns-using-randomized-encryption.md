---
title: 임의 암호화를 사용하는 enclave 사용 열의 인덱스(자습서)
description: 이 자습서에서는 SQL Server용 보안 enclave로 Always Encrypted에서 지원되는 임의 암호화를 사용하여 enclave 사용 열에 인덱스를 만들고 사용하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: d8d3b67a8909867760b7ab01ebf860dd2f8dfe48
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467224"
---
# <a name="tutorial-create-and-use-indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>자습서: 임의 암호화를 사용하는 enclave 사용 열에 인덱스 만들기 및 사용
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

이 자습서에서는 [보안 enclave를 사용한 Always Encrypted](encryption/always-encrypted-enclaves.md)에서 지원되는 임의 암호화를 사용하는 enclave 사용 열에 인덱스를 만들고 사용하는 방법을 설명합니다. 다음이 설명됩니다.

- 열을 보호하는 키(열 마스터 키 및 열 암호화 키)에 액세스할 수 있을 때 인덱스를 만드는 방법
- 열을 보호하는 키에 액세스할 수 없을 때 인덱스를 만드는 방법

## <a name="prerequisites"></a>사전 요구 사항

이 자습서는 [자습서: SSMS를 사용하여 보안 enclave를 사용한 Always Encrypted 시작](./tutorial-getting-started-with-always-encrypted-enclaves.md)에서 이어집니다. 해당 자습서를 완료한 후에 아래 단계를 수행해야 합니다.

## <a name="step-1-enable-accelerated-database-recovery-adr-in-your-database"></a>1단계: 데이터베이스에서 ADR(가속 데이터베이스 복구) 사용

데이터베이스에서 ADR을 사용하도록 설정한 다음, 임의 암호화를 사용한 enclave 사용 열에 첫 번째 인덱스를 만드는 것이 좋습니다. [보안 enclave를 사용한 Always Encrypted](./encryption/always-encrypted-enclaves.md)의 [데이터베이스 복구](./encryption/always-encrypted-enclaves.md#database-recovery) 섹션을 참조하세요.

1. 이전 자습서에서 사용한 SSMS 인스턴스를 모두 닫습니다. 그러면 ADR을 사용하는 데 필요한, 열려 있던 데이터베이스 연결도 닫힙니다.
1. SSMS의 새 인스턴스를 연 다음, 데이터베이스 연결에 Always Encrypted를 사용하지 **않고** SQL Server 인스턴스에 sysadmin으로 연결합니다.
    1. SSMS를 시작합니다.
    1. **서버에 연결** 대화 상자에서 서버 이름을 지정하고 인증 방법을 선택한 다음, 자격 증명을 지정합니다.
    1. **옵션 >>** 을 클릭하고 **Always Encrypted** 탭을 선택합니다.
    1. **Always Encrypted 사용(열 암호화)** 확인란이 선택되어 있지 **않은지** 확인합니다.
    1. **연결** 을 선택합니다.
1. 새 쿼리 창을 열고 아래 문을 실행하여 ADR을 사용하도록 설정합니다.

   ```sql
   ALTER DATABASE ContosoHR SET ACCELERATED_DATABASE_RECOVERY = ON;
   ```

## <a name="step-2-create-and-test-an-index-without-role-separation"></a>2단계: 역할 구분 없이 인덱스 만들기 및 테스트

이 단계에서는 암호화된 열에 인덱스를 만들고 테스트합니다. 데이터베이스를 관리하는 DBA와 데이터를 보호하는 키에 액세스할 수 있는 데이터 소유자의 역할을 모두 담당하는 단일 사용자로 작업하겠습니다.

1. 새 SSMS 인스턴스를 연 다음, 데이터베이스 연결에 Always Encrypted를 **사용** 하여, SQL Server 인스턴스에 연결합니다.
   1. SSMS의 새 인스턴스를 시작합니다.
   1. **서버에 연결** 대화 상자에서 서버 이름을 지정하고 인증 방법을 선택한 다음, 자격 증명을 지정합니다.
   1. **옵션 >>** 을 클릭하고 **Always Encrypted** 탭을 선택합니다.
   1. **Always Encrypted 사용(열 암호화)** 확인란을 선택하고 enclave 증명 URL(예: ht<span>tp://<   span>hgs.bastion.local/Attestation)을 지정합니다.
   1. **연결** 을 선택합니다.
   1. Always Encrypted 쿼리에 대한 매개 변수화를 사용할 것인지 묻는 메시지가 표시되면 **사용** 을 클릭합니다.
1. Always Encrypted에 대해 매개 변수화를 사용하라는 메시지가 표시되지 않으면 사용되는지 확인합니다.
   1. SSMS의 주 메뉴에서 **도구** 를 선택합니다.
   2. **옵션...** 을 선택합니다.
   3. **쿼리 실행** > **SQL Server** > **고급** 으로 이동합니다.
   4. **Always Encrypted에 대해 매개 변수화 사용** 이 선택되었는지 확인합니다.
   5. **확인** 을 선택합니다.
1. 쿼리 창을 열고 아래 문을 실행하여 **Employees** 테이블의 **LastName** 열을 암호화합니다. 이후 단계에서 해당 열에 인덱스를 만들고 사용하겠습니다.

   ```sql
   USE [ContosoHR];
   GO   
   ALTER TABLE [dbo].[Employees]
   ALTER COLUMN [LastName] [nvarchar](50) COLLATE Latin1_General_BIN2 
   ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
   GO   
   ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
   GO
   ```

1. **LastName** 열에 인덱스를 만듭니다. Always Encrypted를 사용하는 데이터베이스에 연결되었으므로, SSMS 내부 클라이언트 드라이버가 인덱스를 만드는 데 필요한 enclave에 **CEK1**(**LastName** 열을 보호하는 열 암호화 키)을 투명하게 제공합니다.

   ```sql
   USE [ContosoHR];
   GO

   CREATE INDEX IX_LastName ON [Employees] ([LastName])
   INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
   GO
   ```

1. **LastName** 열에 대해 풍부한 쿼리를 실행하고, SQL Server에서 쿼리를 실행할 때 인덱스를 사용하는지 확인합니다.
   1. 동일한 쿼리 창이나 새 쿼리 창에서 도구 모음의 **활성 쿼리 통계 포함** 단추가 켜져 있는지 확인합니다.
   1. 아래 쿼리를 실행합니다.

       ```sql
       USE [ContosoHR];
       GO

       DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
       SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
       GO
      ```

   1. **활성 쿼리 통계** 탭(쿼리 창의 아래쪽 부분)에서 쿼리가 인덱스를 사용하는지 확인합니다.

## <a name="step-3-create-an-index-with-role-separation"></a>3단계: 역할 구분을 사용하여 인덱스 만들기

이 단계에서는 서로 다른 두 사용자를 가정하여 암호화된 열에 인덱스를 만듭니다. 한 사용자는 인덱스를 만들어야 하지만 키에 액세스할 수 없는 DBA입니다. 다른 사용자는 키에 액세스할 수 있는 데이터 소유자입니다.

1. Always Encrypted를 사용하지 **않는** SSMS 인스턴스를 통해 아래 문을 실행하여 **LastName** 열의 인덱스를 삭제합니다.

   ```sql
   USE [ContosoHR];
   GO

   DROP INDEX IX_LastName ON [Employees]; 
   GO
   ```

1. 데이터 소유자(또는 키에 액세스할 수 있는 애플리케이션)로, enclave 내부 캐시에 **CEK1** 을 채웁니다.

   > [!NOTE]
   > **2단계: 역할 구분 없이 인덱스 만들기 및 테스트** 후에 SQL Server 인스턴스를 다시 시작하지 않은 경우, **CEK1** 이 캐시에 이미 있기 때문에 이 단계는 중복됩니다. 여기서는 enclave에 키가 없는 경우 데이터 소유자가 enclave에 키를 제공할 수 있는 방법을 보여 주기 위해 추가되었습니다.

   1. Always Encrypted를 **사용** 하는 SSMS 인스턴스의 쿼리 창에서 아래 문을 실행합니다. 이 문은 모든 enclave 사용 열 암호화 키를 enclave로 보냅니다. 자세한 내용은 [sp_enclave_send_keys](../system-stored-procedures/sp-enclave-send-keys-sql.md)를 참조하세요.

        ```sql
        USE [ContosoHR];
        GO

        EXEC sp_enclave_send_keys;
        GO
        ```

   1. 위의 저장 프로시저를 실행하는 대신, **LastName** 열에 대해 enclave를 사용하는 DML 쿼리를 실행할 수 있습니다. 그러면 enclave에 **CEK1** 만 채워집니다.

        ```sql
        USE [ContosoHR];
        GO

        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

1. DBA로 인덱스를 만듭니다.
    1. Always Encrypted를 사용하지 **않는** SSMS 인스턴스의 쿼리 창에서 아래 문을 실행합니다.

        ```sql
        USE [ContosoHR];
        GO

        CREATE INDEX IX_LastName ON [Employees] ([LastName])
        INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
        GO
        ```

1. 데이터 소유자로 **LastName** 열에 대해 풍부한 쿼리를 실행하고, SQL Server에서 쿼리를 실행할 때 인덱스를 사용하는지 확인합니다.
   1. Always Encrypted를 **사용** 하는 SSMS 인스턴스에서 기존 쿼리 창을 선택하거나 새 쿼리 창을 열고, 도구 모음의 **활성 쿼리 통계 포함** 단추가 켜져 있는지 확인합니다.
   1. 아래 쿼리를 실행합니다. 

        ```sql
        USE [ContosoHR];
        GO

        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

   1. **활성 쿼리 통계**(쿼리 창의 아래쪽 부분)에서 쿼리가 인덱스를 사용하는지 확인합니다.

## <a name="next-steps"></a>다음 단계
- [자습서: 보안 enclave를 사용한 Always Encrypted를 이용하여 .NET Framework 애플리케이션 개발](tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)

## <a name="see-also"></a>참고 항목
- [보안 Enclave를 사용한 Always Encrypted를 사용하여 열에 인덱스 만들기 및 사용](encryption/always-encrypted-enclaves-create-use-indexes.md)
