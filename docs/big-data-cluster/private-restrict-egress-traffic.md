---
title: AKS(Azure Kubernetes Service) 프라이빗 클러스터에서 BDC(빅 데이터 클러스터) 클러스터의 송신 트래픽 제한
titleSuffix: SQL Server Big Data Clusters
description: AKS(Azure Kubernetes Service) 프라이빗 클러스터에서 BDC(빅 데이터 클러스터) 클러스터의 송신 트래픽을 제한하는 방법을 알아봅니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 962e155b3b0b5906d36fa4d884be2af353cb25a9
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076602"
---
# <a name="restrict-egress-traffic-of-big-data-clusters-bdc-clusters-in-azure-kubernetes-service-aks-private-cluster"></a>AKS(Azure Kubernetes Service) 프라이빗 클러스터에서 BDC(빅 데이터 클러스터) 클러스터의 송신 트래픽 제한

AKS는 기본적으로 송신을 위해 설정 및 사용할 표준 SKU 부하 분산 장치를 프로비전합니다. 그러나 공용 IP가 허용되지 않거나 송신에 대한 추가 홉이 필요한 경우에는 기본 설정이 모든 시나리오의 요구 사항을 충족하지 못할 수 있습니다. 클러스터가 공용 IP를 허용하지 않고 NVA(네트워크 가상 어플라이언스) 뒤에 있는 경우 사용자 정의 라우팅 테이블을 정의합니다.

기본적으로 AKS 클러스터는 관리 및 운영 목적을 위해 아웃바운드(송신) 인터넷 액세스가 제한되지 않습니다. AKS 클러스터의 작업자 노드는 예를 들어 다음과 같은 경우 특정 포트 및 FQDN(정규화된 도메인 이름)에 액세스해야 합니다.

* 작업자 노드 OS 보안 업데이트의 경우, 클러스터가 MCR(Microsoft Container Registry)에서 기본 시스템 컨테이너 이미지를 가져와야 합니다.
* GPU 사용 AKS 작업자 노드가 드라이버를 설치하기 위해 Nvidia의 일부 엔드포인트에 액세스해야 하는 경우
* 고객이 엔터프라이즈급 규정 준수를 위한 Azure 정책, Azure 모니터링(컨테이너 인사이트 사용)과 같은 Azure 서비스와 연동하여 AKS를 사용하는 시나리오 
* 개발 공간 사용 및 기타 유사한 특성의 시나리오

> [!NOTE]
> 현재, AKS(Azure Kubernetes Service) 프라이빗 클러스터에 BDC를 배포할 때 시나리오에 인바운드 종속성은 없으며, 이 문서에서 설명한 것 외에도 [AKS(Azure Kubernetes Service)에서 클러스터 노드의 송신 트래픽 제어](/azure/aks/limit-egress-traffic)에서 모든 아웃바운드 종속성을 확인할 수 있습니다.

이 문서에서는 고급 네트워킹 및 UDR(사용자 정의 라우팅)을 사용하여 AKS 프라이빗 클러스터에 BDC를 배포하는 방법 및 엔터프라이즈급 네트워킹 환경과의 추가 통합에 대해 설명합니다.

## <a name="use-azure-firewall-to-restrict-egress-traffic"></a>Azure Firewall을 사용하여 송신 트래픽 제한

Azure Firewall은 이 구성을 단순화하기 위해 Azure Kubernetes Service `(AzureKubernetesService)` FQDN 태그를 제공합니다.

