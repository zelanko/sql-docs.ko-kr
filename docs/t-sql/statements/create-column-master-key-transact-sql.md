---
title: CREATE COLUMN MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL13.SWB.NEWCOLUMNMASTERKEYDEF.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEYDEF.GENERAL.F1
- CREATE COLUMN MASTER KEY
- COLUMN MASTER KEY
- CREATE_COLUMN_MASTER_KEY_TSQL
- COLUMN_MASTER_KEY_TSQL
- SQL13.SWB.NEWCOLUMNMASTERKEY.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEY.GENERAL.F1
dev_langs:
- TSQL
helpviewer_keywords:
- column master key definition
- column master key, create
- CREATE COLUMN MASTER KEY statement
- Always Encrypted, create column master key
ms.assetid: f8926b95-e146-4e3f-b56b-add0c0d0a30e
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 17e717fd999109390c001bdab9aeee5629c1a119
ms.sourcegitcommit: ad3b2133585bc14fc6ef8be91f8b74ee2f498b64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2019
ms.locfileid: "56425798"
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

데이터베이스에 열 마스터 키 메타데이터 개체를 만듭니다. 열 마스터 키 메타데이터 항목은 외부 키 저장소에 저장된 키를 나타냅니다. [Always Encrypted&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 기능을 사용할 경우 키가 열 암호화 키를 보호(암호화)합니다. 여러 열 마스터 키는 보안 향상을 위해 정기적으로 키 회전을 허용합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 PowerShell에서 개체 탐색기를 사용하여 키 저장소의 열 마스터 키 및 데이터베이스의 관련 메타데이터 개체를 만듭니다. 자세한 정보는 [상시 암호화를 위한 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 

> [!IMPORTANT]
> Enclave 사용 키를 만들려면(ENCLAVE_COMPUTATIONS 사용) [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)가 필요합니다.

## <a name="syntax"></a>구문  

```  
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
        [,ENCLAVE_COMPUTATIONS (SIGNATURE = signature)]
         )   
[;]  
```  
  
## <a name="arguments"></a>인수  
*key_name*  
데이터베이스에 있는 열 마스터 키의 이름입니다.  
  
*key_store_provider_name*  
키 저장소 공급자의 이름을 지정합니다. 키 저장소 공급자는 열 마스터 키가 포함된 키 저장소를 포함하는 클라이언트 쪽 소프트웨어 구성 요소입니다. 

Always Encrypted를 통해 사용 가능한 클라이언트 드라이버는 다음을 수행합니다.

- 키 저장소 공급자 이름 사용 
- 키 저장소 공급자의 드라이버 레지스트리에서 키 저장소 공급자 검색 

이후 드라이버는 공급자를 사용하여 열 암호화 키의 암호를 해독합니다. 열 암호화 키는 열 마스터 키로 보호됩니다. 열 마스터 키는 기본 키 저장소에 저장됩니다. 열 암호화 키의 일반 텍스트 값은 암호화된 데이터베이스 열에 해당하는 쿼리 매개 변수를 암호화는 데 사용됩니다. 또는 열 암호화 키는 암호화된 열에서 쿼리 결과의 암호를 해독합니다.  
  
상시 암호화 기반 클라이언트 드라이버 라이브러리에는 인기 있는 키 저장소를 위한 키 저장소 공급자가 포함됩니다.   
  
사용 가능한 공급자 세트는 클라이언트 드라이버의 유형 및 버전에 따라 달라집니다. 특정 드라이버에 대한 Always Encrypted 설명서를 참조하세요.

[.NET Framework Provider for SQL Server와 상시 암호화를 사용하여 애플리케이션 개발](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


다음 표는 시스템 공급자의 이름을 보여 줍니다.  
  
|키 저장소 공급자 이름|기본 키 저장소|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Windows 인증서 저장소| 
    |'MSSQL_CSP_PROVIDER'|Microsoft CryptoAPI를 지원하는 HSM(하드웨어 보안 모듈) 같은 저장소입니다.|
    |'MSSQL_CNG_STORE'|Cryptography API: Next Generation을 지원하는 HSM(하드웨어 보안 모듈) 같은 저장소입니다.|  
    |'Azure_Key_Vault'|[Azure Key Vault 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/) 참조|  
  

Always Encrypted 사용 가능 클라이언트 드라이버에서 기본 제공 키 저장소 공급자가 없는 경우 열 마스터 키를 저장하는 사용자 지정 키 저장소 공급자를 설정할 수 있습니다. 사용자 지정 키 저장소 공급자의 이름은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 키 저장소 공급자용으로 예약된 접두사인 'MSSQL_'로 시작할 수 없습니다. 

  
key_path  
열 마스터 키 저장소에서의 키 경로입니다. 키 경로는 데이터를 암호화하거나 암호 해독해야 하는 각 클라이언트 애플리케이션에 대해 유효해야 합니다. 데이터는 참조된 열 마스터 키로 간접적으로 보호되는 열에 저장됩니다. 클라이언트 애플리케이션은 키에 액세스할 권한이 있어야 합니다. 키 경로의 형식은 키 저장소 공급자에 따라 다릅니다. 다음 목록은 특정 Microsoft 시스템 키 저장소 공급자에 대한 키 경로 형식을 설명합니다.  
  
-   **공급자 이름:** MSSQL_CERTIFICATE_STORE  
  
    **키 경로 형식:** *CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     각 항목이 나타내는 의미는 다음과 같습니다.  
  
    *CertificateStoreLocation*  
    현재 사용자나 로컬 컴퓨터여야 하는 인증서 저장소입니다. 자세한 내용은 [로컬 컴퓨터 및 현재 사용자 인증서 저장소](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx)를 참조합니다.  
  
    *CertificateStore*  
    인증서 저장소 이름에 예를 들어 '나의'를 사용합니다.  
  
    *CertificateThumbprint*  
    인증서 지문입니다.  
  
    **예:**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   **공급자 이름:** MSSQL_CSP_PROVIDER  
  
    **키 경로 형식:** *ProviderName*/*KeyIdentifier*  
  
    각 항목이 나타내는 의미는 다음과 같습니다.  
  
    *ProviderName*  
    열 마스터 키 저장소에 대한 CAPI를 구현하는 CSP(암호화 서비스 공급자)의 이름입니다. 키 저장소로 HSM을 사용하는 경우 공급자 이름은 HSM 공급업체가 제공하는 CSP 이름이어야 합니다. 클라이언트 컴퓨터에 공급자를 설치해야 합니다.  
  
    *KeyIdentifier*  
    키의 식별자가 키 저장소에서 열 마스터 키로 사용됩니다.  
  
    **예:**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **공급자 이름:** MSSQL_CNG_STORE  
  
    **키 경로 형식:** *ProviderName*/*KeyIdentifier*  
  
    각 항목이 나타내는 의미는 다음과 같습니다.  
  
    *ProviderName*  
    열 마스터 키 저장소에 대한 CNG(Cryptography: Next Generation) API를 구현하는 KSP(키 저장소 공급자)의 이름입니다. 키 저장소로 HSM을 사용하는 경우 공급자 이름은 HSM 공급업체가 제공하는 KSP 이름이어야 합니다. 클라이언트 컴퓨터에 공급자를 설치해야 합니다.  
  
    *KeyIdentifier*  
    키의 식별자가 키 저장소에서 열 마스터 키로 사용됩니다.  
  
    **예:**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **공급자 이름:** AZURE_KEY_STORE  
  
    **키 경로 형식:** *KeyUrl*  
  
    각 항목이 나타내는 의미는 다음과 같습니다.  
  
    *KeyUrl*  
    Azure Key Vault의 키의 URL

ENCLAVE_COMPUTATIONS  
열 마스터 키를 Enclave 사용 키로 지정합니다. 이 열 마스터 키로 암호화된 모든 열 암호화 키를 서버 쪽 보안 Enclave와 공유하고 Enclave 내의 계산에 사용할 수 있습니다. 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.

*signature*  
이진 리터럴은 ‘키 경로’ 및 ENCLAVE_COMPUTATIONS 설정을 열 마스터 키로 디지털 서명한 결과입니다. 이 서명은 ENCLAVE_COMPUTATIONS가 지정되었는지 여부를 반영합니다. 이 서명은 권한 없는 사용자가 서명된 값을 변경하지 못하도록 보호합니다. Always Encrypted 사용 가능 클라이언트 드라이버는 서명을 확인하고, 서명이 유효하지 않은 경우 애플리케이션에 오류를 반환합니다. 이 서명은 클라이언트 쪽 도구를 사용하여 생성해야 합니다. 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.
  
  
## <a name="remarks"></a>Remarks  

열 암호화 키 메타데이터 항목을 데이터베이스에서 만들기 전에 그리고 Always Encrypted를 사용하여 데이터베이스의 모든 열을 암호화하기 전에 열 마스터 키 메타데이터 항목을 만듭니다. 메타데이터의 열 마스터 키 항목에는 실제 열 마스터 키가 포함되지 않습니다. 열 마스터 키는 외부 열 키 저장소(SQL Server 외부)에 저장되어야 합니다. 메타데이터의 키 저장소 공급자 이름과 열 마스터 키 경로는 클라이언트 애플리케이션에 대해 유효해야 합니다. 클라이언트 애플리케이션은 열 마스터 키를 사용하여 열 암호화 키의 암호를 해독해야 합니다. 열 암호화 키는 열 마스터 키로 암호화됩니다. 또한 클라이언트 애플리케이션은 암호화된 열을 쿼리해야 합니다.


  
## <a name="permissions"></a>Permissions  
**ALTER ANY COLUMN MASTER KEY** 권한을 요구합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-column-master-key"></a>1. 열 마스터 키 만들기  
다음 예제에서는 열 마스터 키의 열 마스터 키 메타데이터 항목을 만듭니다. MSSQL_CERTIFICATE_STORE 공급자를 사용하는 클라이언트 애플리케이션이 열 마스터 키에 액세스할 수 있도록 열 마스터 키가 인증서 저장소에 저장됩니다.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
열 마스터 키의 열 마스터 키 메타데이터 항목을 만듭니다. MSSQL_CNG_STORE 공급자를 사용하는 클라이언트 애플리케이션은 열 마스터 키에 액세스합니다.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
열 마스터 키의 열 마스터 키 메타데이터 항목을 만듭니다. AZURE_KEY_VAULT 공급자를 사용하는 클라이언트 애플리케이션이 열 마스터 키에 액세스할 수 있도록 열 마스터 키가 Azure Key Vault에 저장됩니다.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
열 마스터 키의 열 마스터 키 메타데이터 항목을 만듭니다. 열 마스터 키는 사용자 지정 열 마스터 키 저장소에 저장됩니다.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
### <a name="b-creating-an-enclave-enabled-column-master-key"></a>2. Enclave 사용 열 마스터 키 만들기  
다음 예제에서는 Enclave 사용 가능 열 마스터 키의 열 마스터 키 메타데이터 항목을 만듭니다. MSSQL_CERTIFICATE_STORE 공급자를 사용하는 클라이언트 애플리케이션이 열 마스터 키에 액세스할 수 있도록 Enclave 사용 가능 열 마스터 키가 인증서 저장소에 저장됩니다.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
     ENCLAVE_COMPUTATIONS (SIGNATURE = 0xA80F5B123F5E092FFBD6014FC2226D792746468C901D9404938E9F5A0972F38DADBC9FCBA94D9E740F3339754991B6CE26543DEB0D094D8A2FFE8B43F0C7061A1FFF65E30FDDF39A1B954F5BA206AAC3260B0657232020542419990261D878318CC38EF4E853970ED69A8D4A306693B8659AAC1C4E4109DE5EB148FD0E1FDBBC32F002C1D8199D313227AD689279D8DEEF91064DF122C19C3767C463723AB663A6F8412AE17E745922C0E3A257EAEF215532588ACCBD440A03C7BC100A38BD0609A119E1EF7C5C6F1B086C68AB8873DBC6487B270340E868F9203661AFF0492CEC436ABF7C4713CE64E38CF66C794B55636BFA55E5B6554AF570CF73F1BE1DBD)
  );  
```  
  
Enclave 사용 가능 열 마스터 키의 열 마스터 키 메타데이터 항목을 만듭니다. AZURE_KEY_VAULT 공급자를 사용하는 클라이언트 애플리케이션이 열 마스터 키에 액세스할 수 있도록 Enclave 사용 가능 열 마스터 키가 Azure Key Vault에 저장됩니다.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700');
    ENCLAVE_COMPUTATIONS (SIGNATURE = 0xA80F5B123F5E092FFBD6014FC2226D792746468C901D9404938E9F5A0972F38DADBC9FCBA94D9E740F3339754991B6CE26543DEB0D094D8A2FFE8B43F0C7061A1FFF65E30FDDF39A1B954F5BA206AAC3260B0657232020582413990261D878318CC38EF4E853970ED69A8D4A306693B8659AAC1C4E4109DE5EB148FD0E1FDBBC32F002C1D8199D313227AD689279D8DEEF91064DF122C19C3767C463723AB663A6F8412AE17E745922C0E3A257EAEF215532588ACCBD440A03C7BC100A38BD0609A119E1EF7C5C6F1B086C68AB8873DBC6487B270340E868F9203661AFF0492CEC436ABF7C4713CE64E38CF66C794B55636BFA55E5B6554AF570CF73F1BE1DBD)
  );
```  
  
## <a name="see-also"></a>참고 항목
 
* [DROP COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys(Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [상시 암호화를 위한 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  
