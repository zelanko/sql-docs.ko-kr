---
title: CREATE COLUMN MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a8e383e48532f62b2d81bc412696379e79ba115
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  데이터베이스에 열 마스터 키 메타데이터 개체를 만듭니다. 열 마스터 키 메타데이터 항목은 외부 키 저장소에 저장된 키를 나타내며 [Always Encrypted &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 기능을 사용할 때 열 암호화 키를 보호(암호화)하는 데 사용됩니다. 여러 열 마스터 키는 보안 향상을 위해 해당 키를 정기적으로 변경하고 키 회전을 허용합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 PowerShell에서 개체 탐색기를 사용하여 키 저장소의 열 마스터 키 및 데이터베이스에서 해당 메타데이터 개체를 만들 수 입니다. 자세한 정보는 [상시 암호화를 위한 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
         )   
[;]  
```  
  
## <a name="arguments"></a>인수  
 *key_name*  
 데이터베이스에서 열 마스터 키를 식별하는 이름입니다.  
  
 *key_store_provider_name*  
 열 마스터 키가 포함된 키 저장소를 캡슐화하는 클라이언트 쪽 소프트웨어 구성 요소인 키 저장소 공급자 이름을 지정합니다. 상시 암호화 기반 클라이언트 드라이버는 키 저장소 공급자 이름을 사용하여 키 저장소 공급자의 드라이버 레지스트리에서 키 저장소 공급자를 조회합니다. 해당 드라이버는 해당 공급자를 사용해 기본 키 저장소에 저장된 열 마스터 키로 보호되는 열 암호화 키를 해독합니다. 열 암호화 키의 일반 텍스트 값은 암호화된 데이터베이스 열에 상응하는 쿼리 매개 변수를 암호화하거나 암호화된 열에서 쿼리 결과를 해독하기 위해 사용됩니다.  
  
 상시 암호화 기반 클라이언트 드라이버 라이브러리에는 인기 있는 키 저장소를 위한 키 저장소 공급자가 포함됩니다.   
  
사용 가능한 공급자 집합은 클라이언트 드라이버의 유형 및 버전에 따라 달라집니다. 특정 드라이버에 대한 상시 암호화 설명서를 참조 하십시오.

[.NET Framework Provider for SQL Server와 상시 암호화를 사용하여 응용 프로그램 개발](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


아래 테이블은 시스템 공급자의 이름을 캡처합니다.  
  
|키 저장소 공급자 이름|기본 키 저장소|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Windows 인증서 저장소| 
    |'MSSQL_CSP_PROVIDER'|Microsoft CryptoAPI를 지원하는 HSM(하드웨어 보안 모듈) 같은 저장소입니다.|
    |'MSSQL_CNG_STORE'|CryptoAPI: Next Generation를 지원하는 HSM 같은 저장소입니다.|  
    |'Azure_Key_Vault'|[Azure Key Vault 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/) 참조|  
  

 상시 암호화 기반 클라이언트 드라이버에서 기본 키 저장소 제공자가 없는 경우 저장소에 열 마스터 키를 저장하기 위해 사용자 지정 키 저장 공급자를 구현할 수 있습니다.  사용자 지정 키 저장소 공급자의 이름은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 키 저장소 공급자용으로 예약된 접두사인 'MSSQL_'로 시작할 수 없습니다. 

  
 key_path  
 열 마스터 키 저장소에서의 키 경로입니다. 키 경로는 참조된 열 마스터 키에 의해 (직접) 보호되는 열에 저장된 데이터를 암호화하거나 해독할 것으로 예상되는 각 클라이언트 응용 프로그램의 컨텍스트에서 유효해야 합니다. 해당 클라이언트 응용 프로그램은 허용돼야 키에 액세스할 수 있습니다. 키 경로의 형식은 키 저장소 공급자에 따라 다릅니다. 다음 목록은 특정 Microsoft 시스템 키 저장소 공급자에 대한 키 경로 형식을 설명합니다.  
  
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
     열 마스터 키 저장소에 대한 CAPI를 구현하는 CSP(암호화 서비스 공급자) 이름입니다. 키 저장소로 HSM을 사용하는 경우 HSM 공급업체가 제공하는 CSP 이름이어야 합니다. 클라이언트 컴퓨터에 공급자를 설치해야 합니다.  
  
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
     마스터 키 저장소에 대한 CNG(차세대 암호화) API를 구현하는 KSP(키 저장소 공급자) 이름입니다. 키 저장소로 HSM을 사용하는 경우 HSM 공급업체가 제공하는 KSP 이름이어야 합니다. 클라이언트 컴퓨터에 공급자를 설치해야 합니다.  
  
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


예:
 
`N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700'`  
  
## <a name="remarks"></a>Remarks  

열 암호화 키 메타데이터 항목을 데이터베이스에서 만들 수 있기 전에 그리고 상시 암호화를 사용하여 데이터베이스의 모든 열을 암호화할 수 있기 전에 열 마스터 키 메타데이터 항목 만들기를 요청합니다. 메타데이터에서 열 마스터 키 항목은 외부 열 키 저장소(SQL Server 외부)에 저장되어야 하는 실제 열 마스터 키를 포함하지 않는다는 점에 유의하십시오. 메타데이터에서 키 저장소 공급자 이름 및 열 마스터 키 경로는 클라이언트 응용 프로그램이 열 마스터 키를 사용해 암호화된 열 암호화 키를 해독하고 암호화된 열을 쿼리하기 위해 열 마스터 키를 사용할 수 있도록 유효해야 합니다.


  
## <a name="permissions"></a>사용 권한  
 **ALTER ANY COLUMN MASTER KEY** 권한을 요구합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-column-master-key"></a>1. 열 마스터 키 만들기  
 MSSQL_CERTIFICATE_STORE 공급자를 사용하는 클라이언트 응용 프로그램이 열 마스터 키에 액세스 하려면 인증서 저장소에 저장되는 열 마스터 키에 대한 열 마스터 키 메타데이터 항목 만들기.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 MSSQL_CNG_STORE 공급자를 사용하는 클라이언트 응용 프로그램에서 액세스하는 열 마스터 키에 대한 열 마스터 키 메타데이터 항목 만들기.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 열 마스터 키에 액세스하기 위해 AZURE_KEY_VAULT 공급자를 사용하는 클라이언트 응용 프로그램에 대한 Azure Key Vault에 저장된 열 마스터 키 만들기.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 사용자 지정 열 마스터 키 저장소에 저장된 CMK 만들기.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
  
## <a name="see-also"></a>참고 항목
 
* [DROP COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys(Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [상시 암호화를 위한 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  
