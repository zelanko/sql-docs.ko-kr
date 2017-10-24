---
title: CREATE COLUMN MASTER KEY (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/18/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 871acb46898a9a62b25062f69d4e51bf28658f06
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  데이터베이스에 열 마스터 키 메타 데이터 개체를 만듭니다. 보호 하는 데 사용 되는 외부 키 저장소에 저장 된 키를 나타내는 열 마스터 키 메타 데이터 항목 (암호화) 열 암호화 키를 사용 하는 경우는 [상시 암호화 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 기능입니다. 키 회전;에 대 한 여러 열 마스터 키 허용 보안 향상을 위해 키를 주기적으로 변경 합니다. 개체 탐색기를 사용 하 여 키 저장소와 데이터베이스에 해당 메타 데이터 개체에 열 마스터 키를 만들 수 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 PowerShell입니다. 자세한 내용은 참조 [키 관리 개요 상시 암호화를 위한](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)합니다.  
  
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
 되는 열 마스터 키에서에서 인식 될 데이터베이스의 이름이입니다.  
  
 *key_store_provider_name*  
 열 마스터 키를 포함 하는 키 저장소를 캡슐화 하는 클라이언트 쪽 소프트웨어 구성 요소에서 키 저장소 공급자의 이름을 지정 합니다. 상시 암호화 활성화 클라이언트 드라이버 드라이버의 레지스트리 키 저장소 공급자에서 키 저장소 공급자를 조회 하는 키 저장소 공급자 이름을 사용 합니다. 드라이버는 기본 키 저장소에 저장 하는 열 마스터 키로 보호 되는 열 암호화 키를 해독 하는 공급자를 사용 합니다. 일반 텍스트 값 열 암호화 키의 암호화 된 데이터베이스 열에 해당 하는 쿼리 매개 변수를 암호화 하거나 암호화 된 열에서 쿼리 결과 암호를 해독 하려면 사용 됩니다.  
  
 항상 암호화 활성화 클라이언트 드라이버 라이브러리 인기 있는 키 저장소에 대 한 키 저장소 공급자가 포함 됩니다.   
  
사용 가능한 공급자 집합 유형 및 버전의 클라이언트 드라이버에 따라 달라 집니다. 특정 드라이버에 대 한 상시 암호화 설명서를 참조 하십시오.

[사용 하 여 상시 암호화와.NET Framework Provider for SQL Server 응용 프로그램을 개발](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


아래 표 시스템 공급자의 이름이 캡처합니다.  
  
|키 저장소 공급자 이름|기본 키 저장소|  
    |-----------------------------|--------------------------|
    |' MSSQL_CERTIFICATE_STORE'|Windows 인증서 저장소| 
    |' MSSQL_CSP_PROVIDER'|같은 저장소에 지 원하는 Microsoft CryptoAPI 하드웨어 보안 모듈 (HSM).|
    |' MSSQL_CNG_STORE'|지 원하는 암호화 API 하드웨어 보안 모듈 (HSM) 같은 저장소에: 차세대 합니다.|  
    |' Azure_Key_Vault'|참조 [Azure 키 자격 증명 모음 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
  

 상시 암호화 활성화 클라이언트 드라이버에서 기본 제공 키가 저장소에 열 마스터 키 저장소 공급자를 저장 하기 위해, 사용자 지정 키 저장소 공급자를 구현할 수 있습니다.  사용자 지정 키 저장소 공급자의 이름이 접두사는 'MSSQL_'로 시작할 수 없습니다는 내부용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 키 저장소 공급자입니다. 

  
 key_path  
 열 마스터 키에서 키의 경로 저장 합니다. 키 경로 암호화 하거나 참조 된 열 마스터 키에 의해 (직접) 보호 하는 열에 저장 된 데이터를 해독 하는 각 클라이언트 응용 프로그램의 컨텍스트에서 유효 해야 하 고 클라이언트 응용 프로그램 키에 액세스할 수 있도록 허용 하려면 필요 합니다. 키 경로의 형식은 키 저장소 공급자와 관련 합니다. 다음은 특정 Microsoft 시스템 키 저장소 공급자에 대 한 키 경로 형식을 설명합니다.  
  
-   **공급자 이름:** MSSQL_CERTIFICATE_STORE  
  
     **키 경로 형식을:** *CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     각 항목이 나타내는 의미는 다음과 같습니다.  
  
     *CertificateStoreLocation*  
     인증서 저장소 위치 현재 사용자나 로컬 컴퓨터 여야 합니다. 자세한 내용은 참조 [로컬 컴퓨터 및 현재 사용자 인증서 저장소](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx)합니다.  
  
     *CertificateStore*  
     인증서 저장소 이름에 예를 들어 '내'.  
  
     *CertificateThumbprint*  
     인증서 지문입니다.  
  
     **예:**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   **공급자 이름:** MSSQL_CSP_PROVIDER  
  
     **키 경로 형식을:** *ProviderName*/*KeyIdentifier*  
  
     각 항목이 나타내는 의미는 다음과 같습니다.  
  
     *ProviderName*  
     암호화 서비스 공급자 (CSP)를 열 마스터 키 저장소에 대 한, CAPI를 구현 하는 이름입니다. 키 저장소로 HSM을 사용 하는 경우 HSM 공급 업체에 문의 CSP의 이름 이어야 합니다를 제공 합니다. 클라이언트 컴퓨터에 공급자를 설치 합니다.  
  
     *KeyIdentifier*  
     키의 식별자를 키 저장소를 열 마스터 키로 사용 됩니다.  
  
     **예:**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **공급자 이름:** MSSQL_CNG_STORE  
  
     **키 경로 형식을:** *ProviderName*/*KeyIdentifier*  
  
     각 항목이 나타내는 의미는 다음과 같습니다.  
  
     *ProviderName*  
     저장소 공급자 KSP (키)를 암호화를 구현 하는 이름: CNG (Next Generation) API 열 마스터 키 저장소에 대 한 합니다. 키 저장소로 HSM을 사용 하는 경우 HSM 공급 업체에 문의 KSP의 이름 이어야 합니다를 제공 합니다. 공급자는 클라이언트 컴퓨터에 설치 해야 합니다.  
  
     *KeyIdentifier*  
     키의 식별자를 키 저장소를 열 마스터 키로 사용 됩니다.  
  
     **예:**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **공급자 이름:** AZURE_KEY_STORE  
  
     **키 경로 형식을:** *KeyUrl*  
  
     각 항목이 나타내는 의미는 다음과 같습니다.  
  
     *Keyurl은*  
     Azure 키 자격 증명 모음의 키의 URL


예:
 
`N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700'`  
  
## <a name="remarks"></a>주의  

열 마스터 키 메타 데이터 항목을 만드는 그래야를 해당 데이터베이스와 상시 암호화를 사용 하 여 데이터베이스의 모든 열을 암호화할 수 전에 열 암호화 키 메타 데이터 항목을 만들 수 있습니다. 참고에, 메타 데이터에 열 마스터 키 항목 (SQL Server) 외부 열을 외부 키 저장소에 저장 해야 하는 실제 열 마스터 키로 포함 되지 않습니다. 키 저장소 공급자 이름 및 메타 데이터에 열 마스터 키 경로 열 마스터 키로 암호화 된 열 암호화 키의 암호를 해독 하 고 암호화 된 열을 쿼리 하는 열 마스터 키를 사용 하려면 클라이언트 응용 프로그램에 대 한 유효 해야 합니다.


  
## <a name="permissions"></a>Permissions  
 필요는 **ALTER ANY COLUMN MASTER KEY** 권한.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-column-master-key"></a>1. 열 마스터 키 만들기  
 열 마스터 키에 액세스 하려면 MSSQL_CERTIFICATE_STORE 공급자를 사용 하는 클라이언트 응용 프로그램에 대 한 인증서 저장소에 저장 하는 열 마스터 키에 대 한 열 마스터 키 메타 데이터 항목을 만드는 중입니다.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 MSSQL_CNG_STORE 공급자를 사용 하는 클라이언트 응용 프로그램에서 액세스 하는 열 마스터 키에 대 한 열 마스터 키 메타 데이터 항목을 만드는 중입니다.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 열 마스터 키에 액세스할 수 AZURE_KEY_VAULT 공급자를 사용 하는 클라이언트 응용 프로그램에 대 한 Azure 주요 자격 증명에 저장 된 열 마스터 키를 만드는 중입니다.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 사용자 지정 열 마스터 키 저장소에 저장 하는 CMK 만드는 중입니다.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
  
## <a name="see-also"></a>관련 항목:
 
* [DROP COLUMN MASTER key&#40; Transact SQL &#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys(Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [상시 암호화를 위한 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  

