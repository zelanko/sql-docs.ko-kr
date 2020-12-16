---
title: 호스트 보호 서비스에 컴퓨터 등록
description: 보안 Enclave를 사용하여 Always Encrypted의 호스트 보호 서비스에 SQL Server 컴퓨터를 등록합니다.
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1774e2b2a27b2b1f0c36b298f98c916318fd1543
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477654"
---
# <a name="register-computer-with-host-guardian-service"></a>호스트 보호 서비스에 컴퓨터 등록

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

이 문서에서는 증명하기 위해 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터를 HGS(호스트 보호 서비스)에 등록하는 방법을 설명합니다.

시작하기 전에 하나 이상의 HGS 컴퓨터를 배포하고 증명 서비스를 설정했는지 확인합니다.
자세한 내용은 [[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]에 대한 호스트 보호 서비스 배포](./always-encrypted-enclaves-host-guardian-service-deploy.md)를 참조하세요.

## <a name="step-1-install-the-attestation-client-components"></a>1단계: 증명 클라이언트 구성 요소 설치

SQL 클라이언트가 신뢰할 수 있는 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터와 통신하는지 확인할 수 있으려면 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터가 호스트 보호 서비스에서 성공적으로 증명되어야 합니다.
증명 프로세스는 HGS 클라이언트라는 선택적 Windows 구성 요소를 통해 관리됩니다.
아래 단계는 이 구성 요소를 설치하고 증명을 시작하는 데 도움이 됩니다.

1. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터가 [HGS 계획 문서에 개략적으로 설명된 필수 구성 요소](./always-encrypted-enclaves-host-guardian-service-plan.md#prerequisites)를 충족하는지 확인합니다.

2. 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행하여 HGS 클라이언트 및 증명 구성 요소가 포함된 호스트 보호 Hyper-V 지원 기능을 설치합니다.

    ```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
    ```

3. 설치를 완료하려면 다시 시작합니다.

## <a name="step-2-verify-virtualization-based-security-is-running"></a>2단계: 가상화 기반 보안이 실행 중인지 확인

호스트 보호 Hyper-V 지원 기능을 설치하면 VBS(가상화 기반 보안)가 자동으로 구성되고 사용하도록 설정됩니다.
[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] Always Encrypted용 enclave는 VBS 환경에서 보호되고 실행됩니다.
컴퓨터에 IOMMU 디바이스가 설치되고 사용하도록 설정되지 않으면 VBS를 시작할 수 없습니다.
VBS가 실행 중인지 확인하려면 `msinfo32.exe`를 실행하여 시스템 정보 도구를 열고 시스템 요약 아래쪽에서 `Virtualization-based security` 항목을 찾습니다.

![가상화 기반 보안 상태 및 구성을 보여 주는 시스템 정보 스크린샷](./media/always-encrypted-enclaves/msinfo32-vbs-status.png)

확인할 첫 번째 항목은 `Virtualization-based security`이며, 다음 세 개의 값을 포함할 수 있습니다.

- `Running`은 VBS가 올바르게 구성되고 성공적으로 시작할 수 있었음을 의미합니다. 컴퓨터에 이 상태가 표시되면 3단계로 건너뛸 수 있습니다.
- `Enabled but not running`은 VBS가 실행하도록 구성되었지만, 하드웨어에 VBS를 실행할 최소 보안 요구 사항이 없음을 의미합니다. IOMMU 같은 선택적 프로세서 기능을 사용하도록 설정하려면 BIOS 또는 UEFI에서 하드웨어 구성을 변경해야 할 수 있으며, 하드웨어가 실제로 필요한 기능을 지원하지 않는 경우에는 VBS 보안 요구 사항을 낮춰야 할 수 있습니다. 자세히 알아보려면 이 섹션을 계속 읽어보세요.
- `Not enabled`는 VBS가 실행하도록 구성되지 않았음을 의미합니다. 호스트 보호 Hyper-V 지원 기능은 VBS를 자동으로 사용하도록 설정하므로 이 상태가 표시되면 1단계를 반복하는 것이 좋습니다.

VBS가 컴퓨터에서 실행되고 있지 않으면 `Virtualization-based security` 속성을 확인합니다. `Required Security Properties` 항목의 값을 `Available Security Properties` 항목의 값과 비교합니다.
필수 속성은 VBS를 실행하는 데 사용할 수 있는 보안 속성과 같거나 해당 보안 속성의 하위 집합이어야 합니다.

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] enclave 증명의 컨텍스트에서 보안 속성의 중요도는 다음과 같습니다.

