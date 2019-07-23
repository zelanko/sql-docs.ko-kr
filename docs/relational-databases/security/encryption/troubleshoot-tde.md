---
title: Azure Key Vault의 고객 관리 키를 통한 투명한 데이터 암호화의 일반적인 오류 | Microsoft Docs
description: Azure Key Vault 구성으로 TDE(투명한 데이터 암호화) 문제를 해결합니다.
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: aliceku
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 04/26/2019
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f67d1ed9bf809baaa4d934947e86d3fd1b7ed0b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111531"
---
# <a name="common-errors-for-transparent-data-encryption-with-customer-managed-keys-in-azure-key-vault"></a>Azure Key Vault의 고객 관리 키를 통한 투명한 데이터 암호화의 일반적인 오류

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
이 문서에서는 Azure Key Vault의 고객 관리 키를 통한 TDE(투명한 데이터 암호화)를 사용하기 위한 요구 사항과 일반적인 오류를 식별하고 해결하는 방법을 설명합니다.

## <a name="requirements"></a>요구 사항

Key Vault의 고객 관리 TDE 보호기로 TDE 문제를 해결하려면 다음 요구 사항을 충족해야 합니다.

- 논리 SQL Server 인스턴스와 Key Vault가 동일한 지역에 있어야 합니다.
- Azure Active Directory (Azure AD)에서 제공되는 논리 SQL Sever 인스턴스 ID, 즉 Azure Key Vault의 APPID는 원래 구독의 테넌트여야 합니다. 서버가 원래 구독에서 다른 구독으로 이동된 경우 서버 ID(APPID)를 다시 만들어야 합니다.
- Key Vault를 사용할 수 있어야 합니다. Key Vault 상태를 확인하는 방법은 [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview)를 참조하세요. 알림에 등록하려면 [작업 그룹](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups)을 확인하세요.
- 지리적 재해 복구 시나리오에서는 두 Key Vault에 동일한 키 자료가 포함되어 있어야만 장애 조치(failover)가 작동합니다.
- 논리 서버는 Azure AD ID(APPID)가 있어야 Key Vault에 인증됩니다.
- APPID는 Key Vault에 액세스할 수 있어야 하며 TDE 보호기로 선택된 키에 대한 가져오기, 래핑 및 래핑 해제 권한을 가져야 합니다.

자세한 내용은 [Guidelines for configuring TDE with Azure Key Vault](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault)합니다.

## <a name="common-misconfigurations"></a>일반적인 구성 오류

Key Vault로 TDE를 사용할 때 발생하는 문제는 대부분 다음 구성 오류 중 하나 때문에 발생합니다.

### <a name="the-key-vault-is-unavailable-or-doesnt-exist"></a>Key Vault를 사용할 수 없거나 존재하지 않습니다.

- Key Vault를 실수로 삭제되었습니다.
- Azure Key Vault에 대해 방화벽이 구성되었지만 이 방화벽에서 Microsoft 서비스에 대한 액세스를 허용하지 않습니다.

### <a name="no-permissions-to-access-the-key-vault-or-the-key-doesnt-exist"></a>Key Vault 또는 키에 액세스할 수 있는 권한이 없습니다.

- 키를 실수로 삭제했습니다.
- 논리 SQL Server 인스턴스 APPID를 실수로 삭제했습니다.
- 논리 SQL Server 인스턴스를 다른 구독으로 이동했습니다. 논리 서버를 다른 구독으로 이동했으면 새 APPID를 만들어야 합니다.
- 키의 APPID에 부여된 권한이 부족합니다(가져오기, 래핑 및 래핑 해제를 포함하지 않음).
- 논리 SQL Server 인스턴스 APPID에 대한 권한이 철회되었습니다.

## <a name="identify-and-resolve-common-errors"></a>일반적인 오류 식별 및 해결

이 섹션에서는 가장 일반적인 오류의 문제 해결 단계를 설명합니다.

### <a name="missing-server-identity"></a>누락된 서버 ID

**오류 메시지입니다.**

_401 AzureKeyVaultNoServerIdentity - 서버 ID가 서버에 올바르게 구성되어 있지 않습니다. 지원 담당자에게 문의하세요._

**검색**

다음 cmdlet 또는 명령을 사용하여 ID가 논리 SQL Server 인스턴스에 할당되었는지 확인합니다.

