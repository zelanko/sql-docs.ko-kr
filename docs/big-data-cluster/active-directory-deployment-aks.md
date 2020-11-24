---
title: AKS(Azure Kubernetes Services)의 Active Directory에서 배포
titleSuffix: SQL Server Big Data Cluster
description: AKS(Azure Kubernetes Services)의 AD 모드에서 SQL Server 빅 데이터 클러스터를 배포하는 방법에 대한 개념 및 계획 정보를 설명합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 11/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3f6b3ce5f6a594e5be385ee1f7ea7d1c03c1f92a
ms.sourcegitcommit: 0f484f32709a414f05562bbaafeca9a9fc57c9ed
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632969"
---
# <a name="deploy-sql-server-big-data-clusters-in-ad-mode-on-azure-kubernetes-services-aks"></a>AKS(Azure Kubernetes Services)의 AD 모드에서 SQL Server 빅 데이터 클러스터 배포

SQL Server 빅 데이터 클러스터는 **IAM(ID 및 액세스 관리)** 을 위한 [AD(Active Directory) 배포 모드](deploy-active-directory.md)를 지원합니다. **AKS(Azure Kubernetes Service)** 의 IAM은 Microsoft ID 플랫폼에서 광범위하게 지원하는 OAuth 2.0 및 OpenID Connect 같은 산업 표준 프로토콜이 SQL Server에서는 지원되지 않기 때문에 어려움이 있었습니다.  

이 문서에서는 [AKS(Azure Kubernetes Service)](/azure/aks/intro-kubernetes)에서 배포하는 동안 AD 모드에서 BDC(빅 데이터 클러스터)를 배포하는 방법을 설명합니다. 

## <a name="architecture-topologies"></a>아키텍처 토폴로지

**AD DS(Active Directory Domain Services)** 는 여러 온-프레미스 인스턴스에서 실행되는 것과 [동일한 방식](/windows-server/identity/ad-ds/deploy/virtual-dc/adds-on-azure-vm)으로 Azure VM(가상 머신)에서 실행됩니다.  Azure에서 새 도메인 컨트롤러의 수준을 올린 후 가상 네트워크의 기본 및 보조 DNS 서버를 설정하면 온-프레미스 DNS 서버 수준이 3차 이상으로 내려갑니다. AD 인증을 통해 [Linux의 도메인 조인 클라이언트는 도메인 자격 증명 및 Kerberos 프로토콜을 사용하여 SQL Server에서 인증](../linux/sql-server-linux-active-directory-auth-overview.md)을 받을 수 있습니다.

AKS의 AD 모드에서 BDC를 배포하는 몇 가지 방법이 있습니다.  이 문서에서는 보다 쉽게 구현하고 기존 엔터프라이즈급 아키텍처와 통합하는 두 가지 방법을 소개합니다.

* **온-프레미스 Active Directory 도메인을 Azure로 확장합니다.** 이 방법을 사용하면 [Active Directory 환경](/azure/architecture/reference-architectures/identity/adds-extend-domain)에서 Azure의 AD DS(Active Directory Domain Services)를 사용하여 분산 인증 서비스를 제공할 수 있습니다. 온-프레미스 AD DS(Active Directory Domain Services)를 복제하여 인증 요청을 클라우드에서 온-프레미스 AD DS로 되돌려 보낼 때 발생하는 대기 시간을 줄입니다. 이 솔루션은 일반적으로 애플리케이션의 일부는 온-프레미스로 호스트되고 일부는 Azure에서 호스트되어 그 사이에서 인증 요청을 주고받아야 하는 경우에 사용됩니다.

   [이 참조 아키텍처](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-extend-domain)에서 이 솔루션을 배포하는 단계별 방법을 참조하세요.

* **AD DS(Active Directory Domain Services) 리소스 포리스트를 Azure로 확장합니다.** 이 아키텍처에서는 온-프레미스 AD 포리스트에서 신뢰하는 새 도메인을 Azure에 만듭니다. 이 아키텍처에서는 [Azure의 도메인에서 온-프레미스 포리스트로의 단방향 트러스트](/azure/architecture/reference-architectures/identity/adds-forest)를 보여 줍니다.

   이 트러스트를 통해 온-프레미스 사용자는 Azure의 도메인에 있는 리소스에 액세스할 수 있습니다. [이 참조 아키텍처](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-forest)에서 이 솔루션을 배포하는 단계별 방법을 참조하세요.

위에서 설명한 참조 아키텍처를 사용하면 랜딩 존을 만들어 처음부터 모든 리소스를 배포하거나 기존 아키텍처를 기반으로 추가 해결 방법을 만들 수 있습니다. 이러한 참조 아키텍처 외에도 대상 VNet 또는 피어링된 VNet에 유지되는 별도의 서브넷에 있는 AKS 클러스터에 BDC를 배포해야 합니다.

