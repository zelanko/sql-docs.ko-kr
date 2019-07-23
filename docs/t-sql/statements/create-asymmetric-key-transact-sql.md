---
title: CREATE ASYMMETRIC KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASYMMETRIC_KEY_TSQL
- CREATE ASYMMETRIC KEY
- CREATE_ASYMMETRIC_KEY_TSQL
- ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], creating
- encryption [SQL Server], asymmetric keys
- CREATE ASYMMETRIC KEY statement
- asymmetric keys [SQL Server]
- cryptography [SQL Server], asymmetric keys
ms.assetid: 141bc976-7631-49f6-82bd-a235028645b1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b017b3cccbce4f993723d24f952eb605ce36a376
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141097"
---
# <a name="create-asymmetric-key-transact-sql"></a>CREATE ASYMMETRIC KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스에서 비대칭 키를 만듭니다.  
  
 이 기능은 Data Tier Application Framework(DACFx)를 사용하는 데이터베이스 내보내기와 호환되지 않습니다. 내보내기 전에 모든 비대칭 키를 삭제해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE ASYMMETRIC KEY asym_key_name   
   [ AUTHORIZATION database_principal_name ]  
   [ FROM <asym_key_source> ]  
   [ WITH <key_option> ] 
   [ ENCRYPTION BY <encrypting_mechanism> ] 
   [ ; ]
  
<asym_key_source>::=  
     FILE = 'path_to_strong-name_file'  
   | EXECUTABLE FILE = 'path_to_executable_file'  
   | ASSEMBLY assembly_name  
   | PROVIDER provider_name  
  