- Azure PowerShell: [Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 

- Azure CLI: [az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

**마이그레이션**

다음 cmdlet 또는 명령을 사용하여 논리 SQL Server 인스턴스의 Azure AD ID(APPID)를 구성합니다.

- Azure PowerShell: [Set-AzureRmSqlServer](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0)(`-AssignIdentity` 옵션 사용)

- Azure CLI: [az sql server 업데이트](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update)(`--assign_identity` 옵션 사용)

Azure Portal에서 Key Vault로 이동한 다음 **액세스 정책**으로 이동합니다. 다음 단계를 완료합니다. 

 1. **새로 추가** 단추를 사용하여 이전 단계에서 만든 서버의 APPID를 추가합니다. 
 1. 다음 키 사용 권한을 할당합니다. Get, 래핑 및 래핑 해제 

자세한 내용은 [Assign an Azure AD identity to your server](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server)(서버에 Azure AD ID 할당)를 참조하세요.

> [!IMPORTANT]
> Key Vault로 TDE의 초기 구성 후에 논리 SQL Server 인스턴스를 새 구독으로 이동한 경우 Azure AD ID를 구성하는 단계를 반복하여 새 APPID를 만듭니다. 그런 다음 Key Vault에 APPID를 추가하고 키에 올바른 권한을 할당합니다. 
>

### <a name="missing-key-vault"></a>누락된 Key Vault

**오류 메시지입니다.**

_503 AzureKeyVaultConnectionFailed - Azure Key Vault에 연결하려는 시도가 실패했으므로 서버에서 작업을 완료할 수 없습니다._

**검색**

키 URI 및 Key Vault를 식별하려면:

1. 다음 cmdlet 또는 명령을 사용하여 특정 논리 SQL Server 인스턴스의 키 URI를 가져옵니다.

    - Azure PowerShell: [Get-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

    - Azure CLI: [az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

1. 키 URI를 사용하여 Key Vault 식별:

    - Azure PowerShell: $MyServerKeyVaultKey 변수의 속성을 검사하여 Key Vault에 대한 세부 정보를 가져올 수 있습니다.

    - Azure CLI: Key Vault에 대한 자세한 내용은 반환된 서버 암호화 보호기를 검사합니다.

**마이그레이션**

Key Vault 사용 가능 여부 확인:

- Key Vault를 사용할 수 있고 논리 SQL Server 인스턴스에서 액세스할 수 있는지 확인합니다.
- Key Vault가 방화벽 뒤에 있는 경우 Microsoft 서비스에서 Key Vault에 액세스할 수 있도록 확인란이 선택되어 있는지 확인합니다.
- Key Vault를 실수로 삭제한 경우 구성을 처음부터 완료해야 합니다.


### <a name="missing-key"></a>누락된 키

**오류 메시지**

_404 ServerKeyNotFound - 요청된 서버 키를 현재 구독에서 찾을 수 없습니다._ 

_409 ServerKeyDoesNotExists - 서버 키가 없습니다._

**검색**

키 URI 및 Key Vault를 식별하려면:

- [누락된 Key Vault](#missing-key-vault)의 cmdlet 또는 명령을 사용하여 논리 SQL Server 인스턴스에 추가된 키 URI를 식별합니다. 명령을 실행하면 키 목록이 반환됩니다.

**마이그레이션**

TDE 보호기가 Key Vault에 있는지 확인합니다.

1. Key Vault를 식별하고 Azure Portal의 Key Vault로 이동합니다.
1. 키 URI로 식별되는 키가 있는지 확인합니다.

### <a name="missing-permissions"></a>누락된 권한

**오류 메시지입니다.**

_401 AzureKeyVaultMissingPermissions - 서버에서 Azure Key Vault에 필요한 사용 권한이 누락되었습니다._

**검색**

키 URI 및 Key Vault를 식별하려면: 

- [누락된 Key Vault](#missing-key-vault)의 cmdlet 또는 명령을 사용하여 논리 SQL Server 인스턴스에서 사용하는 Key Vault를 식별합니다.

**마이그레이션**

논리 SQL Server 인스턴스에 Key Vault에 대한 사용 권한 및 키에 액세스할 수 있는 권한이 있는지 확인:

- Azure Portal에서 Key Vault >**액세스 정책**으로 이동합니다. 논리 SQL Server 인스턴스 APPID를 찾습니다.  
- APPID가 있는 경우 APPID에 다음 키 사용 권한이 있는지 확인합니다. Get, 래핑 및 래핑 해제.
- APPID가 없는 경우 **새로 추가** 단추를 사용하여 추가합니다. 

## <a name="next-steps"></a>다음 단계

- [guidelines for configuring TDE with Azure Key Vault](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault)(Azure Key Vault로 TDE 구성 지침)를 참조하세요.
- [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview)를 확인하세요.
- [서버에 Azure AD ID를 할당](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server)하는 방법에 관한 최신 정보를 확인하세요.