다음 이미지는 일반적인 아키텍처를 나타냅니다.

:::image type="content" source="media/active-directory-deployment-aks/ad-in-aks-diagram.png" alt-text="AD 및 SQL Server 빅 데이터 클러스터를 사용하는 AKS 클러스터":::

## <a name="recommendations"></a>권장 사항

다음 권장 사항은 AKS의 AD 모드에서 수행되는 대부분의 BDC 배포에 적용됩니다. 구성 요소마다 사용 가능한 옵션을 설명하여 더 효과적으로 엔터프라이즈급 아키텍처와 통합할 수 있는 지침을 제공합니다.

### <a name="networking-recommendations"></a>네트워킹 권장 사항

몇 가지 주요 구성 요소를 사용하여 온-프레미스 환경을 Azure에 연결할 수 있습니다.

* **Azure VPN Gateway**: VPN Gateway는 퍼블릭 인터넷을 통해 Azure 가상 네트워크와 온-프레미스 위치 간의 암호화된 트래픽을 전송하는 데 사용되는 특정 유형의 가상 네트워크 게이트웨이입니다. Azure Virtual Network 게이트웨이와 로컬 가상 네트워크 게이트웨이를 모두 사용합니다. 구성 방법에 대한 자세한 내용은 [VPN Gateway란?](/azure/vpn-gateway/vpn-gateway-about-vpngateways)을 참조하세요.
* **Azure ExpressRoute**: ExpressRoute 연결은 퍼블릭 인터넷을 사용하지 않으며 인터넷을 통한 일반 연결보다 보안성과 안정성이 뛰어나며 대기 시간이 짧아 속도가 빠릅니다. 선택한 연결 옵션은 SKU에 따라 솔루션의 대기 시간, 성능, SLA 수준에 영향을 줍니다. 자세한 내용은 [ExpressRoute 가상 네트워크 게이트웨이 정보](/azure/expressroute/expressroute-about-virtual-network-gateways)를 참조하세요.

대부분의 고객은 점프 상자 또는 [Azure Bastion](/azure/bastion/bastion-overview)을 사용하여 다른 Azure 인프라에 액세스합니다. **Azure Private Link** 를 사용하면 가상 네트워크의 프라이빗 엔드포인트를 통해 이 시나리오의 AKS를 비롯한 Azure PaaS 서비스뿐 아니라 다른 Azure 호스팅 서비스에 안전하게 액세스할 수 있습니다. 가상 네트워크와 서비스 간의 트래픽은 Microsoft 백본 네트워크를 통해 트래버스하여 퍼블릭 인터넷에 노출되지 않도록 합니다. 또한 가상 네트워크에서 고유한 프라이빗 링크 서비스를 만들어 고객에게 비공개로 제공할 수도 있습니다.

### <a name="active-directory-and-azure-recommendation"></a>Active Directory 및 Azure 권장 사항

온-프레미스 AD DS는 사용자 계정에 대한 정보를 저장하고, 동일한 네트워크에 있는 다른 권한 있는 사용자가 보안 경계에 포함된 사용자, 컴퓨터, 애플리케이션 또는 기타 리소스와 연결된 ID를 인증하여 이 정보에 액세스할 수 있도록 합니다. 대부분의 하이브리드 시나리오에서 사용자 인증은 온-프레미스 AD DS 환경에 연결된 VPN Gateway 또는 ExpressRoute를 통해 실행됩니다.  

AD 모드에서 BDC를 배포하는 경우 [온-프레미스 Active Directory를 Azure와 통합](/azure/architecture/reference-architectures/identity/)하는 솔루션에는 다음 필수 구성 요소가 있어야 합니다.

* 온-프레미스 Active Directory에서 제공된 OU(조직 구성 단위) 내에 사용자, 그룹, 머신 계정을 만들 수 있는 [특정 권한이 AD 계정에 있습니다](active-directory-prerequisites.md).
* [내부 DNS를 확인하는](active-directory-dns-reconciliation.md) DNS 서버. 이 도메인에서 이름을 사용하여 **A(정방향 조회)** 및 **PTR(역방향 조회) 레코드** 를 모두 DNS 서버에 포함해야 합니다. BDC 배포 프로필에서 도메인 DNS 설정을 지정합니다.  

## <a name="next-steps"></a>다음 단계

[자습서: AKS(Azure Kubernetes Services)의 AD 모드에서 SQL Server 빅 데이터 클러스터 배포](active-directory-deployment-aks-tutorial.md)
