---
title: TDE - BYOK(Bring Your Own Key) - Azure SQL | Microsoft Docs
description: "SQL Database 및 데이터 웨어하우스용 Azure Key Vault를 사용하여 TDE(투명한 데이터 암호화)를 위한 BYOK(Bring Your Own Key) 지원에 대해 간략히 설명합니다. BYOK 기반 TDE 개요, 이점, 작동 방법, 고려 사항 및 권장 사항입니다."
keywords: 
services: sql-database
documentationcenter: 
author: aliceku
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: aliceku
ms.openlocfilehash: 5a0b56974d85f63e3382f26b1388e7d30dfbd6f8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehouse"></a>Azure SQL Database 및 데이터 웨어하우스에 대한 Bring Your Own Key 지원으로 투명한 데이터 암호화
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

[TDE(투명한 데이터 암호화)](transparent-data-encryption.md)에 대한 BYOK(Bring Your Own Key) 지원을 통해 TDE 암호화 키를 제어하고 이 키에 액세스할 수 있는 사용자 및 시기를 제한할 수 있습니다. [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)는 Azure의 클라우드 기반 외부 키 관리 시스템으로, TDE가 BYOK에 대한 지원을 통합한 최초의 키 관리 서비스입니다. BYOK를 통해 데이터베이스 암호화 키는 Key Vault에 저장된 비대칭 키로 보호됩니다. 비대칭 키는 서버 수준에서 설정되고 해당 서버 아래 모든 데이터베이스에 의해 상속됩니다. 

BYOK 지원을 통해 사용자는 키 회전, 키 자격 증명 모음 권한, 키 삭제, 모든 암호화 키에 감사/보고 사용 등의 키 관리 작업을 제어할 수 있습니다. Key Vault는 중앙 키 관리를 제공하고, 엄격하게 모니터링되는 HSM(하드웨어 보안 모듈)을 활용하며, 키 및 데이터 관리의 의무를 분리하여 규정 준수를 충족하도록 합니다. 

BYOK 기반 TDE는 다음과 같은 이점을 제공합니다.
- TDE 보호자를 자체 관리하는 기능으로 투명도 증가 및 제어 세분화   
- Key Vault에 키를 호스팅하여 다른 Azure 서비스에 사용된 다른 키 및 비밀과 함께 TDE 암호화 키의 중앙 관리
- 조직 내에서 의무 구분을 위해 키 및 데이터 관리 역할 구분
- Key Vault는 Microsoft가 암호화 키를 보거나 추출하지 못하도록 설계되었으므로 클라이언트가 안심할 수 있음 
- 키 회전 지원

> [!IMPORTANT]
> Key Vault를 사용하려는 서비스 관리 TDE를 사용하는 경우 TDE는 Key Vault의 키로 전환하는 과정 중에 계속 설정 상태입니다. 작동 중단이나 데이터베이스 파일 자체를 다시 암호화하는 일은 없습니다. 서비스 관리 키에서 Key Vault 키로 전환하려면 데이터베이스 암호화 키를 다시 암호화해야 하며 이 작업은 신속한 온라인 작업입니다.
>

## <a name="how-does-tde-with-byok-support-work"></a>BYOK 기반 TDE 지원은 어떻게 작동하나요?
 
