---
title: EKM(확장 가능 키 관리) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Key Management
- Extensible Key Management
- EKM, described
ms.assetid: 9bfaf500-2d1e-4c02-b041-b8761a9e695b
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: df1fe03ce3d0bf0397222ab3ef0834fac1cf6e33
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545345"
---
# <a name="extensible-key-management-ekm"></a>EKM(확장 가능 키 관리)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 암호화 및 키 생성용 MSCAPI( *Microsoft Cryptographic API* ) 공급자를 사용하여 EKM( *Extensible Key Management* )과 함께 데이터 암호화 기능을 제공합니다. 데이터 및 키 암호화를 위한 암호화 키는 임시 키 컨테이너에서 생성되며 데이터베이스에 저장되기 전에 공급자로부터 내보내져야 합니다. 이 방법을 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 암호화 키 계층 및 키 백업을 포함한 키 관리를 처리할 수 있습니다.  
  
 규정 준수에 대한 요구와 데이터에 포함된 개인 정보 보호에 대한 관심이 증가함에 따라 조직에서는 "심층 방어" 솔루션을 제공하기 위해 암호화를 활용하고 있습니다. 일반적으로 이 방법은 데이터베이스 암호화 관리 도구만 사용하므로 유용한 방법이 아닙니다. 하드웨어 공급업체에서는 HSM( *하드웨어 보안 모듈* )을 사용하여 엔터프라이즈 키 관리를 해결하는 제품을 제공합니다. HSM 디바이스는 하드웨어나 소프트웨어 모듈에 암호화 키를 저장합니다. 이 방법은 암호화 키와 암호화 데이터가 별도로 보관되므로 더욱 안전한 솔루션입니다.  
  
 많은 공급업체에서 키 관리와 암호화 가속 둘 다를 위해 HSM을 제공합니다. HSM 디바이스는 응용 프로그램과 HSM 간의 매개자로 서버 프로세스가 포함된 하드웨어 인터페이스를 사용합니다. 또한 공급업체는 하드웨어나 소프트웨어일 수 있는 해당 모듈을 통해 MSCAPI 공급자를 구현합니다. 일반적으로 MSCAPI는 HSM에서 제공하는 기능의 하위 집합만 제공합니다. 또한 공급업체는 HSM, 키 구성 및 키 액세스를 위해 관리 소프트웨어를 제공할 수도 있습니다.  
  
 HSM 구현은 공급업체마다 다르며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 사용하려면 공용 인터페이스가 필요합니다. MSCAPI는 이 인터페이스를 제공하지만 HSM 기능의 하위 집합만 지원합니다. 이외에도 MSCAPI에는 기본적으로 대칭 키를 지속할 수 없고 세션 지향이 지원되지 않는 등의 제한 사항이 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 확장 가능 키 관리를 사용하면 타사 EKM/HSM 공급업체가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 해당 모듈을 등록할 수 있습니다. EKM 모듈이 등록되면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 이러한 모듈에 저장된 암호화 키를 사용할 수 있고, 이를 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 이러한 모듈이 지원하는 대량 암호화 및 암호 해독 같은 고급 암호화 기능과 키 에이징 및 키 회전 같은 키 관리 함수에 액세스할 수 있습니다.  
  
 Azure VM에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 실행할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 [Azure 키 자격 증명 모음](https://go.microsoft.com/fwlink/?LinkId=521401)에 저장된 키를 사용할 수 있습니다. 자세한 내용은 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)에서 암호화 키 계층 및 키 백업을 포함한 키 관리를 처리할 수 있습니다.  
  
## <a name="ekm-configuration"></a>EKM 구성  
 일부 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]버전에서는 확장 가능 키 관리를 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 기본적으로 확장 가능 키 관리는 해제되어 있습니다. 이 기능을 사용하도록 설정하려면 다음 예와 같이 다음 옵션과 값이 포함된 sp_configure 명령을 사용합니다.  
  
