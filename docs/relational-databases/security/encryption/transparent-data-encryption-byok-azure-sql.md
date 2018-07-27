---
title: TDE - BYOK(Bring Your Own Key) - Azure SQL | Microsoft Docs
description: SQL Database 및 데이터 웨어하우스용 Azure Key Vault를 사용하여 TDE(투명한 데이터 암호화)를 위한 BYOK(Bring Your Own Key) 지원에 대해 간략히 설명합니다. BYOK 기반 TDE 개요, 이점, 작동 방법, 고려 사항 및 권장 사항입니다.
keywords: ''
services: sql-database
documentationcenter: ''
author: aliceku
manager: craigg
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.date: 06/28/2018
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: a803f26e65a4bdda5264fc2cea53a5b360f0df89
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982395"
---
# <a name="transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehouse"></a>Azure SQL Database 및 데이터 웨어하우스에 대한 Bring Your Own Key 지원으로 투명한 데이터 암호화
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

[TDE(투명한 데이터 암호화)](transparent-data-encryption.md)에 대한 BYOK(Bring Your Own Key) 지원을 사용하면 TDE 보호기라는 비대칭 키로 DEK(데이터베이스 암호화 키)를 암호화할 수 있습니다.  TDE 보호기는 사용자의 제어 하에 Azure의 클라우드 기반 외부 키 관리 시스템인 [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)에 저장됩니다. Azure Key Vault는 TDE가 BYOK에 대한 지원을 통합한 최초의 키 관리 서비스입니다. 데이터베이스의 부팅 페이지에 저장된 TDE DEK는 TDE 보호기로 암호화되고 해독됩니다. TDE 보호기는 Azure Key Vault에 저장되며 키 자격 증명 모음을 절대 벗어나지 않습니다. 키 자격 증명 모음에 대한 서버의 액세스 권한이 철회되면 데이터베이스를 해독하여 메모리에 읽어 들일 수 없습니다.  TDE 보호기는 논리 서버 수준에 설정되며 이 서버와 연결된 모든 데이터베이스에 상속됩니다. 

BYOK 지원을 통해 Azure Key Vault 기능을 사용하여 키 순환, 키 자격 증명 모음 권한, 키 삭제, 모든 TDE 보호기에 대한 감사/보고 기능 활성화를 비롯한 키 관리 작업을 제어할 수 있습니다. Key Vault는 중앙 키 관리를 제공하고, 엄격하게 모니터링되는 HSM(하드웨어 보안 모듈)을 활용하며, 키 및 데이터 관리의 의무를 분리하여 규정 준수를 충족하도록 합니다.  


BYOK 기반 TDE는 다음과 같은 이점을 제공합니다.
- TDE 보호자를 자체 관리하는 기능으로 투명도 증가 및 제어 세분화   
- TDE 보호기(다른 Azure 서비스에서 사용되는 다른 키 및 비밀과 함께)를 Key Vault에 호스팅하여 중앙 관리
- 조직 내에서 직무 분리를 위해 키 관리와 데이터 관리 책임을 분리
- Key Vault는 Microsoft가 암호화 키를 보거나 추출하지 못하도록 설계되었으므로 클라이언트가 안심할 수 있음 
- 키 회전 지원

> [!IMPORTANT]
> Key Vault를 사용하려는 서비스 관리 TDE를 사용하는 경우 TDE는 Key Vault의 TDE 보호기로 전환하는 동안 계속 사용됩니다. 작동 중단이나 데이터베이스 파일을 다시 암호화하는 일은 없습니다. 서비스 관리 키에서 Key Vault 키로 전환하는 경우에만 DEK(데이터베이스 암호화 키)를 다시 암호화해야 하며 이 작업은 신속한 온라인 작업입니다. 
>

## <a name="how-does-tde-with-byok-support-work"></a>BYOK 기반 TDE 지원은 어떻게 작동하나요?
 
