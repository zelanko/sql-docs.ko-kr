---
title: AKS(Azure Kubernetes Service) 프라이빗 클러스터에 BDC 배포
titleSuffix: SQL Server Big Data Cluster
description: CNI(고급 네트워킹)를 사용하여 AKS(Azure Kubernetes Service) 프라이빗 클러스터로 SQL Server 빅 데이터 클러스터를 배포하는 방법을 알아봅니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4a55d7f6c9c55891f8d1a7bf97d8834c9df4a796
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283122"
---
# <a name="deploy-bdc-in-azure-kubernetes-service-aks-private-cluster"></a>AKS(Azure Kubernetes Service) 프라이빗 클러스터에 BDC 배포

이 문서에서는 AKS(Azure Kubernetes Service) 프라이빗 클러스터에 SQL Server 빅 데이터 클러스터를 배포하는 방법을 설명합니다. 이 구성은 엔터프라이즈 네트워킹 환경에서 공용 IP 주소의 제한적 사용을 지원합니다.

비공개 배포는 다음과 같은 이점을 제공합니다.

* 공용 IP 주소의 제한적 사용
* 애플리케이션 서버와 클러스터 노드 풀 간의 네트워크 트래픽이 프라이빗 네트워크에만 유지됨
* 특정 요구 사항에 맞게 필수 송신 트래픽을 사용자 지정 구성

이 문서에서는 AKS 프라이빗 클러스터를 사용하여 각 보안 문자열이 적용되는 동안 공용 IP 주소의 사용을 제한하는 방법을 보여 줍니다.

## <a name="deploy-private-bdc-cluster-with-aks-private-cluster"></a>AKS 프라이빗 클러스터를 사용하여 프라이빗 BDC 클러스터 배포

시작하려면 API 서버와 노드 풀 간의 네트워크 트래픽이 개인 네트워크에만 유지되도록 [AKS 프라이빗 클러스터](/azure/aks/private-clusters)를 만듭니다. AKS 프라이빗 클러스터에는 컨트롤 플레인 또는 API 서버에 내부 IP 주소가 있습니다.

이 섹션에서는 CNI(고급 네트워킹)를 사용하여 AKS(Azure Kubernetes Service) 프라이빗 클러스터에 BDC 클러스터를 배포하는 방법을 보여 줍니다.

## <a name="create-a-private-aks-cluster-with-advanced-networking"></a>고급 네트워킹을 사용하여 AKS 프라이빗 클러스터 만들기

```console

export REGION_NAME=<your Azure region >
export RESOURCE_GROUP=< your resource group name >
export SUBNET_NAME=aks-subnet
export VNET_NAME=bdc-vnet
export AKS_NAME=< your aks private cluster name >
 
az group create -n $RESOURCE_GROUP -l $REGION_NAME
 
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
 
echo $SUBNET_ID
## will be displayed something similar as the following: 
/subscriptions/xxxx-xxxx-xxx-xxxx-xxxxxxxx/resourceGroups/your-bdc-rg/providers/Microsoft.Network/virtualNetworks/your-aks-vnet/subnets/your-aks-subnet
```

### <a name="create-aks-private-cluster-with-advanced-networking-cni"></a>CNI(고급 네트워킹)를 사용하여 AKS 프라이빗 클러스터 만들기

다음 단계로 이동하려면 프라이빗 클러스터 기능이 사용하도록 설정된 표준 Load Balancer를 사용하여 AKS 클러스터를 프로비전해야 합니다. 명령은 다음과 같습니다. 

```console
az aks create \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.2.0.10 \
    --service-cidr 10.2.0.0/24 \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

배포에 성공하면 `<MC_yourakscluster>` 리소스 그룹으로 이동하여 `kube-apiserver`가 프라이빗 엔드포인트인지 확인할 수 있습니다. 예제는 다음 섹션을 참조하세요.

## <a name="connect-to-an-aks-cluster"></a>AKS 클러스터에 연결

```console
az aks get-credentials -n $AKS_NAME -g $RESOURCE_GROUP
```

## <a name="build-big-data-cluster-bdc-deployment-profile"></a>BDC(빅 데이터 클러스터) 배포 프로필 빌드

AKS 클러스터에 연결한 후에는 BDC 배포를 시작할 수 있으며, 환경 변수를 준비하고 배포를 시작할 수 있습니다. 

```console
azdata bdc config init --source aks-dev-test --target private-bdc-aks --force
```

BDC 사용자 지정 배포 프로필 생성 및 구성

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

## <a name="deploy-private-sql-server-big-data-cluster-with-ha"></a>HA를 사용하여 프라이빗 SQL Server 빅 데이터 클러스터 배포

[HA(고가용성)를 사용하여 SQL-BDC(SQL Server 빅 데이터 클러스터)를 배포](deployment-high-availability.md)하는 경우 `aks-dev-test-ha` 배포 프로필을 사용하여 배포합니다. 성공적으로 배포되면 동일한 `kubectl get svc` 명령을 사용하여 추가 `master-secondary-svc` 서비스가 생성되는 것을 볼 수 있습니다. `ServiceType`을 `NodePort`로 구성해야 합니다. 다른 단계는 이전 섹션에서 설명한 것과 비슷합니다.

다음 예제에서는 `ServiceType`을 `NodePort`로 설정합니다.

```console
azdata bdc config replace -c private-bdc-aks /bdc.json -j "$.spec.resources.master.spec.endpoints[1].serviceType=NodePort"
```

## <a name="deploy-bdc-in-aks-private-cluster"></a>AKS 프라이빗 클러스터에 BDC 배포

```console
export AZDATA_USERNAME=<your bdcadmin username>
export AZDATA_PASSWORD=< your bdcadmin password>

azdata bdc create --config-profile private-bdc-aks --accept-eula yes
```

## <a name="check-deployment-status"></a>배포 상태 확인

배포는 몇 분 정도 걸리며, 다음 명령을 사용하여 배포 상태를 확인할 수 있습니다. 

```console
kubectl get pods -n mssql-cluster -w
```

## <a name="check-the-service-status"></a>서비스 상태 확인

다음 명령을 사용하여 서비스를 확인합니다. 외부 IP 없이 모두 정상 상태인지 확인합니다.

```console
kubectl get services -n mssql-cluster
```

[AKS 프라이빗 클러스터에서 BDC를 관리](private-manage.md)하는 방법을 확인합니다. 다음 단계는 [BDC 클러스터 연결](connect-to-big-data-cluster.md)입니다.

[GitHub의 SQL Server 샘플 리포지토리](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/private-aks)에서 이 시나리오에 대한 자동화 스크립트를 참조하세요.

## <a name="next-steps"></a>다음 단계

[프라이빗 클러스터 관리](private-manage.md)

[프라이빗 BDC 클러스터의 송신 트래픽 제한](private-restrict-egress-traffic.md)

[Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)