```  
sp_configure 'show advanced', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'EKM provider enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
> [!NOTE]  
>  EKM을 지원하지 않는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전에서 이 옵션에 대해 명령을 사용할 경우 오류가 수신됩니다.  
  
 기능을 사용하지 않으려면 값을 **0**으로 설정합니다. 서버 옵션을 설정하는 방법은 [sp_configure&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 참조하세요.  
  
## <a name="how-to-use-ekm"></a>EKM 사용 방법  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 확장 가능 키 관리를 사용하면 데이터베이스 파일을 보호하는 암호화 키를 스마트 카드, USB 장치 또는 EKM/HSM 모듈과 같은 외부 장치에 저장할 수 있을 뿐 아니라 데이터베이스 관리자(sysadmin 그룹의 멤버 제외)로부터 데이터를 보호할 수도 있습니다. 즉, 외부 EKM/HSM 모듈에서 데이터베이스 사용자만 액세스할 수 있는 암호화 키를 사용하여 데이터를 암호화할 수 있습니다.  
  
 또한 확장 가능 키 관리는 다음과 같은 이점을 제공합니다.  
  
-   추가 권한 확인(의무 분리 가능)  
  
-   하드웨어 기반 암호화/암호 해독의 성능 향상  
  
-   외부 암호화 키 생성  
  
-   외부 암호화 키 저장(데이터와 키의 물리적 분리)  
  
-   암호화 키 검색  
  
-   외부 암호화 키 보존(암호화 키 회전 사용)  
  
-   더 쉬워진 암호화 키 복구  
  
-   관리 가능한 암호화 키 배포  
  
-   안전한 암호화 키 삭제  
  
 사용자 이름과 암호 조합 또는 EKM 드라이버에서 정의한 다른 메서드에 확장 가능 키 관리를 사용할 수 있습니다.  
  
> [!CAUTION]  
>  문제 해결을 위해 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 기술 지원 서비스에 EKM 공급자의 암호화 키를 제공하거나 공급업체 도구나 프로세스에 액세스해야 할 수 있습니다.  
  
### <a name="authentication-with-an-ekm-device"></a>EKM 디바이스를 사용한 인증  
 EKM 모듈은 둘 이상의 인증 유형을 지원할 수 있습니다. 각 공급자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 한 가지 유형의 인증만 제공합니다. 즉, 모듈에서 기본 또는 기타 인증 유형을 지원하는 경우 둘 다가 아닌 둘 중 하나만 제공합니다.  
  
#### <a name="ekm-device-specific-basic-authentication-using-usernamepassword"></a>사용자 이름/암호를 통한 EKM 디바이스별 기본 인증  
 *사용자 이름/암호* 쌍을 사용한 기본 인증을 지원하는 EKM 모듈의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 자격 증명을 사용하여 투명한 인증을 제공합니다. 자격 증명에 대한 자세한 내용은 [자격 증명&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/authentication-access/credentials-database-engine.md)을 참조하세요.  
  
 로그온할 때마다 EKM 공급자에 대해 자격 증명을 만든 후 로그인(Windows 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 계정 모두)에 매핑하여 EKM 모듈에 액세스할 수 있습니다. 자격 증명의 *Identify* 필드에는 사용자 이름이 포함되고 *secret* 필드에는 EKM 모듈에 연결할 암호가 포함됩니다.  
  
 EKM 공급자에 대해 매핑된 로그인 자격 증명이 없으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정에 매핑된 자격 증명이 사용됩니다.  
  
 자격 증명이 고유한 EKM 공급자에 대해 사용되는 경우 로그인에 여러 개의 매핑된 자격 증명이 있을 수 있습니다. 로그인별로 각 EKM 공급자에 하나의 매핑된 자격 증명만 있어야 합니다. 동일한 자격 증명이 다른 로그인에 매핑될 수 있습니다.  
  
#### <a name="other-types-of-ekm-device-specific-authentication"></a>다른 유형의 EKM 디바이스별 인증  
 Windows 또는 *사용자/암호* 조합 이외의 인증을 사용하는 EKM 모듈의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와는 별도로 인증이 수행되어야 합니다.  
  
### <a name="encryption-and-decryption-by-an-ekm-device"></a>EKM 디바이스별 암호화 및 암호 해독  
 다음 함수와 기능을 사용하여 대칭 및 비대칭 키를 통해 데이터를 암호화하고 암호 해독할 수 있습니다.  
  
|함수 또는 기능|참조|  
|-------------------------|---------------|  
|대칭 키 암호화|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|비대칭 키 암호화|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|EncryptByKey(key_guid, 'cleartext', ...)|[ENCRYPTBYKEY&#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)|  
|DecryptByKey(ciphertext, ...)|[DECRYPTBYKEY&#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)|  
|EncryptByAsmKey(key_guid, 'cleartext')|[ENCRYPTBYASYMKEY&#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)|  
|DecryptByAsmKey(ciphertext)|[DECRYPTBYASYMKEY&#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
  
#### <a name="database-keys-encryption-by-ekm-keys"></a>EKM 키로 데이터베이스 키 암호화  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 EKM 키를 사용하여 데이터베이스에 있는 다른 키를 암호화할 수 있습니다. EKM 디바이스에서 대칭 키 및 비대칭 키 모두를 만들고 사용할 수 있습니다. EKM 비대칭 키를 사용하여 네이티브(비 EKM) 대칭 키를 암호화할 수 있습니다.  
  
 다음 예에서는 데이터베이스 대칭 키를 만들고 EKM 모듈에 저장된 키를 사용하여 이 키를 암호화합니다.  
  
```  
CREATE SYMMETRIC KEY Key1  
WITH ALGORITHM = AES_256  
ENCRYPTION BY EKM_AKey1;  
GO  
--Open database key  
OPEN SYMMETRIC KEY Key1  
DECRYPTION BY EKM_AKey1  
```  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 데이터베이스 및 서버 키에 대한 자세한 내용은 [SQL Server 및 데이터베이스 암호화 키&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)를 참조하세요.  
  
> [!NOTE]  
>  한 EKM 키로 다른 EKM 키를 암호화할 수는 없습니다.  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 EKM 공급자에서 생성된 비대칭 키를 사용한 서명 모듈을 지원하지 않습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [EKM provider enabled 서버 구성 옵션](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
  
 [EKM을 사용하여 SQL Server에서 TDE를 사용하도록 설정](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [sys.cryptographic_providers&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)   
 [sys.dm_cryptographic_provider_sessions&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-sessions-transact-sql.md)   
 [sys.dm_cryptographic_provider_properties&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-properties-transact-sql.md)   
 [sys.dm_cryptographic_provider_algorithms&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-algorithms-transact-sql.md)   
 [sys.dm_cryptographic_provider_keys&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-keys-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [Reporting Services 암호화 키 백업 및 복원](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [암호화 키 삭제 및 다시 만들기&#40;SSRS 구성 관리자&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [확장 배포의 암호화 키 추가 및 제거&#40;SSRS 구성 관리자&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [서비스 마스터 키 백업](../../../relational-databases/security/encryption/back-up-the-service-master-key.md)   
 [서비스 마스터 키 복원](../../../relational-databases/security/encryption/restore-the-service-master-key.md)   
 [데이터베이스 마스터 키 만들기](../../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [데이터베이스 마스터 키 백업](../../../relational-databases/security/encryption/back-up-a-database-master-key.md)   
 [데이터베이스 마스터 키 복원](../../../relational-databases/security/encryption/restore-a-database-master-key.md)   
 [두 서버에서 동일한 대칭 키 만들기](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