<key_option> ::=  
   ALGORITHM = <algorithm>  
      |  
   PROVIDER_KEY_NAME = 'key_name_in_provider'  
      |  
      CREATION_DISPOSITION = { CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
      { RSA_4096 | RSA_3072 | RSA_2048 | RSA_1024 | RSA_512 }   
  
<encrypting_mechanism> ::=  
    PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>인수  
 *asym_key_name*  
 데이터베이스에 있는 비대칭 키의 이름입니다. 비대칭 키 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 준수해야 하며 데이터베이스 내에서 고유해야 합니다.  

 AUTHORIZATION *database_principal_name*  
 비대칭 키의 소유자를 지정합니다. 소유자는 역할 또는 그룹일 수 없습니다. 이 옵션을 생략하면 소유자가 현재 사용자가 됩니다.  
  
 FROM *asym_key_source*  
 비대칭 키 쌍을 로드할 원본을 지정합니다.  
  
 FILE = '*path_to_strong-name_file*'  
 키 쌍을 로드할 강력한 이름 파일의 경로를 지정합니다. Windows API에서 MAX_PATH를 통해 260자로 제한됩니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 EXECUTABLE FILE = '*path_to_executable_file*'  
 공개 키를 로드할 어셈블리 파일의 경로를 지정합니다. Windows API에서 MAX_PATH를 통해 260자로 제한됩니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 ASSEMBLY *assembly_name*  
 공개 키를 로드하는 데이터베이스에 이미 로드된 서명된 어셈블리의 이름입니다.  
  
 PROVIDER *provider_name*  
 EKM(확장 가능 키 관리) 공급자의 이름을 지정합니다. 먼저 CREATE PROVIDER 문을 사용하여 공급자를 정의해야 합니다. 외부 키 관리에 대한 자세한 내용은 [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)를 참조하세요.  
  
 ALGORITHM = \<algorithm>  
 RSA_4096, RSA_3072, RSA_2048, RSA_1024 및 RSA_512 등 5개 알고리즘을 제공할 수 있습니다.  
  
 RSA_1024 및 RSA_512는 사용하지 않습니다. RSA_1024 또는 RSA_512(권장하지 않음)를 사용하려면 데이터베이스 호환성 수준을 120 이하로 설정해야 합니다.  
  
 PROVIDER_KEY_NAME = '*key_name_in_provider*'  
 외부 공급자의 키 이름을 지정합니다.  
  
 CREATION_DISPOSITION = CREATE_NEW  
 확장 가능 키 관리 장치에 새 키를 만듭니다. PROVIDER_KEY_NAME을 사용하여 디바이스에 키 이름을 지정해야 합니다. 키가 이미 장치에 있는 경우 문이 오류와 함께 실패합니다.  
  
 CREATION_DISPOSITION = OPEN_EXISTING  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 비대칭 키를 기존 확장 가능 키 관리 키에 매핑합니다. PROVIDER_KEY_NAME을 사용하여 디바이스에 키 이름을 지정해야 합니다. CREATION_DISPOSITION = OPEN_EXISTING을 지정하지 않은 경우 기본값은 CREATE_NEW입니다.  
  
 ENCRYPTION BY PASSWORD = '*password*'  
 프라이빗 키를 암호화하는 데 사용할 암호를 지정합니다. 이 절이 없는 경우 프라이빗 키는 데이터베이스 마스터 키로 암호화됩니다. *password*는 최대 128자입니다. *password*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다.  
  
## <a name="remarks"></a>Remarks  
 *asymmetric key*는 데이터베이스 수준에서 보안 가능한 엔터티입니다. 기본 형태의 이 엔터티에는 퍼블릭 키와 프라이빗 키가 모두 포함됩니다. FROM 절 없이 실행될 경우 CREATE ASYMMETRIC KEY는 새로운 키 쌍을 생성합니다. FROM 절로 실행될 경우 CREATE ASYMMETRIC KEY는 파일에서 키 쌍을 가져오거나 어셈블리 또는 DLL 파일에서 공개 키를 가져옵니다.  
  
 기본적으로 프라이빗 키는 데이터베이스 마스터 키로 보호됩니다. 데이터베이스 마스터 키를 만든 경우 프라이빗 키를 보호하기 위해 암호가 필요합니다.  
  
 프라이빗 키의 길이는 512, 1024 또는 2048비트일 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 CREATE ASYMMETRIC KEY 권한이 필요합니다. AUTHORIZATION 절이 지정된 경우 데이터베이스 보안 주체에 대한 IMPERSONATE 권한 또는 응용 프로그램 역할에 대한 ALTER 권한이 필요합니다. Windows 로그인, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 애플리케이션 역할만 비대칭 키를 소유할 수 있습니다. 그룹 및 역할은 비대칭 키를 소유할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-an-asymmetric-key"></a>1\. 비대칭 키 만들기  
 다음 예에서는 `PacificSales09` 알고리즘을 사용하여 `RSA_2048`라는 비대칭 키를 만들고 암호로 프라이빗 키를 보호합니다.  
  
```  
CREATE ASYMMETRIC KEY PacificSales09   
    WITH ALGORITHM = RSA_2048   
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';   
GO  
```  
  
### <a name="b-creating-an-asymmetric-key-from-a-file-giving-authorization-to-a-user"></a>2\. 파일로부터 비대칭 키를 만들어서 사용자에게 권한 부여  
 다음 예에서는 파일에 저장된 키 쌍으로부터 비대칭 키 `PacificSales19`를 만든 다음, 사용자 `Christina`에게 비대칭 키의 소유권을 할당합니다. 프라이빗 키는 데이터베이스 마스터 키로 보호되며 마스터 키는 비대칭 키를 만들기 전에 만들어져야 합니다.  
  
```  
CREATE ASYMMETRIC KEY PacificSales19  
    AUTHORIZATION Christina  
    FROM FILE = 'c:\PacSales\Managers\ChristinaCerts.tmp';  
GO  
```  
  
### <a name="c-creating-an-asymmetric-key-from-an-ekm-provider"></a>C. EKM 공급자에서 비대칭 키 만들기  
 다음 예제에서는 `EKM_Provider1`이라는 확장 가능 키 관리 공급자에 저장된 키 쌍에서 `EKM_askey1` 비대칭 키와, 해당 공급자에서 `key10_user1`이라는 키를 만듭니다.  
  
```  
CREATE ASYMMETRIC KEY EKM_askey1   
    FROM PROVIDER EKM_Provider1  
    WITH   
        ALGORITHM = RSA_2048,   
        CREATION_DISPOSITION = CREATE_NEW  
        , PROVIDER_KEY_NAME  = 'key10_user1' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
 [DROP ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
 [ASYMKEYPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/asymkeyproperty-transact-sql.md)  
 [ASYMKEY_ID&#40;Transact-SQL&#41](../../t-sql/functions/asymkey-id-transact-sql.md)  
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
 [Azure Key Vault를 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
