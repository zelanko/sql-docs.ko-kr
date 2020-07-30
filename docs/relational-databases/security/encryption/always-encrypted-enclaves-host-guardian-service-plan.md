---
title: 호스트 보호자 서비스 증명 계획
description: 보안 enclave를 사용하여 SQL Server Always Encrypted에 대한 호스트 보호 서비스 증명을 계획합니다.
ms.custom: ''
ms.date: 10/12/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 425fdeb973918744b4aeab423629939a2a84f97a
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411387"
---
# <a name="plan-for-host-guardian-service-attestation"></a>호스트 보호자 서비스 증명 계획

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[보안 enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)를 사용하는 경우 클라이언트 애플리케이션이 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 프로세스 내에서 신뢰할 수 있는 enclave와 통신하고 있는지 확인합니다. VBS(가상화 기반 보안) enclave의 경우 이 요구 사항에는 enclave 내의 코드가 둘 다 유효하고 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 호스트하는 컴퓨터를 신뢰할 수 있는지 확인하는 작업이 포함됩니다. 원격 증명은 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터의 ID 및 구성(선택 사항)의 유효성을 검사할 수 있는 제3자를 도입하여 이 목표를 달성합니다. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]는 enclave를 사용하여 쿼리를 실행하려면 먼저 증명 서비스에 운영 환경에 대한 정보를 제공하여 상태 인증서를 얻어야 합니다. 그러면 이 상태 인증서가 클라이언트에 전송되고 증명 서비스를 사용하여 신뢰성을 독립적으로 확인할 수 있습니다. 클라이언트는 상태 인증서를 신뢰하면 신뢰할 수 있는 VBS enclave와 통신하고 있는 것으로 판단하고 해당 enclave를 사용하는 쿼리를 실행하게 됩니다.

Windows Server 2019의 HGS(호스트 보호자 서비스) 역할은 VBS enclave를 사용하여 Always Encrypted에 대한 원격 증명 기능을 제공합니다.
이 문서에서는 VBS enclave 및 HGS 증명과 함께 Always Encrypted를 사용하기 위한 배포 전 결정 및 요구 사항을 안내합니다.

## <a name="architecture-overview"></a>아키텍처 개요

HGS(호스트 보호자 서비스)는 Windows Server 2019에서 실행되는 클러스터된 웹 서비스입니다.
일반적인 배포에는 1~3개의 HGS 서버, [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 하나 이상의 컴퓨터 및 클라이언트 애플리케이션 또는 도구(예: SQL Server Management Studio)를 실행하는 컴퓨터가 있습니다.
HGS는 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터를 신뢰할 수 있는지 확인하는 일을 담당하므로 보호하고 있는 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 인스턴스로부터 물리적 격리와 논리적 격리가 모두 필요합니다.
동일한 관리자가 HGS 및 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터에 액세스할 수 있는 경우 악의적인 컴퓨터에서 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하여 VBS enclave를 손상시킬 수 있도록 증명 서비스를 구성할 수 있습니다.

### <a name="hgs-domain"></a>HGS 도메인

HGS 설치 프로그램은 HGS 서버, 장애 조치(failover) 클러스터 리소스 및 관리자 계정에 대한 새 Active Directory 도메인을 자동으로 만듭니다.

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터는 도메인에 있을 필요가 없지만, 이 경우에는 HGS 서버에서 사용하는 것과 다른 도메인이어야 합니다.

### <a name="high-availability"></a>고가용성

HGS 기능은 자동으로 장애 조치(failover) 클러스터를 설치하고 구성합니다.
프로덕션 환경에서는 고가용성을 위해 3개의 HGS 서버를 사용하는 것이 좋습니다. 클러스터 쿼럼을 결정하는 방법과 외부 감시를 사용하는 두 노드 클러스터를 비롯한 대체 구성에 대한 자세한 내용은 [장애 조치(failover) 클러스터 설명서](https://docs.microsoft.com/windows-server/failover-clustering/manage-cluster-quorum)를 참조하세요.

HGS 노드 사이에는 공유 스토리지가 필요하지 않습니다. 증명 데이터베이스의 복사본은 각 HGS 서버에 저장되며 클러스터 서비스에서 네트워크를 통해 자동으로 복제합니다.

### <a name="network-connectivity"></a>네트워크 연결

SQL 클라이언트와 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]는 둘 다 HTTP를 통해 HGS와 통신할 수 있어야 합니다.
TLS 인증서를 사용하여 SQL 클라이언트와 HGS 간에, 그리고 SQL Server와 HGS 간에 이루어지는 모든 통신을 암호화하도록 HGS를 구성합니다.
이 구성을 사용하면 중간자(man-in-the-middle) 공격을 방지할 수 있으며 올바른 HGS 서버와 통신하게 됩니다.

HGS 서버는 증명 서비스 데이터베이스를 동기화 상태로 유지하기 위해 클러스터의 각 노드 간 연결이 필요합니다. 장애 조치(failover) 클러스터 모범 사례는 클러스터 통신을 위해 하나의 네트워크에서 HGS 노드를 연결하고 다른 클라이언트가 HGS와 통신할 수 있도록 별도의 네트워크를 사용하는 것입니다.

### <a name="attestation-modes"></a>증명 모드

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터는 HGS를 사용하여 증명을 시도할 때 먼저 HGS가 증명하는 방법을 확인합니다.
HGS는 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]와 함께 사용하기 위한 두 가지 증명 모드를 지원합니다.

