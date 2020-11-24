---
title: AKS(Azure Kubernetes Services)의 Active Directory에서 배포 - 자습서
titleSuffix: SQL Server Big Data Cluster
description: AKS(Azure Kubernetes Services)의 AD 모드에서 SQL Server 빅 데이터 클러스터를 배포하는 방법을 알아봅니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 11/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b24a83e1647b0e32aff3ce19ad69a0fdc9405b0e
ms.sourcegitcommit: 0f484f32709a414f05562bbaafeca9a9fc57c9ed
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632956"
---
# <a name="tutorial-deploy-sql-server-big-data-clusters-in-ad-mode-on-azure-kubernetes-services-aks"></a>자습서: AKS(Azure Kubernetes Services)의 AD 모드에서 SQL Server 빅 데이터 클러스터 배포

이 문서에서는 참조 아키텍처를 사용하여 Active Directory 인증 모드에서 SQL Server BDC(빅 데이터 클러스터)를 배포하는 방법을 설명합니다. 참조 아키텍처는 온-프레미스 AD DS(Active Directory Domain Services)를 Azure로 확장합니다. [Azure 구성 요소](https://github.com/mspnp/template-building-blocks/wiki/Install-Azure-Building-Blocks)를 사용하여 [Azure 아키텍처 센터](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-extend-domain)에서 배포할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

SQL Server 빅 데이터 클러스터를 배포하려면 먼저 다음을 수행해야 합니다.

* 관리를 위한 Azure VM에 액세스합니다. 이 VM은 BDC를 배포할 Azure Virtual Network(VNet)에 대한 액세스 권한이 필요합니다. VM은 동일한 VNet에 있거나 [피어링된 VNet](/azure/virtual-network/virtual-network-manage-peering)에 있어야 합니다.
* 관리 VM에 [빅 데이터 도구를 설치](deploy-big-data-tools.md)합니다.
* 온-프레미스 AD 컨트롤러의 [Active Directory 인증 모드](active-directory-prerequisites.md)에서 클러스터 배포를 준비합니다.

## <a name="create-aks-subnet"></a>AKS 서브넷 만들기

1. 환경 변수 설정

   ```console
   export REGION_NAME=< your Azure Region >
   export RESOURCE_GROUP=<your resource group >
   export SUBNET_NAME=aks-subnet
   export VNet_NAME= adds-vnet
   export AKS_NAME= <your aks cluster name>
   ```

1. AKS 서브넷 만들기

   ```console
   SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNet_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
   ```

다음 스크린샷은 서브넷이 아키텍처의 VNet에 있도록 계획하는 방법을 보여 줍니다.

:::image type="content" source="media/active-directory-deployment-aks/ad-in-aks-diagram.png" alt-text="AD 및 SQL Server 빅 데이터 클러스터를 사용하는 AKS 클러스터":::

## <a name="create-an-aks-private-cluster"></a>AKS 프라이빗 클러스터 만들기

다음 명령을 사용하여 AKS 프라이빗 클러스터를 배포할 수 있습니다. 프라이빗 클러스터가 필요하지 않으면 명령에서 `--enable-private-cluster` 매개 변수를 제거합니다. 다른 요구 사항에 대한 자세한 내용은 [how to deploy an Azure Kubernetes Cluster (AKS)](/azure/aks/tutorial-kubernetes-deploy-cluster)(AKS(Azure Kubernetes Cluster)를 배포하는 방법)를 참조하세요.

```azurecli
az aks create \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.3.0.10 \
    --service-cidr 10.3.0.0/24 \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

AKS 클러스터를 배포한 후 [AKS 클러스터에 연결](/azure/aks/tutorial-kubernetes-deploy-cluster#connect-to-cluster-using-kubectl)합니다.

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>도메인 컨트롤러에 대한 역방향 DNS 항목 확인

AKS 클러스터의 AD 모드에서 BDC 배포를 시작하려면 먼저 도메인 컨트롤러 자체에서 **A 레코드** 와 **PTR 레코드**(역방향 DNS 항목)가 DNS 서버에 등록되어 있는지 확인합니다.

이 설정을 확인하려면 `nslookup` 명령을 실행하거나 [PowerShell 스크립트](troubleshoot-ad-reverse-lookup-zone.md)를 실행하여 역방향 DNS 항목(PTR 레코드)이 구성되어 있는지 확인합니다.

## <a name="create-bdc-deployment-profile"></a>BDC 배포 프로필 만들기

다음 명령은 배포 프로필을 만듭니다.

```console
azdata bdc config init --source kubeadm-prod  --target bdc-ad-aks
```

다음 명령은 배포 프로필에 대한 매개 변수를 설정하는 데 사용됩니다.

### <a name="controljson"></a>control.json

```console
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.storage.data.className=default"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.storage.logs.className=default"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[1].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[0].dnsName=controller.contoso.com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[1].dnsName=proxys.contoso.com"

# security settings 
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"192.168.0.4\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"ad1.contoso.com\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.domainDnsName=contoso.com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
```

### <a name="bdcjson"></a>bdc.json

```console
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=master.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=mastersec.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[1].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=gateway.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=approxy.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].serviceType=NodePort"
```

## <a name="initiate-deployment"></a>배포 시작

다음 명령은 BDC 배포를 시작합니다.

```console
azdata bdc create --config-profile bdc-ad-aks --accept-eula yes
```

## <a name="next-steps"></a>다음 단계

[Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)

[자습서: SQL Server 빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)