- `Base virtualization support`는 하이퍼바이저를 실행하는 데 필요한 최소 하드웨어 기능을 나타내므로 항상 필수입니다.
- `Secure Boot`는 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] Always Encrypted에 권장되지만 필수는 아닙니다. 보안 부팅은 UEFI 초기화가 완료된 후 즉시 Microsoft 서명된 부팅 로더를 실행하도록 요구하여 루트킷을 방지합니다. TPM(신뢰할 수 있는 플랫폼 모듈) 증명을 사용하는 경우 보안 부팅을 요구하도록 VBS를 구성할지 여부와 관계없이 보안 부팅 활성화가 측정되고 적용됩니다.
- `DMA Protection`은 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] Always Encrypted에 권장되지만 필수는 아닙니다. DMA 보호는 IOMMU를 사용하여 직접 메모리 액세스 공격을 방지하여 VBS 및 enclave 메모리를 보호합니다. 프로덕션 환경에서는 항상 DMA 보호가 적용된 컴퓨터를 사용해야 합니다. 개발/테스트 환경에서는 DMA 보호에 대한 요구 사항을 제거해도 됩니다. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 인스턴스가 가상화되면 DMA 보호를 사용하지 않을 가능성이 크며 VBS를 실행하려면 요구 사항을 제거해야 합니다. VM에서 실행하는 경우 낮춰진 보안 보증에 대한 자세한 내용은 [신뢰 모델](./always-encrypted-enclaves-host-guardian-service-plan.md#trust-model)을 검토하세요.

VBS에 필요한 보안 기능을 낮추기 전에 OEM 또는 클라우드 서비스 공급자에게 문의하여 UEFI 또는 BIOS에서 누락된 플랫폼 요구 사항을 사용하도록 설정하는 방법이 있는지 확인하세요(예: 보안 부팅, Intel VT-d 또는 AMD IOV 사용).

VBS에 필요한 플랫폼 보안 기능을 변경하려면 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행합니다.

```powershell
# Value 0 = No security features required (use this for Azure VMs)
# Value 1 = Only Secure Boot is required
# Value 2 = Only DMA protection is required (default configuration)
# Value 3 = Both Secure Boot and DMA protection are required
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name RequirePlatformSecurityFeatures -Value 0
```

레지스트리를 변경한 후 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터를 다시 시작하고 VBS가 다시 실행 중인지 확인합니다.

컴퓨터가 회사에서 관리되는 경우 다시 부팅한 후 그룹 정책 또는 Microsoft Endpoint Manager가 레지스트리 키 변경 내용을 재정의할 수 있습니다.
IT 지원 센터에 문의하여 VBS 구성을 관리하는 정책을 배포하는지 확인합니다.

## <a name="step-3-configure-the-attestation-url"></a>3단계: 증명 URL 구성

다음으로, HGS 증명 서비스의 URL을 사용하여 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터를 구성합니다.

관리자 권한 PowerShell 콘솔에서 다음 명령을 업데이트하고 실행하여 증명 URL을 구성합니다.

- `hgs.bastion.local`을 HGS 클러스터 이름으로 바꿉니다.
- HGS 컴퓨터에서 `Get-HgsServer`를 실행하여 클러스터 이름을 가져올 수 있습니다.
- 증명 URL은 항상 `/Attestation`으로 끝나야 합니다.
- SQL Server는 HGS의 키 보호 기능을 이용하지 않으므로 `http://localhost` 같은 더미 URL을 `-KeyProtectionServerUrl`에 제공합니다.

```powershell
Set-HgsClientConfiguration -AttestationServerUrl "https://hgs.bastion.local/Attestation" -KeyProtectionServerUrl "http://localhost"
```

이전에 이 머신을 HGS에 등록하지 않은 경우 명령은 증명 실패를 보고합니다. 이 결과는 정상적입니다.

Cmdlet 출력의 `AttestationMode` 필드는 HGS에서 사용하는 증명 모드를 나타냅니다.

[4A단계](#step-4a-register-a-computer-in-tpm-mode)를 계속 진행하여 TPM 모드에서 컴퓨터를 등록하거나 [4B단계](#step-4b-register-a-computer-in-host-key-mode)를 진행하여 호스트 키 모드에서 컴퓨터를 등록합니다.

## <a name="step-4a-register-a-computer-in-tpm-mode"></a>4A단계: TPM 모드에서 컴퓨터 등록

이 단계에서는 컴퓨터 TPM 상태에 대한 정보를 수집하고 HGS에 등록합니다.

HGS 증명 서비스가 호스트 키 모드를 사용하도록 구성된 경우에는 대신 [4B단계](#step-4b-register-a-computer-in-host-key-mode)로 건너뜁니다.

TPM 측정을 수집하기 전에 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터의 알려진 올바른 구성에서 작업하고 있는지 확인합니다.
컴퓨터에 필요한 하드웨어를 모두 설치하고 최신 펌웨어 및 소프트웨어 업데이트를 적용해야 합니다.
HGS는 컴퓨터가 증명될 때 이 기준에 따라 컴퓨터를 측정하므로 TPM 측정을 수집할 때 가장 안전하고 의도한 상태에 있는 것이 중요합니다.

TPM 증명을 위해 세 개의 데이터 파일이 수집되며 동일하게 구성된 컴퓨터를 사용하는 경우 파일 중 일부가 다시 사용될 수 있습니다.

| 증명 아티팩트 | 측정 항목 | 고유성 |
| -------------------- | ---------------- | ---------- |
| 플랫폼 식별자  | 컴퓨터의 TPM에 있는 공용 인증 키와 TPM 제조업체의 인증 키 인증서입니다. | 컴퓨터당 1개 |
| TPM 기준 | 부팅 프로세스 중 로드된 펌웨어 및 OS 구성을 측정하는 TPM의 PCR(플랫폼 제어 레지스터)입니다. 예제에는 보안 부팅 상태와 함께 크래시 덤프 암호화 여부가 포함됩니다. | 고유한 컴퓨터 구성마다 하나의 기준(동일한 하드웨어 및 소프트웨어가 동일한 기준을 사용할 수 있음) |
| 코드 무결성 검사 | 컴퓨터를 보호하기 위해 신뢰할 수 있는 [Windows Defender 애플리케이션 제어](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) 정책입니다. | 컴퓨터에 배포된 고유한 CI 정책당 1개 |

혼합된 하드웨어 및 소프트웨어 집합을 지원하기 위해 HGS에서 각 증명 아티팩트를 두 개 이상 구성할 수 있습니다.
HGS를 사용하려면 컴퓨터 증명이 각 정책 범주에 포함된 하나의 정책과 일치해야 합니다.
예를 들어 HGS에 세 개의 TPM 기준이 등록된 경우 컴퓨터 측정이 정책 요구 사항에 맞게 해당 기준 중 하나와 일치할 수 있습니다.

### <a name="configure-a-code-integrity-policy"></a>코드 무결성 검사 구성

HGS를 사용하려면 TPM 모드에서 증명되는 모든 컴퓨터에 WDAC(Windows Defender Application Control) 정책을 적용해야 합니다.
WDAC 코드 무결성 정책은 신뢰할 수 있는 게시자 및 파일 해시 목록에서 코드를 실행하려고 하는 각 프로세스를 확인하여 컴퓨터에서 실행할 수 있는 소프트웨어를 제한합니다.
[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 사용 사례의 경우 enclave는 가상화 기반 보안으로 보호되며 호스트 OS에서 수정될 수 없으므로, WDAC 정책의 엄격성은 암호화된 쿼리의 보안에 영향을 주지 않습니다.
따라서 시스템에 추가 제한을 적용하지 않고 증명 요구 사항을 충족하도록 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터에 간단한 감사 모드 정책을 배포하는 것이 좋습니다.

이미 컴퓨터에서 사용자 지정 WDAC 코드 무결성 검사를 사용하여 OS 구성을 강화하고 있는 경우 [TPM 증명 정보 수집](#collect-tpm-attestation-information)으로 건너뛸 수 있습니다.

1. 모든 Windows Server 2019, Windows 10 버전 1809 이상 운영 체제에서 미리 만들어진 예제 정책을 사용할 수 있습니다. `AllowAll` 정책은 컴퓨터에서 모든 소프트웨어를 제한 없이 실행하도록 허용합니다. 정책을 사용하려면 OS 및 HGS에서 인식하는 이진 형식으로 정책을 변환합니다. 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행하여 `AllowAll` 정책을 컴파일합니다.

    ```powershell
    # We are changing the policy to disable enforcement and user mode code protection before compiling
    $temppolicy = "$HOME\Desktop\allowall_edited.xml"
    Copy-Item -Path "$env:SystemRoot\schemas\CodeIntegrity\ExamplePolicies\AllowAll.xml" -Destination $temppolicy
    Set-RuleOption -FilePath $temppolicy -Option 0 -Delete
    Set-RuleOption -FilePath $temppolicy -Option 3

    ConvertFrom-CIPolicy -XmlFilePath $temppolicy -BinaryFilePath "$HOME\Desktop\allowall_cipolicy.bin"
    ```

2. [Windows Defender Application Control 배포 가이드](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)의 지침에 따라 [그룹 정책](/windows/security/threat-protection/windows-defender-application-control/deploy-windows-defender-application-control-policies-using-group-policy)을 사용하여 `allowall_cipolicy.bin` 파일을 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터에 배포합니다. 작업 그룹 컴퓨터의 경우 로컬 그룹 정책 편집기(`gpedit.msc`)를 사용하여 동일한 프로세스를 수행합니다.

3. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터에서 `gpupdate /force`를 실행하여 새 코드 무결성 검사를 구성한 다음, 컴퓨터를 다시 시작하여 정책을 적용합니다.

### <a name="collect-tpm-attestation-information"></a>TPM 증명 정보 수집

HGS를 사용하여 증명할 각 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터에서 다음 단계를 반복합니다.

1. 컴퓨터가 알려진 올바른 상태이면 PowerShell에서 다음 명령을 실행하여 TPM 증명 정보를 수집합니다.

    ```powershell
    # Collects the TPM EKpub and EKcert
    $name = $env:computername
    $path = "$HOME\Desktop"
    (Get-PlatformIdentifier -Name $name).Save("$path\$name-EK.xml")

    # Collects the TPM baseline (current PCR values)
    Get-HgsAttestationBaselinePolicy -Path "$path\$name.tcglog" -SkipValidation

    # Collects the applied CI policy, if one exists
    Copy-Item -Path "$env:SystemRoot\System32\CodeIntegrity\SIPolicy.p7b" -Destination "$path\$name-CIpolicy.bin"
    ```

2. 세 개의 증명 파일을 HGS 서버에 복사합니다.

3. HGS 서버의 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행하여 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터를 등록합니다.

    ```powershell
    # TIP: REMEMBER TO CHANGE THE FILENAMES
    # Registers the unique TPM with HGS (required for every computer)
    Add-HgsAttestationTpmHost -Path "C:\temp\SQL01-EK.xml"

    # Registers the TPM baseline (required ONCE for each unique hardware and software configuration)
    Add-HgsAttestationTpmPolicy -Name "MyHWSoftwareConfig" -Path "C:\temp\SQL01.tcglog"

    # Registers the CI policy (required ONCE for each unique CI policy)
    Add-HgsAttestationCiPolicy -Name "AllowAll" -Path "C:\temp\SQL01-CIpolicy.bin"
    ```

    > [!TIP]
    > 고유한 TPM 식별자를 등록하는 동안 오류가 발생하면 사용 중인 HGS 컴퓨터에서 [TPM 중간 및 루트 인증서를 가져왔는지](./always-encrypted-enclaves-host-guardian-service-deploy.md#switch-to-tpm-attestation) 확인합니다.

플랫폼 식별자, TPM 기준 및 코드 무결성 검사 외에도, HGS에서 구성 및 적용된 기본 제공 정책을 변경해야 할 수 있습니다.
해당 기본 제공 정책은 서버에서 수집하는 TPM 기준에 따라 측정되며 컴퓨터를 보호하기 위해 사용하도록 설정해야 하는 다양한 보안 설정을 나타냅니다.
DMA 공격을 방지할 IOMMU가 제공되지 않은 컴퓨터(예: VM)가 있는 경우 IOMMU 정책을 사용하지 않도록 설정해야 합니다.

IOMMU 요구 사항을 사용하지 않도록 설정하려면 HGS 서버에서 다음 명령을 실행합니다.

```powershell
Disable-HgsAttestationPolicy Hgs_IommuEnabled
```

> [!NOTE]
> IOMMU 정책을 사용하지 않도록 설정하면 HGS를 사용하여 증명하는 모든 컴퓨터에는 IOMMU가 필요하지 않습니다.
> 단일 컴퓨터에서만 IOMMU 정책을 사용하지 않도록 설정할 수는 없습니다.

다음 PowerShell 명령을 사용하여 등록된 TPM 호스트 및 정책 목록을 검토할 수 있습니다.

```powershell
Get-HgsAttestationTpmHost
Get-HgsAttestationTpmPolicy
```

## <a name="step-4b-register-a-computer-in-host-key-mode"></a>4B단계: 호스트 키 모드에서 컴퓨터 등록

이 단계에서는 호스트의 고유 키를 생성하고 HGS에 등록하는 프로세스를 안내합니다.
HGS 증명 서비스가 TPM 모드를 사용하도록 구성된 경우에는 대신 [4A단계](#step-4a-register-a-computer-in-tpm-mode)의 지침을 따르세요.

호스트 키 증명은 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터에서 비대칭 키 쌍을 생성하고 해당 키의 공개 키 부분만 HGS에 제공하는 방식으로 작동합니다.
키 쌍을 생성하려면 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행합니다.

```powershell
Set-HgsClientHostKey
Get-HgsClientHostKey -Path "$HOME\Desktop\$env:computername-key.cer"
```

이미 호스트 키를 만들었고 새 키 쌍을 생성하려는 경우에는 다음 명령을 대신 사용합니다.

```powershell
Remove-HgsClientHostKey
Set-HgsClientHostKey
Get-HgsClientHostKey -Path "$HOME\Desktop\$env:computername-key.cer"
```

호스트 키를 생성한 후에는 인증서 파일을 HGS 서버에 복사하고 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행하여 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터를 등록합니다.

```powershell
Add-HgsAttestationHostKey -Name "YourComputerName" -Path "C:\temp\yourcomputername.cer"
```

HGS를 사용하여 증명할 모든 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터에서 4B단계를 반복합니다.

## <a name="step-5-confirm-the-host-can-attest-successfully"></a>5단계: 호스트가 성공적으로 증명될 수 있는지 확인

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터를 HGS에 등록한 후에는(TPM 모드의 경우 [4A단계](#step-4a-register-a-computer-in-tpm-mode), 호스트 키 모드의 경우 [4B단계](#step-4b-register-a-computer-in-host-key-mode)) 성공적으로 증명할 수 있는지 확인해야 합니다.

언제든지 [Get-HgsClientConfiguration](/powershell/module/hgsclient/get-hgsclientconfiguration?view=win10-ps)을 사용하여 HGS 증명 클라이언트의 구성을 확인하고 증명 시도를 수행할 수 있습니다.
명령의 출력은 다음과 유사하게 표시됩니다.

```
PS C:\> Get-HgsClientConfiguration


IsHostGuarded                  : True
Mode                           : HostGuardianService
KeyProtectionServerUrl         : http://localhost
AttestationServerUrl           : http://hgs.bastion.local/Attestation
AttestationOperationMode       : HostKey
AttestationStatus              : Passed
AttestationSubstatus           : NoInformation
FallbackKeyProtectionServerUrl :
FallbackAttestationServerUrl   :
IsFallbackInUse                : False
```

출력에서 가장 중요한 두 개의 필드는 `AttestationStatus`(컴퓨터가 증명을 통과했는지 알려 줌) 및 `AttestationSubStatus`(컴퓨터가 증명에 실패한 경우 컴퓨터가 실패한 정책을 설명함)입니다.

`AttestationStatus`에 표시될 수 있는 가장 일반적인 값은 아래에 설명되어 있습니다.

| `AttestationStatus` | 설명 |
| ----------------- | ----------- |
| 만료됨 | 호스트가 이전에 증명을 통과했지만 발급된 상태 인증서가 만료되었습니다. 호스트 및 HGS 시간이 동기화되었는지 확인합니다. |
| `InsecureHostConfiguration` | 컴퓨터가 HGS 서버에 구성된 하나 이상의 증명 정책을 충족하지 않습니다. 자세한 내용은 `AttestationSubStatus`을 참조하세요. |
| NotConfigured | 컴퓨터가 증명 URL을 사용하여 구성되지 않았습니다. [증명 URL 구성](#step-3-configure-the-attestation-url) |
| 통과 | 컴퓨터가 증명을 통과했고 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] enclave를 실행하도록 신뢰할 수 있습니다. |
| `TransientError` | 임시 오류로 인해 증명 시도가 실패했습니다. 이 오류는 일반적으로 네트워크를 통해 HGS에 연결하는 데 문제가 있었음을 의미합니다. 네트워크 연결을 확인하고 컴퓨터가 HGS 서비스 이름을 확인하고 해당 이름으로 라우팅될 수 있는지 확인합니다. |
| `TpmError` | 증명을 시도하는 동안 컴퓨터의 TPM 디바이스에서 오류를 보고했습니다. 자세한 내용은 TPM 로그를 확인하세요. TPM을 지우면 문제가 해결될 수 있지만 TPM을 지우기 전에 주의해서 TPM을 사용하는 BitLocker 및 기타 서비스를 일시 중단합니다. |
| `UnauthorizedHost` | 호스트 키가 HGS에 알려지지 않습니다. [4B단계](#step-4b-register-a-computer-in-host-key-mode)의 지침에 따라 컴퓨터를 HGS에 등록합니다. |

`AttestationStatus`가 `InsecureHostConfiguration`를 표시하는 경우 `AttestationSubStatus` 필드는 실패한 하나 이상의 정책 이름으로 채워집니다.
다음 표에서는 가장 일반적인 값과 오류를 수정하는 방법을 설명합니다.

| AttestationSubStatus | 의미 및 수행할 작업 |
| -------------------- | ---------------------------- |
| CodeIntegrityPolicy | 컴퓨터의 코드 무결성 검사가 HGS에 등록되지 않았’거나’ 컴퓨터가 현재 코드 무결성 검사를 사용하고 있지 않습니다.  지침은 [코드 무결성 검사 구성](#configure-a-code-integrity-policy)을 참조하세요. |
| DumpsEnabled | 컴퓨터가 크래시 덤프를 허용하도록 구성되었지만 Hgs_DumpsEnabled 정책이 덤프를 허용하지 않습니다. 계속하려면 이 컴퓨터에서 덤프를 사용하지 않도록 설정하거나 Hgs_DumpsEnabled 정책을 사용하지 않도록 설정합니다. |
| FullBoot | 컴퓨터가 절전 모드 또는 최대 절전 모드에서 다시 시작되어 TPM 측정이 변경되었습니다. 컴퓨터를 다시 시작하여 클린 TPM 측정을 생성합니다. |
| HibernationEnabled | 컴퓨터가 암호화되지 않은 최대 절전 모드 파일을 사용하여 최대 절전 모드를 허용하도록 구성되었습니다. 이 문제를 해결하려면 컴퓨터에서 최대 절전 모드를 사용하지 않도록 설정합니다. |
| HypervisorEnforcedCodeIntegrityPolicy | 컴퓨터가 코드 무결성 검사를 사용하도록 구성되지 않았습니다. [그룹 정책] 또는 [로컬 그룹 정책] > [컴퓨터 구성] > [관리 템플릿] > [시스템] > [Device Guard] > [가상화 기반 보안 켜기] > [코드 무결성의 가상화 기반 보호]를 선택합니다. 이 정책 항목은 “UEFI 잠금 없이 사용”이어야 합니다. |
| Iommu | 이 컴퓨터에서 IOMMU 디바이스를 사용하도록 설정하지 않았습니다. 물리적 컴퓨터인 경우 UEFI 구성 메뉴에서 IOMMU를 사용하도록 설정합니다. 가상 머신이고 IOMMU를 사용할 수 없는 경우 HGS 서버에서 `Disable-HgsAttestationPolicy Hgs_IommuEnabled`를 실행합니다. |
| SecureBoot | 이 컴퓨터에서 보안 부팅이 사용하도록 설정되지 않았습니다. 이 오류를 해결하려면 UEFI 구성 메뉴에서 보안 부팅을 사용하도록 설정합니다. |
| VirtualSecureMode | 이 컴퓨터에서 가상화 기반 보안이 실행되고 있지 않습니다. [2단계: 컴퓨터에서 VBS가 실행 중인지 확인](#step-2-verify-virtualization-based-security-is-running)의 지침을 따릅니다. |