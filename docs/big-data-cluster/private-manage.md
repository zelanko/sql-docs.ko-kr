---
title: AKS(Azure Kubernetes Service) 프라이빗 클러스터에서 BDC(빅 데이터 클러스터) 관리
titleSuffix: SQL Server Big Data Cluster
description: AKS(Azure Kubernetes Service) 프라이빗 클러스터에서 SQL Server 빅 데이터 클러스터를 관리하는 방법을 알아봅니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 442f5def7e1378b750460cfc6860e780b1dcfd80
ms.sourcegitcommit: fe5dedb2a43516450696b754e6fafac9f5fdf3cf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2020
ms.locfileid: "89202231"
---
# <a name="manage-big-data-cluster-in-aks-private-cluster"></a>AKS 프라이빗 클러스터에서 빅 데이터 클러스터 관리

이 문서에서는 Azure에 배포된 SQL Server BDC(빅 데이터 클러스터)를 사용하여 AKS(Azure Kubernetes Service) 프라이빗 클러스터를 관리하는 방법을 설명합니다.

[프라이빗 클러스터 만들기](/azure/aks/private-clusters/)에 설명된 대로 AKS 프라이빗 클러스터 API 서버 엔드포인트에는 공용 IP 주소가 없습니다. API 서버를 관리하려면 AKS 클러스터의 Azure VNet(Virtual Network)에 대한 액세스 권한이 있는 VM을 사용합니다.

## <a name="azure-vm---same-vnet"></a>Azure VM - 동일한 VNet

가장 간단한 방법은 AKS 클러스터와 동일한 VNet에서 Azure VM을 배포하는 것입니다.

1. AKS 클러스터를 사용하여 동일한 VNET에 Azure VM을 배포합니다. 이를 *jumpbox*라고도 합니다.
1. 해당 VM에 연결하고 [SQL Server 2019 빅 데이터 도구를 설치](deployment-guidance.md#install-sql-server-2019-big-data-tools)합니다.

보안을 위해, API 서버 권한 있는 IP 범위에 AKS 기능을 사용하여 AKS 컨트롤 플레인에 위치하는 API 서버에 대한 액세스를 제한할 수 있습니다. 제한된 액세스를 통해 특정 IP 주소(예: jumpbox VM, 관리 VM, 개발자 그룹 IP 주소 범위) 및 방화벽 공용 프런트 엔드 IP 주소를 사용할 수 있습니다.

## <a name="other-options"></a>기타 옵션

Jumpbox 사용에 대한 대안은 다음과 같습니다.

* VM을 별도의 네트워크에서 사용하고 VNet에 대한 [가상 네트워크 피어링](/azure/virtual-network/virtual-network-peering-overview)을 설정합니다.

* [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 또는 [VPN Gateway](/azure/vpn-gateway/vpn-gateway-about-vpngateways) 연결합니다.

   [프라이빗 클러스터에 연결하기 위한 옵션](/azure/aks/private-clusters#options-for-connecting-to-the-private-cluster)에서 위의 각 방법에 대해 설명합니다.

* 서비스가 [Azure 표준 부하 분산 장치](/azure/aks/load-balancer-standard) 뒤에서 실행되는 경우 [Azure Private Link](/azure/private-link/private-link-service-overview#limitations)를 사용하도록 설정할 수 있습니다. Azure Private Link에서는 다른 Azure VNet에서 프라이빗 액세스를 사용할 수 있습니다.

* 하이브리드 시나리오에서는 [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 또는 [VPN Gateway](/azure/vpn-gateway/vpn-gateway-about-vpngateways) 연결을 설정할 수도 있습니다.

## <a name="next-steps"></a>다음 단계

[Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)