| 증명 모드 | 설명 |
| ---------------- | ------- |
| TPM | TPM(신뢰할 수 있는 플랫폼 모듈) 증명은 HGS를 사용하여 증명하는 컴퓨터의 ID 및 무결성에 대해 가장 강력한 보증을 제공합니다. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터에 TPM 버전 2.0을 설치해야 합니다. 각 TPM 칩에는 특정 컴퓨터를 식별하는 데 사용할 수 있는 고유하고 변경할 수 없는 ID(인증 키)가 포함되어 있습니다. 또한 TPM은 컴퓨터의 부팅 프로세스를 측정하여 운영 체제에서 읽을 수 있지만 수정할 수 없는 보안 관련 측정값의 해시를 PCR(플랫폼 제어 레지스터)에 저장합니다. 이러한 측정값은 증명 과정에서 컴퓨터가 선언하는 보안 구성에 대한 암호화 증명을 제공합니다. |
| 호스트 키 | 호스트 키 증명은 비대칭 키 쌍을 사용하여 컴퓨터의 ID만 확인하는 간단한 증명 형식입니다. 개인 키가 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터에 저장되고, 공개 키가 HGS에 제공됩니다. 컴퓨터의 보안 구성이 측정되지 않고 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터에 TPM 2.0 칩이 필요하지 않습니다. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터에 설치된 개인 키를 보호하는 것이 중요합니다. 이 키를 획득하는 모든 사용자는 합법적인 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터와 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 내에서 실행되는 VBS enclave를 가장할 수 있습니다. |

일반적으로 권장 사항은 다음과 같습니다.

