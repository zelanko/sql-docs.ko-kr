---
title: SQL Server 및 데이터베이스 암호화 키
description: SQL Server 데이터베이스 엔진이 데이터를 암호화하고 보호하는 데 사용하는 서비스 마스터 키와 데이터베이스 마스터 키를 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- keys [SQL Server], database encryption
ms.assetid: 15c0a5e8-9177-484c-ae75-8c552dc0dac0
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: bd4a4e98f464c56e5c46c669b7ca26e5db5c814e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883080"
---
# <a name="sql-server-and-database-encryption-keys-database-engine"></a>SQL Server 및 데이터베이스 암호화 키(데이터베이스 엔진)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 암호화 키를 사용하여 데이터, 자격 증명 및 서버 데이터베이스에 저장된 연결 정보의 보안을 유지할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에는 *대칭* 과 *비대칭*등, 두 종류의 키가 있습니다. 대칭 키는 동일한 암호를 사용하여 데이터를 암호화하고 해독합니다. 비대칭 키는 한 암호를 사용하여 데이터를 암호화하고(*퍼블릭* 키라고 함) 다른 암호를 사용하여 데이터를 해독합니다(*프라이빗* 키라고 함).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 암호화 키에는 중요한 데이터를 보호하는 데 사용되는 퍼블릭 키, 프라이빗 키 및 대칭 키의 조합이 포함됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 처음 시작할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 초기화하는 동안 대칭 키가 생성됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 이 키를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 저장된 중요한 데이터를 암호화합니다. 퍼블릭 키 및 프라이빗 키는 운영 체제에서 생성되며 대칭 키를 보호하는 데 사용됩니다. 데이터베이스의 중요한 데이터를 저장하는 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스당 하나의 퍼블릭 키 및 프라이빗 키 쌍이 생성됩니다.  
  
## <a name="applications-for-sql-server-and-database-keys"></a>SQL Server 애플리케이션 및 데이터베이스 키  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 두 가지 주요한 용도로 키를 사용합니다. 이러한 키에는 *인스턴스에서 해당 인스턴스를 위해 생성되는 SMK(* 서비스 마스터 키 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] )와 데이터베이스에 사용되는 DMK( *데이터베이스 마스터 키* )가 있습니다.

### <a name="service-master-key"></a>서비스 마스터 키
  
 서비스 마스터 키는 SQL Server 암호화 계층의 루트입니다. SMK는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 시작되고 연결된 서버 암호, 자격 증명 및 데이터베이스 마스터 키를 암호화하는 데 사용될 때 처음으로 자동 생성됩니다. SMK는 Windows DPAPI(데이터 보호 API)를 사용하는 로컬 머신 키로 암호화됩니다. DPAPI는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정의 Windows 자격 증명 및 컴퓨터의 자격 증명에서 파생된 키를 사용합니다. 서비스 마스터 키의 암호는 해당 키가 만들어진 서비스 계정이나 해당 컴퓨터의 자격 증명에 대한 액세스 권한이 있는 보안 주체에 의해서만 해독될 수 있습니다.

서비스 마스터 키는 이 키를 만든 Windows 서비스 계정이나 서비스 계정 이름 및 암호에 대한 액세스를 갖고 있는 보안 주체만 열 수 있습니다.

 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에서는 AES 암호화 알고리즘을 사용하여 SMK(서비스 마스터 키) 및 DMK(데이터베이스 마스터 키)를 보호합니다. AES는 이전 버전에서 사용하는 3DES보다 최신 암호화 알고리즘입니다. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 인스턴스를 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 로 업그레이드한 후 SMK와 DMK를 다시 생성해야 마스터 키가 AES로 업그레이드됩니다. SMK를 다시 생성하는 방법은 [ALTER SERVICE MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-service-master-key-transact-sql.md) 및 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요.

### <a name="database-master-key"></a>데이터베이스 마스터 키
  
 데이터베이스 마스터 키는 데이터베이스에 있는 비대칭 키와 인증서의 프라이빗 키를 보호하는 데 사용되는 대칭 키입니다. 이 키는 데이터를 암호화하는 데에도 사용되지만 길이에 제한이 있기 때문에 대칭 키를 사용하는 것보다 유용하지 않습니다. 데이터베이스 마스터 키의 자동 암호 해독을 설정하려면 SMK를 사용하여 이 키의 복사본을 암호화합니다. 이 복사본이 사용되는 데이터베이스와 **master** 시스템 데이터베이스 모두에 암호화된 복사본이 저장됩니다.  
  
 **master** 시스템 데이터베이스에 저장된 DMK 복사본은 DMK가 변경될 때마다 자동으로 업데이트됩니다. 그러나 **DROP ENCRYPTION BY SERVICE MASTER KEY** 문의 **ALTER MASTER KEY** 옵션을 사용하여 이 기본값을 변경할 수 있습니다. 서비스 마스터 키로 암호화되지 않은 DMK는 **OPEN MASTER KEY** 문과 암호를 사용하여 열어야 합니다.  
  
