---
title: SQL Server Management Studio를 사용하여 Always Encrypted 키 프로비저닝 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 13bb5944c5907f3bebc9f01eb969b4b8979f8c97
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78338177"
---
# <a name="provision-always-encrypted-keys-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Always Encrypted 키 프로비저닝
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

이 문서에서는 [SSMS(SQL Server Management Studio)](../../../ssms/download-sql-server-management-studio-ssms.md)를 사용하여 Always Encrypted 키의 열 마스터 키와 열 암호화 키를 프로비저닝하는 방법을 설명합니다.

모범 사례, 권장 사항 및 중요한 보안 고려 사항을 비롯한 Always Encrypted 키 관리의 개요는 [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.

<a name="provisioncmk"></a>
## <a name="provision-column-master-keys-with-the-new-column-master-key-dialog"></a>새 열 마스터 키 대화 상자를 사용하여 열 마스터 키 프로비저닝

**새 열 마스터 키** 대화 상자에서 열 마스터 키를 생성하거나 키 저장소를 통해 기존 키를 선택하고 데이터베이스에서 생성된 키 또는 선택한 키에 대한 열 마스터 키 메타데이터를 만들 수 있습니다.

1.  **개체 탐색기**를 사용하여 데이터베이스 아래의 **보안>상시 암호화 키** 폴더로 이동합니다.
2.  **열 마스터 키** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 열 마스터 키...** 를 선택합니다. 
3.  **새 열 마스터 키** 대화 상자에서 열 마스터 키 메타데이터 개체의 이름을 입력합니다.
4.  키 저장소를 선택합니다.
    - **인증서 저장소 - 현재 사용자** – 개인 저장소인 Windows 인증서 저장소의 현재 사용자 인증서 저장소 위치를 나타냅니다. 
    - **인증서 저장소 - 로컬 컴퓨터** – Windows 인증서 저장소의 로컬 컴퓨터 인증서 저장소 위치를 나타냅니다. 
    - **Azure Key Vault** - Azure에 로그인해야 합니다(**로그인** 클릭). 로그인하면 Azure 구독 및 주요 자격 증명 모음 중 하나를 선택할 수 있습니다.
    - **KSP(키 저장소 공급자)** – CNG(암호화 서비스 공급자) API를 구현하는 KSP(키 저장소 공급자)를 통해 액세스할 수 있는 키 저장소를 나타냅니다. 일반적으로 이 유형의 저장소는 HSM(하드웨어 보안 모듈)입니다. 이 옵션을 선택한 후 KSP를 선택해야 합니다. 기본적으로**Microsoft 소프트웨어 키 저장소 공급자** 가 선택되어 있습니다. HSM에 저장된 열 마스터 키를 사용하려는 경우 디바이스에 대해 KSP를 선택합니다(대화 상자를 열기 전에 컴퓨터에 설치 및 구성해야 함).
    -   **CSP(암호화 서비스 공급자)** - CAPI(암호화 API)를 구현하는 CSP(암호화 서비스 공급자)를 통해 액세스할 수 있는 키 저장소입니다. 일반적으로 이러한 저장소는 HSM(하드웨어 보안 모듈)입니다. 이 옵션을 선택한 후 CSP를 선택해야 합니다.  HSM에 저장된 열 마스터 키를 사용하려는 경우 디바이스에 대해 CSP를 선택합니다(대화 상자를 열기 전에 컴퓨터에 설치 및 구성해야 함).
    
    > [!NOTE]
    > CAPI가 사용되지 않는 API이기 때문에 CAPI(암호화 서비스 공급자) 옵션은 기본적으로 비활성화되어 있습니다. Windows 레지스트리에서 **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** 키 아래에 CAPI Provider Enabled DWORD 값을 만들고 1로 설정하면 사용할 수 있습니다. 키 저장소가 CNG를 지원하는 한, CAPI 대신 CNG를 사용해야 합니다.
   
    위의 키 저장소에 대한 자세한 내용은 [Always Encrypted를 위한 열 마스터 키 만들기 및 저장](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)을 참조하세요.

5. [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)]를 사용 중이며 SQL Server 인스턴스가 보안 Enclave로 구성된 경우, **Enclave 계산 허용** 확인란을 선택하여 마스터 키에서 Enclave를 사용하도록 설정할 수 있습니다. 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)를 참조하세요. 

    > [!NOTE]
    > SQL Server 인스턴스가 보안 Enclave를 사용하여 올바르게 구성되지 않은 경우에는 **Enclave 계산 허용** 확인란이 표시되지 않습니다.

6.  키 저장소에서 기존 키를 선택하거나 **키 생성** 또는 **인증서 생성** 단추를 클릭하여 키 저장소에 키를 만듭니다. 
7.  **확인** 을 클릭하면 새 키가 목록에 표시됩니다. 

