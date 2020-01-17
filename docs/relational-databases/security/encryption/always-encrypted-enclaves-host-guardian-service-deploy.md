---
title: 호스트 보호 서비스 배포
description: 보안 Enclave를 사용하여 Always Encrypted의 호스트 보호 서비스 배포
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6794f5fd57d1c89e7c1989e79b5072a8c15cf43e
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74320056"
---
# <a name="deploy-the-host-guardian-service-for-include-ssnoversion-mdincludesssnoversion-mdmd"></a>[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]에 대한 호스트 보호 서비스 배포

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

이 문서에서는 HGS(호스트 보호 서비스)를 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]에 대한 증명 서비스로 배포하는 방법을 설명합니다.
시작하기 전에 필수 구성 요소 및 아키텍처 지침의 전체 목록을 보려면 [호스트 보호 서비스 증명 계획](./always-encrypted-enclaves-host-guardian-service-plan.md) 문서를 읽어보세요.

## <a name="step-1-set-up-the-first-hgs-computer"></a>1단계: 첫 번째 HGS 컴퓨터 설정

HGS(호스트 보호 서비스)는 하나 이상의 컴퓨터에서 클러스터된 서비스로 실행됩니다.
이 단계에서는 첫 번째 컴퓨터에서 새 HGS 클러스터를 설정합니다.
이미 HGS 클러스터가 있고 고가용성을 위해 클러스터에 컴퓨터를 추가하는 경우 [2단계: 클러스터에 더 많은 HGS 컴퓨터 추가](#step-2-add-more-hgs-computers-to-the-cluster)로 이동합니다.

시작하기 전에 사용 중인 컴퓨터가 Windows Server 2019 Standard 또는 Datacenter Edition을 실행하고 있고, 로컬 관리자 권한이 있으며, 컴퓨터가 Active Directory 도메인에 아직 가입되지 않았는지 확인합니다.

1. 로컬 관리자로 첫 번째 HGS 컴퓨터에 로그인하고 관리자 권한 Windows PowerShell 콘솔을 엽니다. 다음 명령을 실행하여 호스트 보호 서비스 역할을 설치합니다. 변경 내용을 적용하기 위해 컴퓨터가 자동으로 다시 시작됩니다.

    ```powershell
    Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
    ```

2. HGS 컴퓨터가 다시 시작된 후 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행하여 새 Active Directory 포리스트를 설치합니다.

    ```powershell
    # Select the name for your new Active Directory root domain.
    # Make sure the name does not conflict with, and is not subordinate to, any existing domains on your network.
    $HGSDomainName = 'bastion.local'

    # Specify a Directory Services Restore Mode password that can be used to recover your domain in safe mode.
    # This password is not, and will not change, your admin account password.
    # Save this password somewhere safe and include it in your disaster recovery plan.
    $DSRMPassword = Read-Host -AsSecureString -Prompt "Directory Services Restore Mode Password"

    Install-HgsServer -HgsDomainName $HgsDomainName -SafeModeAdministratorPassword $DSRMPassword -Restart
    ```

    Active Directory 포리스트 구성을 완료하기 위해 HGS 컴퓨터가 다시 시작됩니다. 다음에 로그인할 때 관리자 계정은 도메인 관리자 계정이 됩니다. 새 포리스트를 관리하고 보안을 설정하는 방법에 대한 자세한 내용은 [Active Directory Domain Services 작업 문서](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/ad-ds-operations)를 검토하는 것이 좋습니다.

3. 다음으로, 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행하여 HGS 클러스터를 설정하고 증명 서비스를 설치합니다.

    ```powershell
    # Note: the name you provide here will be shared by all HGS nodes and used to point your SQL Server computers to the HGS cluster.
    # For example, if you provide "attsvc" here, a DNS record for "attsvc.yourdomain.com" will be created for every HGS computer.
    Initialize-HgsAttestation -HgsServiceName 'hgs'
    ```

## <a name="step-2-add-more-hgs-computers-to-the-cluster"></a>2단계: 클러스터에 더 많은 HGS 컴퓨터 추가

첫 번째 HGS 컴퓨터와 클러스터가 설정되면 다른 HGS 서버를 추가하여 고가용성을 제공할 수 있습니다.
예를 들어 개발/테스트 환경에서 HGS 서버를 하나만 설정하는 경우 3단계로 건너뛸 수 있습니다.

첫 번째 HGS 컴퓨터와 마찬가지로, 클러스터에 가입 중인 컴퓨터가 Windows Server 2019 Standard 또는 Datacenter Edition을 실행하고 있고, 로컬 관리자 권한이 있으며, 컴퓨터가 Active Directory 도메인에 아직 가입되지 않았는지 확인합니다.

1. 로컬 관리자로 컴퓨터에 로그인하고 관리자 권한 Windows PowerShell 콘솔을 엽니다. 다음 명령을 실행하여 호스트 보호 서비스 역할을 설치합니다. 변경 내용을 적용하기 위해 컴퓨터가 자동으로 다시 시작됩니다.

    ```powershell
    Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
    ```

2. 컴퓨터의 DNS 클라이언트 구성을 확인하여 HGS 도메인을 확인할 수 있는지 확인합니다. 다음 명령은 HGS 서버의 IP 주소를 반환해야 합니다. HGS 도메인을 확인할 수 없는 경우 이름 확인에 HGS DNS 서버를 사용하도록 네트워크 어댑터에서 DNS 서버 정보를 업데이트해야 할 수 있습니다.

    ```powershell
    # Change 'bastion.local' to the domain name you specified in Step 1.2
    nslookup bastion.local

    # If it fails, use sconfig.exe, option 8, to set the first HGS computer as your preferred DNS server.
    ```

3. 컴퓨터가 다시 시작된 후 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행하여 첫 번째 HGS 서버에서 만든 Active Directory 도메인에 컴퓨터를 가입시킵니다. 이 명령을 실행하려면 AD 도메인의 도메인 관리자 자격 증명이 필요합니다. 명령이 완료되면 컴퓨터가 다시 시작되고 머신은 HGS 도메인의 Active Directory 도메인 컨트롤러가 됩니다.

    ```powershell
    # Provide the fully qualified HGS domain name
    $HGSDomainName = 'bastion.local'

    # Provide a domain administrator's credential for the HGS domain
    $DomainAdminCred = Get-Credential

    # Specify a Directory Services Restore Mode password that can be used to recover your domain in safe mode.
    # This password is not, and will not change, your admin account password.
    # Save this password somewhere safe and include it in your disaster recovery plan.
    $DSRMPassword = Read-Host -AsSecureString -Prompt "Directory Services Restore Mode Password"

    Install-HgsServer -HgsDomainName $HgsDomainName -HgsDomainCredential $DomainAdminCred -SafeModeAdministratorPassword $DSRMPassword -Restart
    ```

4. 컴퓨터가 다시 시작된 후 도메인 관리자 자격 증명을 사용하여 로그인합니다. 관리자 권한 Windows PowerShell 콘솔을 열고 다음 명령을 실행하여 증명 서비스를 구성합니다. 증명 서비스는 클러스터를 인식하므로 다른 클러스터 구성원의 구성을 복제합니다. HGS 노드에서 증명 정책의 변경 내용은 다른 모든 노드에 적용됩니다.

    ```powershell
    # Provide the IP address of an existing, initialized HGS server
    # If you are using separate networks for cluster and application traffic, choose an IP address on the cluster network.
    # You can find the IP address of your HGS server by signing in and running "ipconfig /all"
    Initialize-HgsAttestation -HgsServerIPAddress '172.16.10.20'
    ```

5. HGS 클러스터에 추가하려는 모든 컴퓨터에서 2단계를 반복합니다.

## <a name="step-3-configure-a-dns-forwarder-to-your-hgs-cluster"></a>3단계: HGS 클러스터에 대한 DNS 전달자 구성

HGS는 증명 서비스를 확인하는 데 필요한 이름 레코드를 포함하는 자체 DNS 서버를 실행합니다.
요청을 HGS DNS 서버로 전달하도록 네트워크의 DNS 서버를 구성할 때까지는 SQL Server 컴퓨터에서 해당 레코드를 확인할 수 없습니다.

DNS 전달자를 구성하는 프로세스는 공급업체마다 다르므로, 네트워크 관리자에게 특정 네트워크에 대한 올바른 지침을 문의하는 것이 좋습니다.

회사 네트워크에 Windows Server DNS 서버 역할을 사용하는 경우 DNS 관리자는 HGS 도메인에 대한 요청만 전달되도록 HGS 도메인에 대한 조건부 전달자를 만들 수 있습니다.
예를 들어 HGS 서버가 “bastion.local” 도메인 이름을 사용하고 IP 주소 172.16.10.20, 172.16.10.21 및 172.16.10.22를 사용하는 경우 회사 DNS 서버에서 다음 명령을 실행하여 조건부 전달자를 구성할 수 있습니다.

```powershell
# Tip: make sure to provide every HGS server's IP address
# If you use separate NICs for cluster and application traffic, use the application traffic NIC IP addresses here
Add-DnsServerConditionalForwarderZone -Name 'bastion.local' -ReplicationScope "Forest" -MasterServers "172.16.10.20", "172.16.10.21", "172.16.10.22"
```

## <a name="step-4-configure-the-attestation-service"></a>4단계: 증명 서비스 구성

HGS는 다음과 같은 두 가지 증명 모드를 지원합니다. 각 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터의 무결성 및 ID에 대한 암호화 확인을 위한 TPM 증명 및 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터 ID의 간단한 확인을 위한 호스트 키 증명.
증명 모드를 아직 선택하지 않은 경우 각 모드의 보안 보증 및 사용 사례에 대한 자세한 내용은 [계획 가이드](./always-encrypted-enclaves-host-guardian-service-plan.md#attestation-modes)의 증명 정보를 확인하세요.

이 섹션의 단계에서는 특정 증명 모드의 기본 증명 정책을 구성합니다.
4단계에서 호스트 관련 정보를 등록합니다.
나중에 증명 모드를 변경해야 하는 경우 원하는 증명 모드를 사용하여 3단계와 4단계를 반복합니다.

### <a name="switch-to-tpm-attestation"></a>TPM 증명으로 전환

HGS에서 TPM 증명을 구성하려면 인터넷에 액세스할 수 있는 컴퓨터 및 TPM 2.0 수정 1.16 칩이 있는 하나 이상의 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터가 필요합니다.

TPM 모드를 사용하도록 HGS를 구성하려면 관리자 권한 PowerShell 콘솔을 열고 다음 명령을 실행합니다.

```powershell
Set-HgsServer -TrustTpm
```

이제 클러스터의 모든 HGS 컴퓨터는 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터가 증명을 시도할 때 TPM 모드를 사용합니다.

SQL Server 컴퓨터에서 HGS에 TPM 정보를 등록하려면 먼저 TPM 공급업체의 EK(인증 키) 루트 인증서를 설치해야 합니다.
각 물리적 TPM은 제조업체를 식별하는 인증 키 인증서와 함께 제공되는 고유한 인증 키를 사용하여 팩터리에서 구성됩니다.
이 인증서는 TPM이 정품임을 보장합니다.
HGS는 인증서 체인을 신뢰할 수 있는 루트 인증서 목록과 비교하여 새 TPM을 HGS에 등록할 때 인증 키 인증서를 확인합니다.

Microsoft는 HGS 신뢰할 수 있는 TPM 루트 인증서 저장소로 가져올 수 있는 알려진 올바른 TPM 공급업체 루트 인증서 목록을 게시합니다.
SQL Server 컴퓨터가 가상화되는 경우 가상 TPM 인증 키에 대한 인증서 체인을 가져오는 방법에 대한 정보는 클라우드 서비스 공급자 또는 가상화 플랫폼 공급업체에 문의해야 합니다.

물리적 TPM용으로 신뢰할 수 있는 TPM 루트 인증서 패키지를 Microsoft에서 다운로드하려면 다음 단계를 완료합니다.

1. 인터넷에 액세스할 수 있는 컴퓨터에 [https://go.microsoft.com/fwlink/?linkid=2097925](https://go.microsoft.com/fwlink/?linkid=2097925)에서 최신 TPM 루트 인증서 패키지를 다운로드합니다.

2. Cab 파일의 서명을 확인하여 정품인지 확인합니다.

    ```powershell
    # Note: replace the path below with the correct one to the file you downloaded in step 1
    Get-AuthenticodeSignature ".\TrustedTpm.cab"
    ```

    > [!WARNING]
    > 서명이 유효하지 않은 경우에는 계속 진행하지 말고 Microsoft 지원에 문의하세요.

3. Cab 파일을 새 디렉터리로 확장합니다.

    ```powershell
    mkdir .\TrustedTpmCertificates
    expand.exe -F:* ".\TrustedTpm.cab" ".\TrustedTpmCertificates"
    ```

4. 새 디렉터리에 각 TPM 공급업체의 디렉터리가 표시됩니다. 사용하지 않는 공급업체의 디렉터리를 삭제할 수 있습니다.

5. 전체 “TrustedTpmCertificates” 디렉터리를 HGS 서버에 복사합니다.

6. HGS 서버에서 관리자 권한 PowerShell 콘솔을 열고 다음 명령을 실행하여 모든 TPM 루트 및 중간 인증서를 가져옵니다.

    ```powershell
    # Note: replace the path below with the correct location of the TrustedTpmCertificates folder on your HGS computer
    cd "C:\scratch\TrustedTpmCertificates"
    .\setup.cmd
    ```

7. 모든 HGS 컴퓨터에서 5단계와 6단계를 반복합니다.

OEM, 클라우드 서비스 공급자 또는 가상화 플랫폼 공급업체에서 중간 및 루트 CA 인증서를 가져온 경우 각 로컬 머신 인증서 저장소인 `TrustedHgs_RootCA` 또는 `TrustedHgs_IntermediateCA`에 인증서를 직접 가져올 수 있습니다. 예를 들어 PowerShell에서 다음을 수행합니다.

```powershell
# Imports MyCustomTpmVendor_Root.cer to the local machine's "TrustedHgs_RootCA" store
Import-Certificate -FilePath ".\MyCustomTpmVendor_Root.cer" -CertStoreLocation "Cert:\LocalMachine\TrustedHgs_RootCA"
```

### <a name="switch-to-host-key-attestation"></a>호스트 키 증명으로 전환

호스트 키 증명을 사용하려면 HGS 서버의 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행합니다.

```powershell
Set-HgsServer -TrustHostKey
```

이제 클러스터의 모든 HGS 컴퓨터는 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터가 증명을 시도할 때 호스트 키 모드를 사용합니다.

## <a name="step-5-configure-the-hgs-https-binding"></a>5단계: HGS HTTPS 바인딩 구성

기본 설치에서 HGS는 HTTP(포트 80) 바인딩만 공개합니다.
[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터와 HGS 간에 모든 통신을 암호화하도록 HTTPS(포트 443) 바인딩을 구성할 수 있습니다.
HGS의 모든 프로덕션 인스턴스는 HTTPS 바인딩을 사용하는 것이 좋습니다.

1. 1\.3단계의 정규화된 HGS 서비스 이름을 주체 이름으로 사용하여 인증 기관에서 TLS 인증서를 가져옵니다. 서비스 이름을 모르는 경우 HGS 컴퓨터에서 `Get-HgsServer`를 실행하여 찾을 수 있습니다. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터가 다른 DNS 이름을 사용하여 HGS 클러스터에 연결하는 경우(예: HGS가 다른 주소를 사용하는 네트워크 부하 분산 장치 뒤에 있는 경우) 대체 DNS 이름을 주체 대체 이름 목록에 추가할 수 있습니다.

2. HGS 컴퓨터에서 [Set-HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/set-hgsserver)를 사용하여 HTTPS 바인딩을 사용하도록 설정하고 이전 단계에서 가져온 TLS 인증서를 지정합니다. 인증서가 컴퓨터의 로컬 인증서 저장소에 이미 설치된 경우 다음 명령을 사용하여 HGS에 등록합니다.

    ```powershell
    # Note: you'll need to know the thumbprint for your certificate to configure HGS this way
    Set-HgsServer -Http -Https -HttpsCertificateThumbprint "54A043386555EB5118DB367CFE38776F82F4A181"
    ```

    인증서(프라이빗 키 포함)를 암호로 보호된 PFX 파일로 내보낸 경우 다음 명령을 실행하여 HGS에 등록할 수 있습니다.

    ```powershell
    $PFXPassword = Read-Host -AsSecureString -Prompt "PFX Password"
    Set-HgsServer -Http -Https -HttpsCertificatePath "C:\path\to\hgs_tls.pfx" -HttpsCertificatePassword $PFXPassword
    ```

3. 클러스터의 각 HGS 컴퓨터에서 1단계와 2단계를 반복합니다. TLS 인증서는 HGS 노드 간에 자동으로 복제되지 않습니다. 또한 각 HGS 컴퓨터는 주체가 HGS 서비스 이름과 일치하는 경우 고유한 TLS 인증서를 포함할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [HGS에 컴퓨터 등록](./always-encrypted-enclaves-host-guardian-service-register.md)