## <a name="managing-sql-server-and-database-keys"></a>SQL Server 및 데이터베이스 키 관리  
 암호화 키 관리에는 새 데이터베이스 키 생성과 서버와 데이터베이스 키의 백업 생성뿐만 아니라 키 복원, 삭제 또는 변경 시기와 방법에 대한 이해가 포함됩니다.  
  
 대칭 키를 관리하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 포함된 도구를 사용하여 다음을 수행할 수 있습니다.  
  
-   서버 및 데이터베이스 키의 복사본을 백업하여 서버 설치를 복구하거나 계획된 마이그레이션의 일부로 사용합니다.  
  
-   이전에 저장한 키를 데이터베이스에 복원합니다. 이렇게 하면 새 서버 인스턴스를 사용하여 원래 암호화하지 않았던 기존 데이터에 액세스할 수 있습니다.  
  
-   암호화된 데이터에 더 이상 액세스할 수 없는 경우 데이터베이스에서 암호화된 데이터를 삭제합니다.  
  
-   키가 노출되는 경우 키를 다시 만들고 데이터를 다시 암호화합니다. 최상의 보안을 위해 키를 주기적으로(예: 몇 달에 한 번씩) 다시 만들어 키 해독을 시도하는 공격으로부터 서버를 보호해야 합니다.  
  
-   여러 서버가 단일 데이터베이스와 해당 데이터베이스에 해독 가능한 암호화를 제공하는 키를 모두 공유하는 서버 스케일 아웃 배포에서 서버 인스턴스를 추가하거나 제거합니다.  
  
## <a name="important-security-information"></a>중요한 보안 정보  
 서비스 마스터 키로 보안이 설정된 개체에 액세스하려면 이 키를 생성하는 데 사용된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정이나 컴퓨터 계정이 필요합니다. 즉, 컴퓨터는 키가 생성된 시스템에 연결되어 있습니다. 키에 대한 액세스 권한의 상실 없이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정 *또는* 컴퓨터 계정을 변경할 수 있습니다. 그러나 이 두 계정을 모두 변경하면 서비스 마스터 키에 대한 액세스 권한이 상실됩니다. 이러한 두 요소 중 하나가 없어서 서비스 마스터 키에 대한 액세스 권한을 상실한 경우 원래 키를 사용하여 암호화된 개체와 데이터의 암호를 해독할 수 없습니다.  
  
 서비스 마스터 키로 보안이 설정된 연결은 서비스 마스터 키가 없으면 복원할 수 없습니다.  
  
 데이터베이스 마스터 키로 보안이 설정된 개체와 데이터에 대해 액세스하려면 해당 키를 보호하기 위해 사용된 암호만 있으면 됩니다.  
  
> [!CAUTION]  
>  앞에서 설명한 키에 대한 액세스 권한을 모두 상실한 경우 해당 키로 보안이 설정된 개체, 연결 및 데이터에 대한 액세스 권한을 잃게 됩니다. 여기에 표시된 링크에 설명된 대로 서비스 마스터 키를 복원할 수 있고 원래 암호화한 시스템으로 이동하여 액세스 권한을 복구할 수 있습니다. 액세스 권한을 복구할 수 있는 다른 방법은 없습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [서비스 마스터 키](../../../relational-databases/security/encryption/service-master-key.md)  
 서비스 마스터 키 및 이 키를 사용하는 최상의 방법에 대해 간략하게 설명합니다.  
  
 [확장 가능 키 관리 &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
 타사 키 관리 시스템을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 사용하는 방법에 대해 설명합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [서비스 마스터 키 백업](../../../relational-databases/security/encryption/back-up-the-service-master-key.md)  
  
 [서비스 마스터 키 복원](../../../relational-databases/security/encryption/restore-the-service-master-key.md)  
  
 [데이터베이스 마스터 키 만들기](../../../relational-databases/security/encryption/create-a-database-master-key.md)  
  
 [데이터베이스 마스터 키 백업](../../../relational-databases/security/encryption/back-up-a-database-master-key.md)  
  
 [데이터베이스 마스터 키 복원](../../../relational-databases/security/encryption/restore-a-database-master-key.md)  
  
 [두 서버에서 동일한 대칭 키 만들기](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
 [EKM을 사용하여 SQL Server에서 TDE를 사용하도록 설정](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
 [Azure Key Vault를 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 [데이터 열 암호화](../../../relational-databases/security/encryption/encrypt-a-column-of-data.md)  
  
## <a name="related-content"></a>관련 내용  
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
 [ALTER SERVICE MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-service-master-key-transact-sql.md)  
  
 [데이터베이스 마스터 키 복원](../../../relational-databases/security/encryption/restore-a-database-master-key.md)  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 암호화 키 백업 및 복원](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [암호화 키 삭제 및 다시 만들기&#40;SSRS 구성 관리자&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [확장 배포의 암호화 키 추가 및 제거&#40;SSRS 구성 관리자&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [투명한 데이터 암호화&#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