대화 상자를 작성하면 SQL Server Management Studio에서 데이터베이스에 열 마스터 키에 대한 메타데이터를 만듭니다. 대화 상자에서 이 작업을 위해 [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 문을 생성하고 실행합니다.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

Enclave를 사용하도록 설정된 열 마스터 키를 구성 중인 경우 SSMS가 열 마스터 키를 사용하여 메타데이터에 서명합니다. 

::: moniker-end

### <a name="permissions-for-provisioning-a-column-master-key"></a>열 마스터 키 프로비저닝을 위한 권한

대화 상자에서 열 마스터 키를 만들려면 데이터베이스에서 *ALTER ANY COLUMN MASTER KEY* 권한이 있어야 합니다. 대화 상자를 사용하여 새 열 마스터 키를 만들거나 키 저장소 만들기에서 기존 키를 사용하려면 키 저장소 및/또는 키에 대한 권한을 요구해야 합니다.
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure Key Vault** - 키를 선택하고 사용하기 위한 *get* 및 *list* 권한과 새 키를 만들기 위한 *create* 권한이 필요합니다. Enclave를 사용하도록 설정된 열 마스터 키를 구성하려면 권한에 *서명*하여 키 메타데이터의 서명을 생성해야 합니다.
- **CNG(키 저장소 공급 기업)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급 기업)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

자세한 내용은 [Always Encrypted를 위한 열 마스터 키 만들기 및 저장](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)을 참조하세요.

<a name="provisioncek"></a> 
## <a name="provision-column-encryption-keys-with-the-new-column-encryption-key-dialog"></a>새 열 암호화 키 대화 상자를 사용하여 열 암호화 키 프로비저닝

**새 열 암호화 키** 대화 상자에서 새 열 암호화 키를 생성하고, 열 마스터 키로 암호화하고, 데이터베이스에 열 암호화 키 메타데이터를 만들 수 있습니다.

1.  **개체 탐색기**를 사용하여 데이터베이스 아래의 **보안/상시 암호화 키** 폴더로 이동합니다.
2.  **열 암호화 키** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 열 암호화 키...** 를 선택합니다. 
3.  **새 열 암호화 키** 대화 상자에서 열 암호화 키 메타데이터 개체의 이름을 입력합니다.
4.  데이터베이스에서 열 마스터 키를 나타내는 메타데이터 개체를 선택합니다.
5.  **확인**을 클릭합니다. 

대화 상자를 작성하면 SQL Server Management Studio에서 새 열 암호화 키를 생성한 다음 사용자가 데이터베이스에서 선택한 열 마스터 키에 대한 메타데이터를 가져옵니다. 그런 다음 SSMS는 열 마스터 키 메타데이터를 사용하여 열 마스터 키가 포함된 키 저장소에 연결하고 열 암호화 키를 암호화합니다. 마지막으로, SSMS는 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 문을 생성하고 실행하여 데이터베이스에 새 열 암호화를 위한 메타데이터 데이터를 만듭니다.

### <a name="permissions-for-provisioning-a-column-encryption-key"></a>열 암호화 키를 프로비저닝할 수 있는 권한

대화 상자에서 열 암호화 키 메타데이터를 만들고 열 마스터 키 메타데이터에 액세스하려면 데이터베이스에서 *ALTER ANY COLUMN ENCRYPTION KEY* 및 *VIEW ANY COLUMN MASTER KEY DEFINITION* 권한이 있어야 합니다.
키 저장소에 액세스하고 열 마스터 키를 사용하려면 키 저장소 또는/및 키에 대한 사용 권한이 필요할 수 있습니다.
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure Key Vault** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 *get*, *unwrapKey*, *wrapKey*, *sign* 및 *verify* 권한이 필요합니다.
- **CNG(키 저장소 공급 기업)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급 기업)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

자세한 내용은 [Always Encrypted를 위한 열 마스터 키 만들기 및 저장](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)을 참조하세요.

## <a name="provision-always-encrypted-keys-using-the-always-encrypted-wizard"></a>Always Encrypted 마법사를 사용하여 Always Encrypted 키 프로비저닝

[Always Encrypted 마법사](../../../relational-databases/security/encryption/always-encrypted-wizard.md)는 선택한 데이터베이스 열을 암호화, 암호 해독 및 다시 암호화하는 도구입니다. 마법사는 이미 구성된 키를 사용할 수 있을 뿐 아니라 새 열 마스터 키와 새 열 암호화를 생성할 수도 있습니다. 

## <a name="next-steps"></a>다음 단계
- [Always Encrypted 마법사를 사용하여 열 암호화 구성](always-encrypted-wizard.md)
- [DAC 패키지로 Always Encrypted를 사용하여 열 암호화 구성](configure-always-encrypted-using-dacpac.md)
- [SQL Server Management Studio를 사용하여 Always Encrypted 키 회전](rotate-always-encrypted-keys-using-ssms.md)
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)
- [SQL Server 가져오기 및 내보내기 마법사에서 Always Encrypted를 사용하여 열에서 또는 열로 데이터 마이그레이션](always-encrypted-migrate-using-import-export-wizard.md)

## <a name="see-also"></a>참고 항목
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Always Encrypted를 위한 열 마스터 키 만들기 및 저장](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [SQL Server Management Studio를 사용하여 Always Encrypted 구성](configure-always-encrypted-using-sql-server-management-studio.md)
- [PowerShell을 사용하여 Always Encrypted 키 프로비저닝](configure-always-encrypted-keys-using-powershell.md)
- [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