![Key Vault에 대해 서버 인증](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

TDE가 Key Vault의 키를 사용하도록 구성된 경우 서버는 *키 래핑* 요청을 위해 각 TDE 설정 데이터베이스의 데이터베이스 암호화 키를 Key Vault로 보냅니다. Key Vault는 사용자 데이터베이스에 저장된 암호화된 데이터베이스 암호화 키를 반환합니다. 

**키가 Key Vault에 저장되면 키는 Key Vault에서 비밀로 유지**된다는 것을 알아야 합니다. Key Vault의 HSM(하드웨어 보안 모듈) 지원 키는 HSM 보안 경계를 절대로 벗어나지 않습니다. 서버는 Key Vault 내에 있는 TDE 보호기 키 자료로 키 작업 요청만 보낼 수 있습니다. Key Vault 관리자는 모든 지점에서 서버에 대한 Key Vault 권한을 해지할 권한을 보유하며 이 경우 서버에 대한 모든 연결이 끊깁니다. 

## <a name="considerations"></a>고려 사항

BYOK 기반 TDE를 사용하면 추가 키 관리 작업과 키 자격 증명 모음 자체 사용과 관련된 비용이 모두 발생합니다. 이러한 고려 사항은 다음 두 섹션에서 설명합니다.

### <a name="key-management-responsibilities"></a>키 관리 책임

응용 프로그램 리소스의 암호화 키 관리를 인계하는 것은 중요한 책임입니다. Key Vault를 통해 BYOK 기반 TDE를 사용하여 다음 키 관리 작업을 가정합니다.
- **키 회전:** TDE 보호기는 내부 정책 또는 준수 요구 사항에 따라 회전되어야 합니다. 키 회전은 TDE 보호기의 키 자격 증명 모음을 통해 수행할 수 있습니다.  
- **키 자격 증명 모음 사용 권한**: Key Vault 내의 사용 권한은 키 자격 증명 모음 및 서버 수준에서 프로비전됩니다. 키 자격 증명 모음에 대한 서버의 사용 권한은 키 자격 증명 모음의 액세스 정책을 사용하여 언제든지 해지할 수 있습니다.
- **키 삭제**: 보안 강화 또는 준수 요구 사항 충족을 위해 Key Vault 및 SQL Server에서 키를 삭제할 수 있습니다.
- **모든 암호화 키에 대해 감사/보고**: Key Vault는 다른 SIEM(보안 정보 및 이벤트 관리) 도구에 쉽게 삽입되는 로그를 제공합니다. OMS(Operations Management Suite) [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault)는 이미 통합되어 있는 한 가지 예제 서비스입니다.

### <a name="pricing-considerations"></a>가격 책정 고려 사항 

BYOK 기반 TDE 지원은 추가 비용 없이 Azure SQL Database 및 데이터 웨어하우스에 기본 제공되는 보안 기능입니다. 그러나 Key Vault 자체를 사용하는 관련 비용은 발생합니다. 서버가 수행하는 Key Vault 작업에는 일반 작업으로 비용이 청구되며 Key Vault의 [가격 책정](https://azure.microsoft.com/pricing/details/key-vault/)을 따릅니다. 서버는 다음 이벤트에 대해 Key Vault로 요청을 보냅니다.
- SQL 인스턴스 다시 시작
- 키 롤오버
- 키 자격 증명 모음에 대한 서버 권한이 변경되었는지 6시간마다 확인합니다.

## <a name="important-warnings"></a>중요한 경고

### <a name="loss-of-access-to-keys"></a>키에 대한 액세스 권한 손실

서버가 TDE 보호기에 액세스할 수 없으면(Key Vault 사용 권한 제거 또는 키 삭제로 인해) **서버에서 암호화된 데이터베이스에 대한 모든 연결이 차단되고 해당 데이터베이스는 오프라인으로 전환되며 24시간 이내 삭제됩니다**. 사용할 수 없는 키를 사용하여 암호화된 오래된 백업은 더 이상 액세스할 수 없습니다. 키가 손상될 가능성이 있는 경우(서비스 또는 사용자가 키에 무단 액세스하는 경우)에는 [잠재적으로 손상된 키 제거](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)의 지침에 따라 키를 삭제하는 것이 최선입니다. 최대 10분 동안 잠재적인 데이터 손실을 방지하기 위해 활성 TDE 보호기를 삭제하기 전에 데이터베이스를 삭제해야 합니다.  

### <a name="expired-keys"></a>만료된 키

TDE 보호기의 가용성은 데이터베이스 가용성에 직접적인 영향을 주기 때문에 날짜가 만료된 키는 SQL Server에 추가할 수 없습니다. 키가 서버용 TDE 보호기로 이미 사용되고 나중에 Azure Key Vault에서 만료일과 함께 키가 구성된 경우 **키가 만료되면 암호화된 데이터베이스는 TDE 보호기에 액세스할 수 없으며 24시간 이내 삭제됩니다.**

### <a name="deleted-server-identities"></a>삭제된 서버 ID 

Key Vault에 대한 서버 액세스는 서버의 고유한 AAD(Azure Active Directory) ID를 통해 관리됩니다. 따라서 서버의 ID가 AAD에서 삭제되면 서버는 해당 키 자격 증명 모음에 대한 액세스 권한을 잃게 됩니다. 따라서 **서버에서 암호화된 데이터베이스에 대한 모든 연결이 차단되고 해당 데이터베이스는 오프라인으로 전환되며 24시간 이내 삭제됩니다.**

## <a name="limitations"></a>제한 사항

TDE에 사용된 키 자격 증명 모음은 SQL Database 또는 데이터 웨어하우스 서버와 동일한 AAD 테넌트에 있어야 합니다. 교차 테넌트 키 자격 증명 모음 및 서버 상호 작용은 지원되지 않습니다. Key Vault의 키로 암호화되는 리소스는 Azure 구독 간에 이동할 수 없습니다. 구독 간에 리소스를 이동하면 BYOK 기반 TDE를 가능하게 하는 데 필요한 Key Vault 액세스 제어가 중단됩니다. 모든 리소스를 다른 구독으로 이동해야 하는 경우 TDE 모드를 BYOK에서 [서비스 관리 TDE](transparent-data-encryption-azure-sql.md)로 변경합니다. 

데이터베이스 또는 데이터 웨어하우스에 대한 고유 TDE 보호기는 지원되지 않습니다. TDE 보호기는 서버 수준에서 설정되며 서버의 모든 리소스에 의해 상속됩니다. 

## <a name="guidelines-for-managing-encrypted-databases"></a>암호화된 데이터베이스 관리를 위한 지침

### <a name="high-availability-and-disaster-recovery"></a>고가용성 및 재해 복구
  
Key Vault를 사용하여 서버에 대해 두 가지 방법으로 지역에서 복제를 구성할 수 있습니다. 

- **별도의 키 자격 증명 모음**: 각 서버는 별도의 키 자격 증명 모음에 액세스할 수 있습니다(이상적으로는 각각 고유한 Azure 지역에 있음). 각 서버에는 암호화되고 지리적 복제된 데이터베이스에 대한 TDE 보호기의 사본이 있으므로 권장되는 구성입니다. 서버의 Azure 지역 중 하나가 오프라인으로 전환되면 다른 서버는 지리적으로 복제된 데이터베이스에 계속 액세스할 수 있습니다.   

- **공유 키 자격 증명 모음**: 모든 서버가 동일한 키 자격 증명 모음을 공유합니다. 이 구성은 쉽게 설정할 수 있지만 키 자격 증명 모음이 있는 Azure 지역이 오프라인으로 전환되면, 모든 서버에서 암호화되고 지역에서 복제된 데이터베이스 또는 고유한 암호화된 데이터베이스를 읽을 수 없습니다. 
 
시작하려면 [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) cmdlet을 사용하여 각 서버의 Key Vault 키를 지리적 복제 링크의 다른 서버에 추가합니다.  
(Key Vault에서 KeyId의 예: *https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h*)

   ```powershell
   <# Include the version guid in the KeyId #>
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

>[!NOTE]
>키 자격 증명 모음 이름 및 키 이름의 조합 문자 길이는 94자를 초과할 수 없습니다.
>

[활성 지리적 복제 개요](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)의 단계에 따라 이러한 서버로 활성 지리적 복제를 구성하고 장애 조치(failover)를 트리거합니다.  

### <a name="backup-and-restore"></a>Backup 및 Restore 메서드

Key Vault의 키를 사용하여 TDE로 데이터베이스를 암호화하면 생성된 백업 역시 동일한 TDE 보호기로 암호화됩니다.

Key Vault의 TDE 보호기로 암호화된 백업을 복원하려면 해당 키 자료가 원본 키 이름의 원본 자격 증명 모음에 있는지 확인합니다. 데이터베이스에 대한 TDE 보호기가 변경되면 데이터베이스의 이전 백업은 최신 TDE 보호기를 사용하도록 업데이트되지 **않습니다.** 따라서 Key Vault에서 TDE 보호기의 모든 이전 버전을 유지하여 데이터베이스 백업을 복원할 수 있도록 하는 것이 좋습니다. 

백업을 복원하는 데 필요할 수 있는 키가 원본 키 자격 증명 모음에 더 이상 없는 경우 다음 오류 메시지가 반환됩니다. “대상 서버 <Servername>은(는) <Timestamp #1> ~ <Timestamp #2>에 생성된 모든 AKV Uris에 액세스할 수 없습니다. 모든 AKV Uris를 복원한 후 작업을 다시 시도해 보십시오.”

이 문제를 완화하기 위해서는 [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) cmdlet을 실행하여 서버에 추가된 Key Vault의 키 목록을 반환합니다. 모든 백업을 복원할 수 있는지 확인하려면 백업의 대상 서버가 이러한 모든 키에 액세스할 수 있는지 확인하세요.

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
SQL Database에 대한 백업 복구에 대해 자세히 알아보려면 [Azure SQL Database 복구](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups)를 참조하세요. SQL Data Warehouse 백업 복구에 대해 자세히 알아보려면 [Azure SQL Data Warehouse 복구](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview)를 참조하세요.

## <a name="best-practices"></a>최선의 구현 방법

### <a name="key-management"></a>키 관리 

빠른 키 복구를 보장하고 Azure 외부의 데이터에 액세스하려면 다음을 수행하는 것이 좋습니다.
- 로컬 HSM 장치에 암호화 키를 로컬로 만듭니다. (이 키는 Azure Key Vault에 저장할 수 있도록 비대칭, RSA 2048 키여야 합니다.)
- 암호화 키 파일(.pfx, .byok 또는 .backup)을 Azure Key Vault로 가져옵니다. 우발적인 키 삭제로부터 복구를 보호하기 위해 [일시 삭제](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)를 설정하여 키 자격 증명 모음을 사용하는 것이 좋습니다.
- Azure Key Vault에 키를 처음 사용하는 경우 먼저 Azure Key Vault 키 백업을 수행합니다. [백업-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) 명령에 대해 알아 봅니다.
- 키에 대한 어떤 변경이 발생할 때마다 (예: ACL 추가, 태그 추가, 키 특성 추가) 또 다른 Azure Key Vault 키 백업을 수행해야 합니다.
- 키 롤오버 중에는 키 자격 증명 모음에 **키의 이전 버전 유지**하여 이전 데이터베이스 백업을 복원할 수 있습니다. 

먼저 TDE 암호화 키를 로컬로 만들고 비대칭 키를 가져오면 관리자가 키 에스크로 시스템에 키를 위탁할 수 있으므로 비대칭 키를 가져오는 것은 프로덕션 시나리오에 매우 좋습니다. 개인 키는 자격 증명 모음을 벗어날 수 없으므로 비대칭 키를 Azure Key Vault에서 만든 경우에는 키를 위탁할 수 없습니다. 중요한 데이터를 보호하는 데 사용되는 키는 위탁해야 합니다. 비대칭 키가 손실되는 경우 데이터를 영구적으로 복구할 수 없습니다.

### <a name="pre-configuration-for-replicated-databases"></a>복제된 데이터베이스에 대한 사전 구성

암호화된 데이터베이스를 다른 서버로 복제할 예정인 경우 데이터베이스를 이동 또는 복제하기 **전에** 다른 서버에 사용된 Key Vault 키 자료의 사본에 액세스할 수 있는지 확인합니다.  

각 서버는 별도의 키 자격 증명 모음(이상적으로는 서버와 동일한 Azure 영역에 있는 각각의 키 볼트)에 저장되어 있는 다른 서버에서 사용되는 Key Vault 키 자료의 복사본에 액세스할 수 있도록 하는 것이 좋습니다. 각 서버에는 암호화되고 복제된 데이터베이스에 대한 TDE 보호기의 사본이 있습니다. 서버의 Azure 지역 중 하나가 오프라인으로 전환되면 다른 서버는 복제된 데이터베이스에 계속 액세스할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- TDE에 대한 Bring Your Own Key 지원 시작: [PowerShell을 사용하고 Key Vault에서 사용자 고유 키를 사용하여 TDE 설정](transparent-data-encryption-byok-azure-sql-configure.md)
- 보안 정책을 준수하는 서버의 TDE 보호기를 회전하는 방법 알아보기: [PowerShell을 사용하여 투명한 데이터 암호화 보호기 회전](transparent-data-encryption-byok-azure-sql-key-rotation.md)
- 보안 인시던트가 발생할 경우 잠재적으로 손상된 TDE 보호기를 제거하는 방법 알아보기: [잠재적으로 손상된 키 제거](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) 
