---
title: AKV(Azure Key Vault)에서 고객 관리 키를 사용하는 TDE(투명화 데이터 암호화)를 통한 일반적인 오류 및 해결 방법 | Microsoft Docs
description: Azure Key Vault 구성으로 TDE(투명한 데이터 암호화) 문제를 해결합니다.
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: aliceku
manager: craigg
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 04/26/2019
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 1366d0a20ed39b466d1a2f6cb3e84f0f30e17f9f
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718093"
---
# <a name="common-errors-and-resolutions-with-transparent-data-encryption-tde-with-customer-managed-keys-in-azure-key-vault-akv"></a>AKV(Azure Key Vault)에서 고객 관리 키를 사용하는 TDE(투명화 데이터 암호화)를 통한 일반적인 오류 및 해결 방법

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
이 항목에는 다음 문제에 대한 정보가 있습니다.  
  
- 요구 사항  
- 가장 일반적인 오류를 식별하고 해결하는 방법

## <a name="requirements"></a>요구 사항
[AKV 구성의 TDE(고객 관리형 TDE 포함)](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault) 문제를 해결하기 위해 다음 요구 사항을 확인하는 것으로 시작하겠습니다.
- 논리 SQL server와 Key Vault는 동일한 지역에 있어야 합니다.
- Azure Active Directory(Azure Key Vault의 APPID)에서 제공되는 논리 SQL 서버 ID는 원래 구독의 테넌트로 제한됩니다.  서버를 다른 구독으로 이동한 경우 서버 ID(APPID)를 다시 만들어야 합니다.
- Key Vault가 설치되고 실행되어야 하며, Key Vault 상태를 확인하려면 [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview)에 대해 알아보고 알림에 등록하려면 [Action Groups](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups)에 대해 알아봅니다.
- Geo-DR 시나리오에서 두 Key Vaults는 장애 조치(failover)가 작동하는 데 필요한 동일한 핵심 자료가 있어야 합니다.
- 논리 서버는 Key Vault에 인증하기 위해 AAD(Azure Active Directory) ID(APPID)가 있어야 합니다.
- APPID는 Key Vault에 액세스할 수 있어야 하며 TDE 보호기로 선택된 키에 대한 래핑, 래핑 해제 및 사용 권한을 가져야 합니다.

AKV와 함께 TDE를 사용할 때 발생하는 대부분의 문제는 다음과 같은 잘못된 구성 중 하나 때문입니다.

### <a name="key-vault-unavailable-or-doesnt-exist"></a>Key Vault를 사용할 수 없거나 존재하지 않나요?
- 실수로 삭제된 Key Vault
- Microsoft 서비스에 대한 액세스를 허용하지 않고 Azure Key Vault에 대해 구성된 방화벽

### <a name="no-permissions-to-access-the-key-vault-or-key-doesnt-exist"></a>Key Vault 또는 키에 액세스할 수 있는 권한이 없나요?
- 실수로 삭제된 키
- 실수로 삭제된 SQL APPID
- SQL이 다른 구독으로 이동되었으므로 새 APPID가 필요합니다.
- 충분한 키가 아닌 APPID에 부여된 사용 권한(래핑, 래핑 해제, 가져오기)
- SQL APPID에 대한 사용 권한 해지


다음 섹션에서는 가장 일반적인 오류에 대한 문제 해결 단계를 나열합니다.


## <a name="how-to-identify-and-resolve-the-most-common-errors"></a>가장 일반적인 오류를 식별하고 해결하는 방법

## <a name="missing-server-identity"></a>누락된 서버 ID
오류 메시지: "401 AzureKeyVaultNoServerIdentity - 서버 ID가 올바르게 구성되어 있지 않습니다. 지원 담당자에게 문의하세요."

검색: 다음 명령을 사용하여 ID가 논리 SQL 서버에 할당되었는지 확인합니다.