- **물리적 프로덕션 서버**의 경우 제공되는 추가 보증을 위해 TPM 증명을 사용하는 것이 좋습니다.
- **가상 프로덕션 서버**의 경우 대부분의 가상 머신에는 가상 TPM 또는 보안 부팅이 없으므로 호스트 키 증명을 권장합니다. [온-프레미스 보호된 VM](https://aka.ms/shieldedvms) 같이 보안이 강화된 VM을 사용하는 경우 TPM 모드를 사용하도록 선택할 수 있습니다. 모든 가상화된 배포에서 증명 프로세스는 VM 아래 가상화 플랫폼이 아닌 VM 환경만 분석합니다.
- **개발/테스트 시나리오**의 경우 버전을 더 쉽게 업그레이드할 수 있으므로 호스트 키 증명을 권장합니다.

### <a name="trust-model"></a>신뢰 모델

VBS enclave 신뢰 모델에서는 암호화된 쿼리 및 데이터를 소프트웨어 기반 enclave에서 평가하여 호스트 OS로부터 보호합니다.
이 enclave에 대한 액세스는 동일한 컴퓨터에서 실행되는 두 가상 머신에서 서로 다른 메모리에 액세스할 수 없는 것과 같은 방식으로 하이퍼바이저에 의해 보호됩니다.
클라이언트에서 합법적인 VBS 인스턴스와 통신하는 것을 신뢰하려면 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터에서 신뢰의 하드웨어 루트를 설정하는 TPM 기반 증명을 사용해야 합니다.
부팅 프로세스 중에 캡처되는 TPM 측정값에는 VBS 인스턴스의 고유 ID 키가 포함되어 상태 인증서가 정확한 컴퓨터에서만 유효합니다.
또한 VBS를 실행하는 컴퓨터에서 TPM을 사용할 수 있는 경우 VBS ID 키의 개인 부분은 TPM으로 보호되므로 아무도 VBS 인스턴스를 가장할 수 없습니다.

UEFI가 합법적인 Microsoft 서명 부팅 로더를 로드하고 루트킷이 하이퍼바이저 부팅 프로세스를 가로채지 않도록 TPM 증명에 보안 부팅이 필요합니다.
또한 직접 메모리 액세스를 사용하는 하드웨어 장치에서 enclave 메모리를 검사하거나 수정할 수 없도록 하려면 기본적으로 IOMMU 장치가 필요합니다.

이러한 보호는 모두 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터가 물리적 컴퓨터인 것으로 가정합니다.
[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터를 가상화하는 경우 VM의 메모리가 하이퍼바이저 또는 하이퍼바이저 관리자에 의한 검사에서 안전하다고 더 이상 보장할 수 없습니다. 예를 들어 하이퍼바이저 관리자는 VM의 메모리를 덤프하고 enclave의 쿼리 및 데이터의 일반 텍스트 버전에 액세스할 수 있습니다.
마찬가지로 VM에 가상 TPM이 있더라도 VM 운영 체제 및 부팅 환경의 상태와 무결성만 측정할 수 있습니다.
VM을 제어하는 하이퍼바이저의 상태는 측정할 수 없습니다.

그러나 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]가 가상화된 경우에도 enclave는 VM 운영 체제 내에서 발생하는 공격으로부터 보호됩니다.
하이퍼바이저 또는 클라우드 공급자를 신뢰하고 주로 중요한 데이터에 대한 데이터베이스 관리자 및 OS 관리자 공격에 대해 우려하는 경우 가상화된 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]가 요구 사항을 충족할 수 있습니다.

마찬가지로, 호스트 키 증명은 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터에 TPM 2.0 모듈이 설치되지 않은 경우 또는 보안이 가장 중요하지는 않은 개발/테스트 시나리오에서는 여전히 가치가 있습니다.
보안 부팅 및 TPM 1.2 모듈을 비롯하여 위에서 언급한 대부분의 보안 기능을 계속 사용하여 VBS와 운영 체제를 전체적으로 더 효과적으로 보호할 수 있습니다.
그러나 HGS가 컴퓨터에서 실제로 호스트 키 증명을 사용하여 이러한 설정을 사용하도록 설정했는지 확인할 수 없기 때문에 클라이언트는 실제로 호스트가 사용 가능한 모든 보호를 사용하고 있음을 확신할 수 없습니다.

## <a name="prerequisites"></a>사전 요구 사항

### <a name="hgs-server-prerequisites"></a>HGS 서버 필수 구성 요소

호스트 보호자 서비스 역할을 실행하는 컴퓨터는 다음 요구 사항을 충족해야 합니다.

| 구성 요소 | 요구 사항 |
| --------- | ----------- |
| 운영 체제 | Windows Server 2019 Standard 또는 Datacenter Edition |
| CPU | 코어 2개(최소), 코어 4개(권장) |
| RAM | 8GB(최소) |
| NIC | 고정 IP를 사용하는 NIC 2개(클러스터 트래픽용 1개, HGS 서비스용 1개) |

HGS는 암호화 및 암호 해독이 필요한 작업 수 때문에 CPU 바인딩된 역할입니다.
암호화 가속 기능을 제공하는 최신 프로세서를 사용하면 HGS 성능이 향상됩니다.
증명 데이터의 저장소 요구 사항은 고유 컴퓨터 증명당 10KB에서 1MB 사이입니다.

