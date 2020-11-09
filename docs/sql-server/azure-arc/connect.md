---
title: Azure Arc에 연결
titleSuffix: ''
description: Azure Arc에 SQL Server 인스턴스 연결
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: e80892bfef7ee2c8cf22aef1b491ab5ea0c0addd
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235567"
---
# <a name="connect-your-sql-server-to-azure-arc"></a>Azure Arc에 SQL Server 연결

다음 단계를 수행하여 온-프레미스에서 Azure Arc에 SQL Server 인스턴스를 연결할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

* 머신에 SQL Server 인스턴스가 하나 이상 설치되어 있습니다.
* Windows 머신의 경우 Azure PowerShell을 설치했습니다. 지침에 따라 [Azure PowerShell을 설치](/powershell/azure/install-az-ps)합니다.
* Linux 머신의 경우 Azure CLI를 다운로드하고 Azure 계정을 연결했습니다. 지침에 따라 [Azure CLI를 설치](/cli/azure/install-azure-cli-apt)합니다.
* **Microsoft.AzureData** 리소스 공급자가 등록되었습니다. 리소스 공급자에 관한 자세한 내용은 Azure 리소스 공급자 및 종류를 참조하세요.
    * PowerShell에서 `Register-AzResourceProvider -ProviderNamespace Microsoft.AzureData` 실행
    * Linux에서 `az provider register --namespace 'Microsoft.AzureData` 실행



## <a name="generate-a-registration-script-for-sql-server"></a>SQL Server용 등록 스크립트 생성

이 단계에서는 머신에 설치된 SQL Server 인스턴스를 모두 검색하여 __SQL Server - Azure Arc__ 리소스로 등록하는 스크립트를 생성합니다. 호스트하는 물리적 머신 또는 가상 머신이 Azure Arc에 등록되어 있지 않으면 스크립트에서 자동으로 등록합니다.

1. __SQL Server - Azure Arc__ 리소스 종류를 검색하고 만들기 블레이드를 통해 새 항목을 추가합니다.

![만들기 시작](media/join/start-creation-of-sql-server-azure-arc-resource.png)
    
2. 필수 조건을 검토하고 **서버 세부 정보** 탭으로 이동합니다.  

3. 구독, 리소스 그룹, Azure 지역, 호스트 운영 체제를 선택합니다. 필요한 경우 네트워크에서 인터넷 연결에 사용하는 프록시도 지정합니다.

> [!IMPORTANT]
> SQL Server 인스턴스를 호스트하는 머신이 이미 [Azure Arc에 연결](/azure/azure-arc/servers/onboard-portal)되어 있으면 해당 __머신 - Azure Arc__ 리소스가 포함된 것과 동일한 리소스 그룹을 선택해야 합니다.

![서버 세부 정보](media/join/server-details-sql-server-azure-arc.png)

4. **스크립트 실행** 탭으로 이동하여 표시된 등록 스크립트를 다운로드합니다. 포털에서 지정한 호스팅 OS용 스크립트를 생성합니다.

![스크립트 다운로드](media/join/download-script-sql-server-azure-arc.png)

## <a name="connect-the-installed-sql-server-instances-to-azure-arc"></a>설치된 SQL Server 인스턴스를 Azure Arc에 연결

이 단계에서는 Azure Portal에서 다운로드한 스크립트를 사용하고 대상 물리적 머신 또는 가상 머신에서 실행합니다. 그러면 머신에 설치된 각 SQL Server 인스턴스가 __SQL Server - Azure Arc__ 리소스로 등록됩니다. 또한 머신 자체에 게스트 구성 에이전트가 설치되어 있지 않으면 자동으로 설치되고 __머신 - Azure Arc__ 리소스로 등록됩니다.

> [!NOTE]
> [필수 조건](overview.md#prerequisites)에 설명된 최소 사용 권한 요구 사항을 충족하는 계정으로 스크립트를 실행해야 합니다.

### <a name="windows"></a>Windows

1. __powershell.exe__ 의 관리자 인스턴스를 시작하고 Azure 자격 증명으로 PowerShell 모듈에 로그인합니다. [로그인 지침](/powershell/azure/install-az-ps#sign-in)을 따릅니다.

2. 다운로드한 스크립트 실행

   ```powershell
   & '.\RegisterSqlServerArc.ps1'
   ```

   > [!NOTE]
   > PowerShell용 AZ 모듈을 이전에 설치하지 않은 경우에는 처음으로 문제가 발생할 수도 있습니다. 이 경우 스크립트의 지침에 따라 계정을 설치 및 연결하고 스크립트를 다시 실행합니다.

### <a name="linux"></a>Linux

1. Azure CLI를 사용하여 Azure 자격 증명으로 로그인합니다. [로그인 지침](/cli/azure/authenticate-azure-cli)을 따릅니다.

2. 다운로드한 스크립트에 실행 권한을 부여하고 실행합니다.

   ```bash
   sudo chmod +x ./RegisterSqlServerArc.sh
   ./RegisterSqlServerArc.sh
   ```

## <a name="register-sql-server-instances-on-multiple-machines"></a>여러 머신에 SQL Server 인스턴스 등록

단일 머신에 대해 생성한 것과 동일한 스크립트를 사용하여 여러 Windows 또는 Linux 머신에 설치된 여러 SQL Server 인스턴스를 Azure Arc에 연결할 수 있습니다. [SQL Server 인스턴스를 Azure Arc에 대규모로 연결](connect-at-scale.md)하는 방법에 대한 지침을 따릅니다.

## <a name="validate-the-sql-server---azure-arc-resources"></a>SQL Server - Azure Arc 리소스 유효성 검사

[Azure Portal](https://ms.portal.azure.com/#home)로 이동한 다음, 새로 등록된 __SQL Server - Azure Arc__ 리소스를 열어 유효성을 검사합니다.

![연결된 SQL Server 유효성 검사 ](media/join/validate-sql-server-azure-arc.png)

## <a name="un-register-the-sql-server---azure-arc-resources"></a>SQL Server - Azure Arc 리소스 등록 취소

기존 __SQL Server - Azure Arc__ 리소스를 제거하려면 해당 리소스가 포함된 리소스 그룹으로 이동하여 그룹의 리소스 목록에서 제거합니다.

![SQL Server 등록 취소](media/join/delete-sql-server-azure-arc.png)

## <a name="next-steps"></a>다음 단계

* [SQL Server 인스턴스에 대해 Advanced Data Security 구성](configure-advanced-data-security.md)

* [SQL Server 인스턴스에 대해 주문형 SQL 평가 구성](assess.md)