- [Azure PowerShell Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 
- [Azure CLI az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

마이그레이션: 논리 SQL 서버에 대한 Azure AD(Azure Active Directory) ID(APPID) 구성

PowerShell의 경우: [-AssignIdentity](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0) 옵션과 함께 Set-AzureRmSqlServer 명령 사용 

CLI의 경우: [--assign_identity](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update) 옵션과 함께 az sql server 업데이트 명령 사용 

Azure Portal에서 Key Vault로 이동하여 액세스 정책으로 이동합니다.  
 - 새 추가 단추를 사용하여 이전 단계에서 만든 서버에 대한 APPID를 추가합니다. 
 - 다음 키 사용 권한을 할당합니다. Get, 래핑 및 래핑 해제 

[자세히 알아보기](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server)

> [!IMPORTANT]
> AKV로 TDE의 초기 구성 후에 논리 SQL 서버를 새 구독으로 이동한 경우 새 APPID를 만들려면 AAD ID를 구성하는 단계를 반복해야 합니다.  그런 다음, 새 APPID를 Key Vault에 추가하고 올바른 사용 권한을 다시 할당해야 합니다. 
>

## <a name="missing-key-vault"></a>누락된 Key Vault
오류 메시지: "503 AzureKeyVaultConnectionFailed - Azure Key Vault에 연결하려는 시도가 실패했으므로 서버에서 작업을 완료할 수 없습니다."

검색: 키 uri 및 Key Vault를 식별하는 방법 

1단계: 다음 명령을 사용하여 지정된 논리 SQL 서버의 키 uri를 가져옵니다.

-[Azure PowerShell get-azurermsqlserverkeyvaultkey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

-[Azure CLI az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

2단계: 키 uri를 사용하여 Key Vault 식별

PowerShell: $MyServerKeyVaultKey의 속성을 검사하여 Key Vault에 대한 세부 정보를 가져올 수 있습니다.

CLI: Key Vault에 대한 자세한 내용은 반환된 서버 암호화 보호기를 검사합니다.

마이그레이션: Key Vault 사용 가능 여부 확인
- Key Vault를 사용할 수 있고 논리 SQL Server에 액세스할 수 있는지 확인
- Key Vault가 방화벽 뒤에 있는 경우 Microsoft Services에서 Key Vault에 액세스할 수 있도록 확인란이 선택되어 있는지 확인합니다.
- Key Vault를 실수로 삭제한 경우 구성을 처음부터 완료해야 합니다.


## <a name="missing-key"></a>누락된 키 
오류 메시지: "404 ServerKeyNotFound - 요청된 서버 키를 현재 구독에서 찾을 수 없습니다."
"409 ServerKeyDoesNotExists - 서버 키가 없습니다."

검색: 키 uri 및 Key Vault를 식별하는 방법
- 위의 누락된 Key Vault 섹션의 cmdlet을 사용하여 논리 SQL 서버에 추가된 키 uri를 식별하여 키 목록을 반환합니다.

마이그레이션: TDE 보호기가 AKV에 있는지 확인합니다.
- Key Vault를 식별하고 Azure Portal로 이동
- 키 uri로 식별되는 키가 있는지 확인합니다.

## <a name="missing-permissions"></a>누락된 권한 
오류 메시지: "401 AzureKeyVaultMissingPermissions - 서버에서 Azure Key Vault에 필요한 사용 권한이 누락되었습니다."

검색: 키 uri 및 Key Vault를 식별하는 방법
- 위의 누락된 Key Vault 섹션의 cmdlet을 통해 논리 SQL 서버에서 사용하는 Key Vault를 식별합니다.

마이그레이션: 논리 sql 서버에 Key Vault에 대한 사용 권한 및 키에 액세스할 수 있는 권한이 있는지 확인
- Azure Portal에서 Key Vault로 이동하여 액세스 정책으로 이동하고 Sql 서버 APPID를 찾습니다.  
  - APPID가 없는 경우 새로 추가 단추를 사용하여 추가합니다. 
  - APPID가 있는 경우 다음 키 사용 권한이 있는지 확인합니다. Get, 래핑 및 래핑 해제.