시작하기 전에 HGS 컴퓨터를 도메인에 가입시키지 마세요.

### <a name="ssnoversion-md-computer-prerequisites"></a>[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 컴퓨터 필수 구성 요소

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터는 [SQL Server 설치를 위한 요구 사항](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)과 [Hyper-V 하드웨어 요구 사항](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/hyper-v-requirements#hardware-requirements)을 모두 충족해야 합니다.

요구 사항은 다음과 같습니다.

- [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] 이상
- Windows 10 Enterprise 버전 1809 이상 또는 Windows Server 2019 Datacenter Edition. 다른 버전의 Windows 10 및 Windows Server는 HGS를 사용하는 증명을 지원하지 않습니다.
- 가상화 기술에 대한 CPU 지원:
  - Intel VT-x의 확장 페이지 테이블
  - AMD-V의 신속한 가상화 인덱싱
  - VM에서 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 경우 하이퍼바이저 및 실제 CPU에서 중첩된 가상화 기능을 제공해야 합니다. VM에서 VBS enclaves를 실행할 때 보증에 대한 자세한 내용은 [신뢰 모델](#trust-model) 섹션을 참조하세요.
    - Hyper-V 2016 이상에서는 [VM 프로세서에서 중첩된 가상화 확장을 사용하도록 설정](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization#configure-nested-virtualization)합니다.
    - Azure에서는 중첩된 가상화를 지원하는 VM 크기를 선택합니다. 모든 v3 시리즈 VM은 Dv3 및 Ev3와 같은 중첩된 가상화를 지원합니다. [중첩 지원 Azure VM 만들기](/azure/virtual-machines/windows/nested-virtualization#create-a-nesting-capable-azure-vm)를 참조하세요.
    - [VMware 설명서](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.vm_admin.doc/GUID-C2E78F3E-9DE2-44DB-9B0A-11440800AADD.html)에 설명된 대로 VMWare vSphere 6.7 이상에서 VM에 대한 가상화 기반 보안 지원을 사용하도록 설정합니다.
    - 다른 하이퍼바이저 및 퍼블릭 클라우드는 VBS Enclaves 함께 Always Encrypted를 사용할 수 있는 중첩된 가상화 기능을 지원할 수 있습니다. 호환성 및 구성 지침은 가상화 솔루션 설명서를 확인하세요.
- TPM 증명을 사용하려는 경우 서버에서 TPM 2.0 rev 1.16 칩을 사용할 수 있도록 준비해야 합니다. 지금은 HGS 증명이 TPM 2.0 rev 1.38 칩에서 작동하지 않습니다. 또한 TPM에 유효한 인증 키 인증서가 있어야 합니다.

## <a name="devtest-environment-considerations"></a>개발/테스트 환경 고려 사항

개발 또는 테스트 환경에서 VBS enclave를 사용하여 Always Encrypted를 사용하고 있고 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터에 대한 고가용성 또는 강력한 보호가 요구되지 않는 경우 간소화된 배포를 위해 다음과 같은 절충을 일부 또는 모두 적용할 수 있습니다.

- HGS의 노드를 하나만 배포합니다. HGS가 장애 조치(failover) 클러스터를 설치하는 경우에도 고가용성이 중요하지 않은 경우에는 노드를 더 추가할 필요가 없습니다.
- 더 간단한 설치 환경을 위해 TPM 모드 대신 호스트 키 모드를 사용합니다.
- HGS 및/또는 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]를 가상화하여 물리적 리소스를 절약합니다.
- [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]와 동일한 컴퓨터에서 보안 enclave를 사용한 Always Encrypted를 구성하기 위해 SSMS 또는 기타 도구를 실행합니다. 이렇게 하면 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]와 동일한 컴퓨터에 열 마스터 키가 남게 되므로 프로덕션 환경에서는 이 방법을 사용하면 안 됩니다.

## <a name="next-steps"></a>다음 단계

- [[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]에 대한 호스트 보호 서비스 배포](./always-encrypted-enclaves-host-guardian-service-deploy.md)