![Key Vault에 대해 서버 인증](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

TDE가 Key Vault의 TDE 보호기를 사용하도록 처음 구성되면, 서버는 키 래핑 요청을 위해 TDE 가능 데이터베이스의 DEK를 Key Vault로 보냅니다. Key Vault는 사용자 데이터베이스에 저장된 암호화된 데이터베이스 암호화 키를 반환합니다.  

>[!IMPORTANT]
>**TDE 보호기가 Azure Key Vault에 저장되면 Azure Key Vault를 절대 벗어나지 않는다**는 점에 유의해야 합니다. 논리 서버는 Key Vault 내의 TDE 보호기 키 자료에만 키 작업 요청을 전송할 수 있으며 **TDE 보호기에 절대 액세스하거나 캐시하지 않습니다**. Key Vault 관리자는 서버에 대한 Key Vault 권한을 언제든 철회할 권한이 있으며 이렇게 되면 서버에 대한 모든 연결이 끊깁니다. 
>


## <a name="guidelines-for-configuring-tde-with-byok"></a>BYOK 기반 TDE 구성 지침

### <a name="general-guidelines"></a>일반적인 지침
- Azure Key Vault와 Azure SQL Database가 동일한 테넌트에 포함되어야 합니다.  테넌트 간 키 자격 증명 모음 및 서버 상호 작용은 **지원되지 않습니다**.
- 필요한 리소스에 사용할 구독을 결정합니다. 나중에 서버를 다른 구독으로 이동하려면 BYOK 기반 TDE를 새로 설정해야 합니다. [리소스 이동](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-move-resources)에 대한 자세한 정보
- BYOK 기반 TDE를 구성할 때에는 래핑/래핑 해제 작업 때문에 키 자격 증명 모음에 적용되는 부하를 고려하는 것이 중요합니다. 예를 들어 논리 서버와 연결된 모든 데이터베이스는 동일한 TDE 보호기를 사용하며, 따라서 해당 서버를 장애 조치(failover)하면 서버에 있는 데이터베이스 수만큼 자격 증명 모음에 대한 키 작업이 트리거됩니다. 우리가 경험한 내용과 [키 자격 증명 모음 서비스 제한](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-service-limits)에 설명된 내용에 따라, 자격 증명 모음의 TDE 보호기에 액세스할 때 일관적으로 고가용성을 보장할 수 있도록 단일 구독의 Azure Key Vault 하나에 표준/범용 데이터베이스는 최대 500개 또는 프리미엄/중요 비즈니스용 데이터베이스는 최대 200개까지만 연결하는 것이 좋습니다. 
- 권장 사항: 온-프레미스에 TDE 보호기 사본을 유지합니다.  이렇게 하려면 로컬로 TDE 보호기를 생성할 HSM 장치와 TDE 보호기의 로컬 복사본을 저장할 키 에스크로 시스템이 필요합니다.


### <a name="guidelines-for-configuring-azure-key-vault"></a>Azure Key Vault 구성 지침

- 키 또는 키 자격 증명 모음이 우발적으로 삭제되는 경우 데이터 손실을 방지하기 위해 [일시 삭제](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)가 설정된 키 자격 증명 모음을 만듭니다.  키 자격 증명 모음에서 ["일시 삭제" 속성을 활성화하는 PowerShell](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell)을 사용해야 합니다(이 옵션은 아직 AKV 포털에서 사용할 수 없으나 SQL에서 필요함).  
  - 일시 삭제된 리소스는 복구되거나 제거되지 않는 한 설정된 기간인 90일 동안 보존됩니다.
  - **복구** 및 **제거** 작업에는 키 자격 증명 모음 액세스 정책과 연결된 고유 권한이 있습니다. 
- 키 자격 증명 모음에 대한 리소스 잠금을 설정하여 이 중요 리소스를 삭제할 수 있는 사용자를 제어하고 우발적이거나 권한 없는 삭제를 방지할 수 있습니다.  [리소스 잠금에 대한 자세한 정보](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-lock-resources)

- Azure AD(Azure Active Directory) ID를 사용하여 키 자격 증명 모음에 대한 논리 서버 액세스 권한을 부여합니다.  포털 UI를 사용하는 경우 Azure AD ID가 자동으로 생성되며 키 자격 증명 모음 액세스 권한이 서버에 부여됩니다.  PowerShell을 사용하여 BYOK 기반 TDE를 구성하면 Azure AD ID가 생성되어야 하며 완료를 확인해야 합니다. PowerShell을 사용하는 경우 자세한 단계별 지침은 [BYOK 기반 TDE 구성](transparent-data-encryption-byok-azure-sql-configure.md)을 참조하세요.

  >[!NOTE]
  >Azure AD ID가 **실수로 삭제되거나 키 자격 증명 모음의 액세스 정책을 사용하여 서버의 권한이 철회되면** 키 자격 증명 모음에 대한 서버의 액세스 권한이 손실되고 TDE로 암호화된 데이터베이스가 24시간 내에 삭제됩니다.
  >

- VNET 또는 방화벽 없이 Azure Key Vault를 구성합니다.  키 자격 증명 모음에 대한 SQL의 액세스 권한이 손실되면 TDE로 암호화된 데이터베이스는 24시간 내에 삭제됩니다.
- 모든 암호화 키에 대한 감사 및 보고 사용: Key Vault는 다른 SIEM(보안 정보 및 이벤트 관리) 도구에 쉽게 삽입되는 로그를 제공합니다. OMS(Operations Management Suite) [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault)는 이미 통합되어 있는 한 가지 예제 서비스입니다.
- 암호화된 데이터베이스의 고가용성을 보장하려면 서로 다른 지역에 있는 두 개의 Azure Key Vault로 각 논리 서버를 구성합니다.


### <a name="guidelines-for-configuring-the-tde-protector-asymmetric-key-stored-in-azure-key-vault"></a>Azure Key Vault에 저장된 TDE 보호기(비대칭 키) 구성 지침

- 로컬 HSM 장치에 암호화 키를 로컬로 만듭니다. Azure Key Vault에 저장할 수 있는 비대칭 RSA 2048 키여야 합니다.
- 키 에스크로우 시스템에서 키를 위탁합니다.  
- 암호화 키 파일(.pfx, .byok 또는 .backup)을 Azure Key Vault로 가져옵니다. 
    

>[!NOTE] 
    >테스트를 위해 Azure Key Vault로 키를 생성할 수 있지만 이 키는 위탁될 수 없습니다. 개인 키는 키 자격 증명 모음을 벗어날 수 없기 때문입니다.  키를 분실하면(키 자격 증명 모음에서 실수로 삭제, 만료 등) 데이터가 영구적으로 손실되므로 프로덕션 데이터를 암호화하는 데 사용되는 키는 항상 백업하고 위탁합니다.
    >
    
- 키를 만료 날짜 없이 사용하고 이미 사용 중인 키에 만료 날짜를 설정하지 않습니다. **키가 만료되면 암호화된 데이터베이스는 TDE 보호기에 액세스 할 수 없게 되고 24시간 이내에 삭제됩니다**.
- 키가 활성화되어 있고 *가져오기*, *키 래핑* 및 *키 래핑 해제* 작업을 수행할 권한이 있어야 합니다.
- Azure Key Vault에서 처음 키를 사용하기 전에 Azure Key Vault 키 백업을 생성합니다. [백업-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) 명령에 대해 알아 봅니다.
- 키가 변경될 때마다(예: ACL 추가, 태그 추가, 키 속성 추가) 새 백업을 만듭니다.
- 키를 순환할 때는 키 자격 증명 모음에 **이전 버전의 키를 유지**하여 이전 데이터베이스 백업이 복원될 수 있도록 합니다. 데이터베이스에 대한 TDE 보호기가 변경되면 데이터베이스의 이전 백업은 최신 TDE 보호기를 사용하도록 업데이트되지 **않습니다**.  각 백업에는 복원 시 함께 생성된 TDE 보호기가 필요합니다. 키 순환은 [PowerShell을 사용하여 투명한 데이터 암호화 보호기 순환](transparent-data-encryption-byok-azure-sql-key-rotation.md)의 지침에 따라 수행할 수 있습니다.
- 서비스 관리 키로 다시 변경한 후에는 이전에 사용된 모든 키를 Azure Key Vault에 유지합니다.  이렇게 하면 Azure Key Vault에 저장된 TDE 보호기로 데이터베이스 백업을 복원할 수 있습니다.  Azure Key Vault로 생성된 TDE 보호기는 저장된 모든 백업이 서비스 관리 키로 생성될 때까지 유지되어야 합니다.  
- [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1)를 사용하여 이러한 키의 복구 가능한 백업 복사본을 만듭니다.
- 보안 인시던트 발생 시 데이터 손실 위험 없이 잠재적으로 손상된 키를 제거하려면 [잠재적으로 손상된 키 제거](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)의 단계를 수행합니다.


## <a name="high-availability-geo-replication-and-backup--restore"></a>고 가용성, 지리적 복제 및 백업/복원

### <a name="high-availability-and-disaster-recovery"></a>고가용성 및 재해 복구

Azure Key Vault로 고가용성을 구성하는 방법은 데이터베이스 및 논리 서버의 구성에 따라 다르며, 다음은 두 가지 다른 경우에 권장되는 구성입니다.  첫 번째 경우는 지리적 중복이 구성되지 않은 독립 실행형 데이터베이스 또는 논리 서버입니다.  두 번째 경우는 장애 조치(failover) 그룹 또는 지리적 중복으로 구성된 데이터베이스 또는 논리 서버입니다. 이런 경우 지리적 장애 조치(failover)가 작동하도록 각 지역 중복 복사본에 장애 조치(failover) 그룹 내의 로컬 Azure Key Vault가 있어야 합니다. 첫 번째 경우, 지리적 중복이 구성되지 않은 데이터베이스 및 논리 서버의 고가용성이 필요하면 동일한 키 자료를 사용하여 두 개의 다른 지역에 있는 두 개의 다른 키 자격 증명 모음을 사용하도록 서버를 구성하는 것이 좋습니다.  이렇게 하려면 데이터베이스가 가동 및 실행되는 동안 기본 키 자격 증명 모음에 정전이 발생할 경우 서버가 두 번째 키 자격 증명 모음에 액세스할 수 있도록, 논리 서버와 동일한 영역에 함께 배치된 기본 Key Vault를 사용하여 TDE 보호기를 생성하고 다른 Azure 지역의 키 자격 증명 모음에 키를 복제합니다. Backup-AzureKeyVaultKey cmdlet을 사용하여 기본 키 자격 증명 모음에서 암호화된 형식으로 키를 검색한 다음 Restore-AzureKeyVaultKey cmdlet을 사용하고 두 번째 지역에서 키 자격 증명 모음을 지정합니다.


![단일 서버 HA 및 Geo-DR 없음](./media/transparent-data-encryption-byok-azure-sql/SingleServer_HA_Config.PNG)

## <a name="how-to-configure-geo-dr-with-azure-key-vault"></a>Azure Key Vault로 Geo-DR을 구성하는 방법

암호화된 데이터베이스에서 TDE 보호기의 고가용성을 유지하려면 기존 또는 원하는 SQL Database 장애 조치(failover) 그룹이나 활성 지역 복제 인스턴스를 기반으로 중복 Azure Key Vault를 구성해야 합니다.  지리적으로 복제된 각 서버에는 별도의 키 자격 증명 모음이 필요하며 동일한 Azure 지역의 서버와 함께 배치해야 합니다. 한 지역의 정전으로 인해 기본 데이터베이스에 액세스할 수 없게 되어 장애 조치(failover)가 트리거되면, 보조 데이터베이스가 보조 키 자격 증명 모음을 사용하여 인수할 수 있습니다. 
 
지리적으로 복제된 Azure SQL Databases의 경우 다음 Azure Key Vault 구성이 필요합니다.
- 지역에서 키 자격 증명 모음을 사용하는 하나의 기본 데이터베이스, 지역에서 키 자격 증명 모음을 사용하는 하나의 보조 데이터베이스. 
- 보조 데이터베이스가 하나 이상 필요하며 최대 4개의 보조 데이터베이스가 지원됩니다. 
- 보조의 보조(체인)는 지원되지 않습니다.

다음 섹션에서는 설치 및 구성 단계를 자세히 살펴봅니다. 

### <a name="azure-key-vault-configuration-steps"></a>Azure Key Vault 구성 단계

- [PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-5.6.0) 설치 
- [“soft-delete” 속성을 활성화하는 PowerShell](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell)을 사용하여 다른 두 지역에 두 개의 Azure Key Vault를 만듭니다(이 옵션은 아직 AKV 포털에서 사용할 수 없으나 SQL에서 필요함).
- 키 백업과 복원이 작동하려면 두 Azure Key Vault 모두 동일한 Azure Geo에서 제공되는 두 지역에 있어야 합니다.  SQL Geo-DR 요구 사항에 부합하기 위해 두 자격 증명 모음이 서로 다른 지역에 있어야 하는 경우 키를 온-프레미스 HSM에서 가져올 수 있는 [BYOK 프로세스가](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-hsm-protected-keys)를 따릅니다.
- 첫 번째 키 자격 증명 모음에서 새 키를 만듭니다.  
  - RSA/RSA-HSA 2048 키 
  - 만료 날짜 없음 
  - 키가 활성화되어 있고 가져오기, 키 래핑 및 키 래핑 해제 작업을 수행할 권한이 있어야 합니다. 
- 기본 키를 백업하고 두 번째 키 자격 증명 모음으로 키를 복원합니다.  [BackupAzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) 및 [복원 - AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey?view=azurermps-5.5.0)를 참조하세요. 

### <a name="azure-sql-database-configuration-steps"></a>Azure SQL Database 구성 단계

다음 구성 단계는 새 SQL 배포로 시작하는지 여부 또는 이미 기존 SQL Geo-DR 배포를 사용하는지 여부에 따라 다릅니다.  먼저 새 배포에 대한 구성 단계를 간략하게 설명한 다음, Azure Key Vault에 저장된 TDE 보호기를 이미 Geo-DR 링크가 설정되어 있는 기존 배포에 할당하는 방법에 대해 설명합니다. 

새 배포를 위한 단계:
- 이전에 만든 키 자격 증명 모음과 동일한 두 지역에 두 개의 논리 SQL 서버를 만듭니다. 
- 논리 서버 TDE 창을 선택하고 각 논리 SQL Server에 대해 다음을 수행합니다.  
   - 동일한 지역에서 AKV를 선택합니다. 
   - TDE 보호기로 사용할 키를 선택합니다. 각 서버는 TDE 보호기의 로컬 복사본을 사용합니다. 
   - 포털에서 이 작업을 수행하면 논리 SQL Server에 대한 [AppID](https://docs.microsoft.com/en-us/azure/active-directory/managed-service-identity/overview)가 만들어집니다. 이는 키 자격 증명 모음에 액세스하도록 논리 SQL Server 권한을 할당하는 데 사용되므로 이 ID는 삭제하지 마세요. 논리 SQL Server 대신 Azure Key Vault에서 사용 권한을 제거하여 액세스를 철회할 수 있습니다. 이는 키 자격 증명 모음에 액세스하도록 논리 SQL Server 권한을 할당하는 데 사용됩니다.
- 기본 데이터베이스를 만듭니다. 
- [활성 지역 복제 지침](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview)에 따라 시나리오를 완료합니다. 이 단계에서는 보조 데이터베이스를 만듭니다.

![장애 조치(failover) 그룹 및 Geo-DR](./media/transparent-data-encryption-byok-azure-sql/Geo_DR_Config.PNG)

>[!NOTE]
>데이터베이스 간에 지리적 연결을 설정하기 전에 동일한 TDE 보호기가 두 키 자격 증명 모음에 모두 있는지 확인하는 것이 중요합니다.
>

Geo-DR 배포를 사용한 기존 SQL DB를 위한 단계:

논리 SQL Server가 이미 존재하고 주 데이터베이스와 보조 데이터베이스가 이미 할당되어 있기 때문에 Azure Key Vault를 구성하는 단계는 다음 순서대로 수행해야 합니다. 
- 보조 데이터베이스를 호스팅하는 논리 SQL Server를 시작합니다. 
   - 동일한 지역에 있는 키 자격 증명 모음에 할당 
   - TDE 보호기 할당 
- 이제 주 데이터베이스를 호스팅하는 논리 SQL Server로 이동합니다. 
   - 보조 DB에 사용한 것과 동일한 TDE 보호기 선택
   
![장애 조치(failover) 그룹 및 Geo-DR](./media/transparent-data-encryption-byok-azure-sql/geo_DR_ex_config.PNG)

>[!NOTE]
>키 자격 증명 모음을 서버를 할당할 때 보조 서버를 시작하는 것이 중요합니다.  두 번째 단계에서는 키 자격 증명 모음을 주 서버에 할당하고 TDE 보호기를 업데이트합니다. 이 시점에서 복제된 데이터베이스에서 사용하는 TDE 보호기는 두 서버에서 모두 사용할 수 있으므로 Geo-DR 링크는 계속 작동합니다.
>

SQL Database Geo-DR 시나리오에 대해 Azure Key Vault에서 고객 관리되는 키를 이용하여 TDE를 활성화하기 전에, SQL Database 지리적 복제에 사용될 것과 동일한 지역의 동일한 콘텐츠로 두 Azure Key Vaults를 만들고 유지 관리하는 것이 중요합니다.  “동일한 콘텐츠”는 특별히 두 서버가 모든 데이터베이스에서 사용하는 TDE 보호기에 대한 액세스 권한을 갖도록 두 키 자격 증명 모음이 동일한 TDE 보호기의 복제본을 포함해야 함을 의미합니다.  앞으로 두 키 자격 증명 모음을 동기적으로 유지해야 합니다. 즉, 키 회전 후에 동일한 TDE 보호기의 복제본을 포함해야 하며, 로그 파일 또는 백업에 사용된 이전 키 버전을 유지해야 하고, TDE 보호기는 동일한 키 속성을 유지 관리해야 하고, 키 자격 증명 모음은 SQL에 대한 동일한 액세스 권한을 유지 관리해야 합니다.  
 
[활성 지리적 복제 개요](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)의 단계에 따라 장애 조치(failover)를 테스트하고 트리거합니다. 이는 두 키 자격 증명 모음이 모두 유지 관리되도록 SQL에 대한 액세스 권한을 확인하기 위해 정기적으로 수행해야 합니다. 


### <a name="backup-and-restore"></a>Backup 및 Restore 메서드

Key Vault의 키를 사용하여 TDE로 데이터베이스를 암호화하면 생성된 백업 역시 동일한 TDE 보호기로 암호화됩니다.

Key Vault의 TDE 보호기로 암호화된 백업을 복원하려면 해당 키 자료가 원본 키 이름의 원본 자격 증명 모음에 있는지 확인합니다. 데이터베이스에 대한 TDE 보호기가 변경되면 데이터베이스의 이전 백업은 최신 TDE 보호기를 사용하도록 업데이트되지 **않습니다.** 따라서 Key Vault에서 TDE 보호기의 모든 이전 버전을 유지하여 데이터베이스 백업을 복원할 수 있도록 하는 것이 좋습니다. 

백업을 복원하는 데 필요할 수 있는 키가 원본 키 자격 증명 모음에 더 이상 없는 경우 다음 오류 메시지가 반환됩니다. “대상 서버 <Servername>은(는) <Timestamp #1> ~ <Timestamp #2>에 생성된 모든 AKV Uris에 액세스할 수 없습니다. 모든 AKV Uris를 복원한 후 작업을 다시 시도해 보십시오.”

마이그레이션하려면 [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) cmdlet을 실행하여 서버에 추가되어 있는 Key Vault의 키 목록을 반환합니다(다른 사용자가 삭제하지 않은 경우). 모든 백업이 복원될 수 있도록 하려면 백업의 대상 서버가 모든 키에 액세스할 수 있어야 합니다.

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
SQL Database에 대한 백업 복구에 대해 자세히 알아보려면 [Azure SQL Database 복구](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups)를 참조하세요. SQL Data Warehouse 백업 복구에 대해 자세히 알아보려면 [Azure SQL Data Warehouse 복구](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview)를 참조하세요.


백업된 로그 파일에 대한 추가 고려 사항: TDE 보호기가 회전되었고 데이터베이스에서 이제 새 TDE 보호기를 사용할지라도 백업된 로그 파일은 원래 TDE 암호기로 암호화된 상태를 유지됩니다.  복원 시 데이터베이스를 복원하려면 두 키가 모두 필요합니다.  로그 파일이 Azure Key Vault에 저장된 TDE 보호기를 사용하는 경우 서비스 관리 TDE를 사용하도록 데이터베이스가 변경된 경우에도 복원 시 이 키가 필요합니다.