이 태그에 대한 자세한 내용은 [을 사용하여 송신 트래픽 제한](/azure/aks/limit-egress-traffic#restrict-egress-traffic-using-azure-firewall)을 참조하세요.

다음 이미지에서는 AKS 프라이빗 클러스터에서 트래픽을 제한하는 방법을 보여 줍니다. 

:::image type="content" source="media/private-cluster-restrict-egress-traffic/aks-azure-firewall-egress.png" alt-text="AKS 프라이빗 클러스터 방화벽 송신 트래픽":::

Azure Firewall을 사용하여 기본 아키텍처를 설정하려면 다음을 수행합니다.

1. 리소스 그룹 및 VNet 만들기
2. Azure Firewall 만들기 및 설정
3. 사용자 정의 라우팅 테이블 만들기
4. 방화벽 규칙 설정
5. SP(서비스 주체) 만들기
6. AKS 프라이빗 클러스터 만들기
7. BDC 배포 프로필 만들기
8. BDC 배포

다음 단계에서는 세부 정보를 제공합니다.

## <a name="create-the-resource-group-and-vnet"></a>리소스 그룹 및 VNet 만들기

1. 리소스를 만들기 위한 환경 변수 집합을 정의합니다.

   ```console
   export REGION_NAME=<region>
   export RESOURCE_GROUP=private-bdc-aksudr-rg
   export SUBNET_NAME=aks-subnet
   export VNET_NAME=bdc-vnet
   export AKS_NAME=bdcaksprivatecluster
   ```

1. 리소스 그룹 만들기

   ```azurecli
   az group create -n $RESOURCE_GROUP -l $REGION_NAME
   ```

1. VNet을 만듭니다.

   ```azurecli
   az network vnet create \
     --resource-group $RESOURCE_GROUP \
     --location $REGION_NAME \
     --name $VNET_NAME \
     --address-prefixes 10.0.0.0/8 \
     --subnet-name $SUBNET_NAME \
     --subnet-prefix 10.1.0.0/16

   SUBNET_ID=$(az network vnet subnet show \
     --resource-group $RESOURCE_GROUP \
     --vnet-name $VNET_NAME \
     --name $SUBNET_NAME \
     --query id -o tsv)
   ```

## <a name="create-and-set-up-azure-firewall"></a>Azure Firewall 만들기 및 설정

1. 리소스를 만들기 위한 환경 변수 집합을 정의합니다.

   ```console
   export FWNAME=bdcaksazfw
   export FWPUBIP=$FWNAME-ip
   export FWIPCONFIG_NAME=$FWNAME-config

   az extension add --name azure-firewall
   ```

1. 방화벽 전용 서브넷을 만듭니다.

   > [!NOTE]
   > 방화벽을 만든 후에는 이름을 변경할 수 없습니다.

   ```azurecli
   az network vnet subnet create \
     --resource-group $RESOURCE_GROUP \
     --vnet-name $VNET_NAME \
     --name AzureFirewallSubnet \
     --address-prefix 10.3.0.0/24

    az network firewall create -g $RESOURCE_GROUP -n $FWNAME -l $REGION_NAME --enable-dns-proxy true

    az network public-ip create -g $RESOURCE_GROUP -n $FWPUBIP -l $REGION_NAME --sku "Standard"

    az network firewall ip-config create -g $RESOURCE_GROUP -f $FWNAME -n $FWIPCONFIG_NAME --public-ip-address $FWPUBIP --vnet-name $VNET_NAME
   ```

기본적으로 Azure는 Azure 서브넷, 가상 네트워크 및 온-프레미스 네트워크 간에 트래픽을 자동으로 라우팅합니다. 

## <a name="create-user-defined-route-table"></a>사용자 정의 라우팅 테이블 만들기

Azure Firewall에 대한 홉을 사용하여 UDR(사용자 정의 라우팅) 테이블을 만듭니다.

```azurecli

export SUBID= <your Azure subscription ID>
export FWROUTE_TABLE_NAME=bdcaks-rt
export FWROUTE_NAME=bdcaksroute
export FWROUTE_NAME_INTERNET=bdcaksrouteinet

export FWPUBLIC_IP=$(az network public-ip show -g $RESOURCE_GROUP -n $FWPUBIP --query "ipAddress" -o tsv)
export FWPRIVATE_IP=$(az network firewall show -g $RESOURCE_GROUP -n $FWNAME --query "ipConfigurations[0].privateIpAddress" -o tsv)

# Create UDR and add a route for Azure Firewall

az network route-table create -g $RESOURCE_GROUP --name $FWROUTE_TABLE_NAME

az network route-table route create -g $RESOURCE_GROUP --name $FWROUTE_NAME --route-table-name $FWROUTE_TABLE_NAME --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address $FWPRIVATE_IP --subscription $SUBID

az network route-table route create -g $RESOURCE_GROUP --name $FWROUTE_NAME_INTERNET --route-table-name $FWROUTE_TABLE_NAME --address-prefix $FWPUBLIC_IP/32 --next-hop-type Internet
```

## <a name="set-up-firewall-rules"></a>방화벽 규칙 설정 

```azurecli
# Add FW Network Rules

az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'apiudp' --protocols 'UDP' --source-addresses '*' --destination-addresses "AzureCloud.$REGION_NAME" --destination-ports 1194 --action allow --priority 100
az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'apitcp' --protocols 'TCP' --source-addresses '*' --destination-addresses "AzureCloud.$REGION_NAME" --destination-ports 9000
az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'time' --protocols 'UDP' --source-addresses '*' --destination-fqdns 'ntp.ubuntu.com' --destination-ports 123

# Add FW Application Rules

az network firewall application-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwar' -n 'fqdn' --source-addresses '*' --protocols 'http=80' 'https=443' --fqdn-tags "AzureKubernetesService" --action allow --priority 100
```

다음 명령을 사용하여 이전에 BDC를 배포한 AKS 클러스터에 UDR(사용자 정의 라우팅 테이블)을 연결할 수 있습니다.

```azurecli
az network vnet subnet update -g $RESOURCE_GROUP --vnet-name $VNET_NAME --name $SUBNET_NAME --route-table $FWROUTE_TABLE_NAME
```

## <a name="create--configure-service-principal-sp"></a>SP(서비스 주체) 만들기 및 구성

이 단계에서는 서비스 주체를 만들고 가상 네트워크에 사용 권한을 할당해야 합니다.

다음 예제를 참조하십시오. 

```azurecli
# Create SP and Assign Permission to Virtual Network

az ad sp create-for-rbac -n "bdcaks-sp" --skip-assignment

APPID=<your service principal ID >
PASSWORD=< your service principal password >
VNETID=$(az network vnet show -g $RESOURCE_GROUP --name $VNET_NAME --query id -o tsv)

# Assign SP Permission to VNET

az role assignment create --assignee $APPID --scope $VNETID --role "Network Contributor"


RTID=$(az network route-table show -g $RESOURCE_GROUP -n $FWROUTE_TABLE_NAME --query id -o tsv)
az role assignment create --assignee $APPID --scope $RTID --role "Network Contributor"
```

## <a name="create-aks-cluster"></a>AKS 클러스터 만들기

그런 다음 아웃바운드 형식으로 `userDefinedRouting`을 사용하여 AKS 클러스터를 만듭니다.

```azurecli
az aks create \
    --resource-group $RESOURCE_GROUP \
    --location $REGION_NAME \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --outbound-type userDefinedRouting \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.2.0.10 \
    --service-cidr 10.2.0.0/24 \
    --service-principal $APPID \
    --client-secret $PASSWORD \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

## <a name="build-big-data-cluster-bdc-deployment-profile"></a>BDC(빅 데이터 클러스터) 배포 프로필 빌드

사용자 지정 프로필을 사용하여 BDC 클러스터를 만들 수 있습니다. 

```console
azdata bdc config init --source aks-dev-test --target private-bdc-aks --force
```

## <a name="generate-and-config-bdc-custom-deployment-profile"></a>BDC 사용자 지정 배포 프로필 생성 및 구성 
```console
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.docker.imageTag=2019-CU6-ubuntu-16.04"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.storage.data.className=default"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.storage.logs.className=default"

azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.endpoints[1].serviceType=NodePort"

azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].serviceType=NodePort"
```

## <a name="deploy-bdc-in-aks-private-cluster"></a>AKS 프라이빗 클러스터에 BDC 배포

```console
export AZDATA_USERNAME=<your bdcadmin username>
export AZDATA_PASSWORD=< your bdcadmin password>

