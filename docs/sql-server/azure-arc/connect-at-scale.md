---
title: SQL Server 인스턴스를 Azure Arc에 대규모로 연결
titleSuffix: ''
description: 이 문서에서는 서비스 주체를 사용하여 SQL Server 인스턴스를 Azure Arc 사용 SQL Server(미리 보기)로 연결하는 방법을 알아봅니다.
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 07b140aceae2eae1a63b826b0bb4f95c8cfc515b
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990356"
---
# <a name="connect-sql-server-instances-to-azure-arc-at-scale"></a>SQL Server 인스턴스를 Azure Arc에 대규모로 연결

[단일 머신에 대해 생성한 것과 동일한 스크립트](connect.md)를 사용하여 여러 Windows 또는 Linux 머신에 설치된 여러 SQL Server 인스턴스를 Azure Arc에 연결할 수 있습니다. 이 스크립트는 각 머신과 머신에 설치된 SQL Server 인스턴스를 Azure Arc에 연결하고 등록합니다. 최적의 환경을 위해 Azure Active Directory [서비스 주체](https://docs.microsoft.com/azure/active-directory/develop/app-objects-and-service-principals)를 사용하는 것이 좋습니다. 서비스 주체는 머신을 Azure에 연결하고 Azure Arc 사용 서버와 Azure Arc 사용 SQL Server에 대한 Azure 리소스를 만드는 데 필요한 최소한의 사용 권한만 부여된 특별한 제한된 관리 ID입니다. 이는 테넌트 관리자와 같은 더 높은 권한의 계정을 사용하는 것보다 안전하며, 액세스 제어 보안 모범 사례를 준수하는 것입니다.  

Connected Machine 에이전트를 설치하고 구성하는 설치 메서드는 사용하는 자동화 메서드에서 머신에 대한 관리자 권한을 요구합니다. Linux에서는 루트 계정을 사용하고 Windows에서는 로컬 관리자 그룹의 멤버여야 합니다.

시작하기 전에 [필수 조건](overview.md#prerequisites)을 검토하고 필요한 사용 권한을 충족하는 사용자 지정 역할을 만들었는지 확인합니다.

## <a name="connecting-multiple-sql-server-instances-on-windows-using-azure-powershell"></a>Azure PowerShell을 사용하여 Windows에서 여러 SQL Server 인스턴스 연결

각 머신에 [Azure PowerShell](/powershell/azure/install-az-ps)이 설치되어 있어야 합니다.

1. [`New-AzADServicePrincipal`](/powershell/module/az.resources/new-azadserviceprincipal) cmdlet을 통해 PowerShell을 사용하여 서비스 주체를 만듭니다. 출력을 변수에 저장해야 합니다. 그러지 않으면 나중에 필요한 암호를 검색할 수 없습니다.

    ```azurepowershell-interactive
    $sp = New-AzADServicePrincipal -DisplayName "Arc-for-servers" -Role <your custom role>
    $sp
    ```

    ```output
    Secret                : System.Security.SecureString
    ServicePrincipalNames : {ad9bcd79-be9c-45ab-abd8-80ca1654a7d1, https://Arc-for-servers}
    ApplicationId         : ad9bcd79-be9c-45ab-abd8-80ca1654a7d1
    ObjectType            : ServicePrincipal
    DisplayName           : Hybrid-RP
    Id                    : 5be92c87-01c4-42f5-bade-c1c10af87758
    Type                  :
    ```

   > [!NOTE]
   > 서비스 주체를 만들 때는 계정이 온보딩에 사용할 구독의 소유자 또는 사용자 액세스 관리자여야 합니다. 역할 할당을 만들 수 있는 충분한 권한이 없는 경우 서비스 주체가 생성될 수 있지만 머신을 온보딩할 수 없습니다. 사용자 지정 역할을 만드는 방법에 대한 지침은 [필요한 사용 권한](overview.md#required-permissions)에 나와 있습니다.

2. `$sp` 변수에 저장된 암호를 검색합니다.

   ```azurepowershell-interactive
   $credential = New-Object pscredential -ArgumentList "temp", $sp.Secret
   $credential.GetNetworkCredential().password
   ```
3. 서비스 주체의 테넌트 ID 값을 검색합니다.
 
   ```azurepowershell-interactive
   $tenantId= (Get-AzContext).Tenant.Id
   ```
4. 적절한 보안 방법을 사용하여 암호, 애플리케이션 ID, 테넌트 ID 값을 복사하고 저장합니다. 서비스 주체 암호를 잊어버린 경우 [`New-AzADSpCredential`](/powershell/module/azurerm.resources/new-azurermadspcredential) cmdlet을 사용하여 재설정할 수 있습니다.

   > [!NOTE]
   > 서버용 Azure Arc는 현재 인증서를 사용한 로그인을 지원하지 않으므로 서비스 주체에는 인증에 사용할 비밀이 있어야 합니다.

5. [Connect your SQL Server to Azure Arc](connect.md)(Azure Arc에 SQL Server 연결) 지침에 따라 Portal에서 PowerShell 스크립트를 다운로드합니다.

6. PowerShell ISE의 관리자 인스턴스에서 스크립트를 열고 앞에서 설명한 서비스 주체 프로비저닝 중에 생성된 값을 사용하여 다음 환경 변수를 바꿉니다. 처음에는 변수가 비어 있습니다.

   ```azurepowershell-interactive
   $servicePrincipalAppId="{serviceprincipalAppID}"
   $servicePrincipalSecret="{serviceprincipalPassword}"
   $servicePrincipalTenantId="{serviceprincipalTenantId}"
   ```

7. 각 대상 머신에서 스크립트를 실행합니다.

## <a name="connecting-multiple-sql-server-instances-on-linux-using-azure-cli"></a>Azure CLI를 사용하여 Linux에서 여러 SQL Server 인스턴스 연결

각 대상 머신에 [Azure CLI가 설치](/cli/azure/install-azure-cli)되어 있어야 합니다. 서비스 주체 자격 증명이 제공되었으며 이미 로그인한 다른 사용자가 없는 경우 등록 스크립트는 해당 자격 증명을 사용하여 Azure에 자동으로 로그인합니다. 다음 단계를 수행하여 여러 Linux 머신의 SQL Server 인스턴스를 연결합니다.

1. [‘az ad sp create-for-rbac’](/cli/azure/ad/sp.md#az_ad_sp_create_for_rbac) 명령을 사용하여 서비스 주체를 만듭니다. 

   ```azurecli-interactive
   az ad sp create-for-rbac --name <your service principal name> --role <your custom role name>    
   ```

   ```output
   { "appId": "d2ff754a-e10a-4eb6-9cdc-ce6e7a4687db",
     "displayName": "Arc-for-servers",
     "name": "http://Arc-for-servers",
     "password": {SomeRandomlyGeneratedPassword}",
     "tenant": "2530e75f-673b-4841-8270-47ca6a34ef4f"
   }
   ```

   > [!NOTE]
   > 서비스 주체를 만들 때는 계정이 온보딩에 사용할 구독의 소유자 또는 사용자 액세스 관리자여야 합니다. 역할 할당을 만들 수 있는 충분한 권한이 없는 경우 서비스 주체가 생성될 수 있지만 머신을 온보딩할 수 없습니다. 사용자 지정 역할을 만드는 방법에 대한 지침은 [필요한 사용 권한](overview.md#required-permissions)에 나와 있습니다.

2. [Connect your SQL Server to Azure Arc](connect.md)(Azure Arc에 SQL Server 연결) 지침에 따라 Portal에서 Linux 셸 스크립트를 다운로드합니다.

3. ‘az ad sp create-for-rbac’ 명령에서 반환된 값을 사용하여 스크립트의 다음 변수를 바꿉니다. 처음에는 변수가 비어 있습니다.

   ```bash
   servicePrincipalAppId="{serviceprincipalAppID}"
   servicePrincipalSecret="{serviceprincipalPassword}"
   servicePrincipalTenant="{serviceprincipalTenant}"
   ```

3. 각 대상 머신에서 스크립트를 실행합니다.
 
   ```bash
   sudo chmod +x ./RegisterSqlServerArc.sh
   ./RegisterSqlServerArc.sh
   ```

## <a name="validate-successful-onboarding"></a>온보딩 성공 확인

Azure Arc 사용 SQL Server(미리 보기)를 사용하여 SQL Server 인스턴스를 등록한 후 [Azure Portal](https://aka.ms/azureportal)로 이동하여 새로 만든 Azure Arc 리소스를 확인합니다. 연결된 각 머신에 대한 새 __머신 - Azure Arc__ 및 등록된 각 SQL Server 인스턴스에 대한 새 __SQL Server - Azure Arc__ 리소스가 표시됩니다. 

![온보딩 성공](./media/join-at-scale/successful-onboard.png)

## <a name="next-steps"></a>다음 단계

- [Azure Policy](/azure/governance/policy/overview)를 사용하여 머신을 관리하는 방법을 알아봅니다(예: VM [게스트 구성](/azure/governance/policy/concepts/guest-configuration), 머신이 예상되는 Log Analytics 작업 영역에 보고되는지 확인, [VM을 사용한 Azure Monitor](/azure/azure-monitor/insights/vminsights-enable-policy)로 모니터링 등).

- [Log Analytics 에이전트](/azure/azure-monitor/platform/log-analytics-agent)에 대해 자세히 알아보세요. 머신에서 실행되는 OS 및 워크로드를 사전에 모니터링하거나, 자동화 Runbook 또는 업데이트 관리 같은 솔루션을 사용하여 관리하거나, [Azure Security Center](/azure/security-center/security-center-intro) 같은 다른 Azure 서비스를 사용하려는 경우에는 Windows 및 Linux용 Log Analytics 에이전트가 필요합니다.

- [SQL Server 인스턴스에 대해 주문형 SQL 평가를 사용한 주기적 환경 상태 검사를 구성](assess.md)하는 방법을 알아봅니다.

- [SQL Server 인스턴스에 대해 Advanced Data Security를 구성](configure-advanced-data-security.md)하는 방법을 알아봅니다.
