---
title: 시작하기
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 빅 데이터 클러스터를 배포하기 위한 단계와 리소스를 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4caaacd2d71d00d874a793129eef2f4144f03190
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784300"
---
# <a name="get-started-with-big-data-clusters-2019-deployment"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포 시작

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법을 설명합니다. 이 문서에서는 배포 시나리오를 이해하는 데 도움이 되는 개념과 프레임워크를 안내합니다. 특정 배포 단계는 클라이언트 및 서버에 대해 선택한 플랫폼에 따라 다릅니다. [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 소개는 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)를 참조하세요.

기타 SQL Server 배포 시나리오는 다음을 참조하세요.

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Docker 컨테이너](../linux/sql-server-linux-configure-docker.md)

## <a name="quick-introduction"></a>간략한 소개 

빅 데이터 클러스터를 배포하는 방법에 대한 개요는 9분 분량의 다음 동영상을 시청하세요.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Big-Data-Clusters-deployment-overview/player?WT.mc_id=dataexposed-c9-niner]


> [!TIP]
> Kubernetes 및 빅 데이터 클러스터가 배포된 환경을 신속하게 구축하여 기능을 강화하려면 [스크립트 섹션](#scripts) 에서 가리키는 샘플 스크립트 중 하나를 사용합니다. 배포 후 클러스터를 관리하려면 다음 섹션의 [클라이언트 도구](#tools)를 사용합니다.


## <a name="client-tools"></a><a id="tools"></a> 클라이언트 도구

빅 데이터 클러스터를 사용하려면 특정 클라이언트 도구 세트가 필요합니다. Kubernetes에 빅 데이터 클러스터를 배포하기 전에 배포에 필요한 도구를 설치해야 합니다. 시나리오에 따라 특정 도구가 필요합니다. 각 문서에서 특정 작업을 수행하는 데 필요한 도구를 설명해야 합니다. 전체 도구 목록과 설치 링크는 [SQL Server 2019 빅 데이터 도구 설치](deploy-big-data-tools.md)를 참조하세요.

## <a name="kubernetes"></a>Kubernetes

빅 데이터 클러스터는 [Kubernetes](https://kubernetes.io/docs/home)에서 관리되는 일련의 상호 관련된 컨테이너로 배포됩니다. 다양한 방법으로 Kubernetes를 호스트할 수 있습니다. 기존 Kubernetes 환경이 이미 있더라도 빅 데이터 클러스터와 관련된 요구 사항을 검토해야 합니다.

- **AKS(Azure Kubernetes Service)** : AKS를 사용하여 관리되는 Kubernetes 클러스터를 Azure에 배포할 수 있습니다. 에이전트 노드만 관리하고 유지하면 됩니다. AKS를 사용하면 클러스터에 사용할 고유한 하드웨어를 프로비저닝할 필요가 없습니다. 또한 간편하게 [python 스크립트](quickstart-big-data-cluster-deploy.md) 또는 [배포 Notebook](notebooks-deploy.md)을 사용하여 한 단계로 AKS 클러스터를 만들고 빅 데이터 클러스터를 배포할 수 있습니다. 빅 데이터 클러스터 배포를 위한 AKS를 구성하는 방법에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]배포를 위한 Azure Kubernetes Service 구성](deploy-on-aks.md)을 참조하세요.

- **ARO(Azure Red Hat OpenShift)** : ARO를 사용하면 Azure에 관리형 Red Hat OpenShift 클러스터를 배포할 수 있습니다. 에이전트 노드만 관리하고 유지하면 됩니다. ARO를 사용하면 클러스터에 사용할 고유한 하드웨어를 프로비저닝할 필요가 없습니다. 또한 간편하게 [python 스크립트](quickstart-big-data-cluster-deploy-aro.md)를 사용하여 한 단계로 ARO 클러스터를 만들고 빅 데이터 클러스터를 배포할 수 있습니다. 이 배포 모델은 SQL Server 2019 CU5에 도입되었습니다. 

- **여러 머신**: 물리적 서버 또는 가상 머신일 수 있는 여러 Linux 머신에 Kubernetes를 배포할 수도 있습니다. [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) 도구를 사용하여 Kubernetes 클러스터를 만들 수 있습니다. [bash 스크립트](deployment-script-single-node-kubeadm.md)를 사용하여 이러한 유형의 배포를 자동화할 수 있습니다. 이 방법은 빅 데이터 클러스터에 사용하려는 기존 인프라가 이미 있는 경우에 적합합니다. 빅 데이터 클러스터에서 **kubeadm** 배포를 사용하는 방법에 대한 자세한 내용은 [여러 머신에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 배포를 위한 Kubernetes 구성](deploy-with-kubeadm.md)을 참조하세요.

- **Red Hat OpenShift**: 고유의 Red Hat OpenShift 클러스터에 배포합니다. 자세한 내용은 OpenShift 온-프레미스 및 Azure Red Hat OpenShift에 SQL Server 빅 데이터 클러스터 [ 배포[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deploy-openshift.md)를 참조하세요. 이 배포 모델은 SQL Server 2019 CU5에 도입되었습니다.

## <a name="deploy-a-big-data-cluster"></a>빅 데이터 클러스터 배포

Kubernetes를 구성한 후에 <`azdata bdc create` 명령을 사용하여 빅 데이터 클러스터를 배포합니다. 배포할 때 여러 가지 방법을 사용할 수 있습니다.

- 개발-테스트 환경에 배포하는 경우에는 **azdata**에서 제공하는 [기본 구성](deployment-guidance.md#deploy) 중 하나를 사용할 수 있습니다.

- 배포를 사용자 지정하려면 고유한 [배포 구성 파일](deployment-guidance.md#configfile)을 만들고 사용할 수 있습니다.

- 완전 무인 설치를 위해 환경 변수에 다른 모든 설정을 전달할 수 있습니다. 자세한 내용은 [무인 배포](deployment-guidance.md#unattended)를 참조하세요.


## <a name="deployment-scripts"></a><a id="scripts"></a> 배포 스크립트

배포 스크립트를 사용하면 한 단계로 Kubernetes 및 빅 데이터 클러스터를 배포할 수 있습니다. 또한 배포 스크립트는 빅 데이터 클러스터 설정의 기본값을 제공하는 경우가 많습니다. 빅 데이터 클러스터 배포를 다르게 구성하는 고유한 버전을 만들어 배포 스크립트를 사용자 지정할 수 있습니다.

현재 사용할 수 있는 배포 스크립트는 다음과 같습니다.

- [Python 스크립트 - AKS(Azure Kubernetes Service)에 빅 데이터 클러스터 배포](quickstart-big-data-cluster-deploy.md)
- [Bash 스크립트 - 단일 노드 kubeadm 클러스터에 빅 데이터 클러스터 배포](deployment-script-single-node-kubeadm.md)

## <a name="deployment-notebooks"></a>배포 Notebook

Azure Data Studio Notebook을 실행하여 빅 데이터 클러스터를 배포할 수도 있습니다. Notebook을 사용하여 AKS에 배포하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

- [Azure Data Studio Notebook을 사용하여 빅 데이터 클러스터 배포](notebooks-deploy.md)

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터를 성공적으로 배포한 후에는 [클러스터에 연결](connect-to-big-data-cluster.md)하고 여러 연습에서 사용할 [샘플 데이터를 로드](tutorial-load-sample-data.md)하는 것이 좋습니다.