azdata bdc create --config-profile private-bdc-aks --accept-eula yes
```

## <a name="use-third-party-firewall-instead-of-azure-firewall"></a>Azure Firewall 대신 타사 방화벽 사용

타사 방화벽을 사용하여 AKS 프라이빗 클러스터로 BDC를 배포할 때 송신 트래픽을 제한합니다. 예를 들어 [Azure Marketplace 방화벽](https://azuremarketplace.microsoft.com/marketplace/apps?search=firewall&page=1)을 참조하세요. 타사 방화벽은 규정 준수를 강화한 구성의 비공개 배포 솔루션에서 사용할 수 있습니다. 방화벽은 다음 네트워크 규칙을 제공해야 합니다.

* 모든 [필수 아웃바운드 네트워크 규칙 및 AKS 클러스터용 FQDN](/azure/aks/limit-egress-traffic#required-outbound-network-rules-and-fqdns-for-aks-clusters) 및 모든 와일드카드 HTTP/HTTPS 엔드포인트 및 종속성(다수의 자격 조건 및 실제 요구 사항에 따라 AKS 클러스터마다 달라질 수 있음).
* [여기](/azure/aks/limit-egress-traffic#azure-global-required-network-rules)에 언급된 Azure Global 필수 네트워크 규칙/FQDN/애플리케이션 규칙.
* [여기](/azure/aks/limit-egress-traffic#optional-recommended-fqdn--application-rules-for-aks-clusters)에 언급된 AKS 클러스터용 권장 FQDN/애플리케이션 규칙(선택 사항). 

[AKS 프라이빗 클러스터에서 BDC를 관리](private-manage.md)하는 방법을 확인하세요. 다음 단계는 [BDC 클러스터 연결](connect-to-big-data-cluster.md)입니다.

[GitHub의 SQL Server 샘플 리포지토리](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/private-aks)에서 이 시나리오에 대한 자동화 스크립트를 참조하세요.

## <a name="next-steps"></a>다음 단계

[AKS 프라이빗 클러스터에서 빅 데이터 클러스터 관리](private-manage.md)

[Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)
