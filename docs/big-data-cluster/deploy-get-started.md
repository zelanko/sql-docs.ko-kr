---
title: 시작
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 배포 하기 위한 단계와 리소스에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 41dd39c7aa613083f8ff47824ed6238b6f3c61b9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419429"
---
# <a name="get-started-with-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터 시작

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 [SQL Server 2019 빅 데이터 클러스터 (미리 보기)](big-data-cluster-overview.md)를 배포 하는 방법에 대 한 개요를 제공 합니다. 개념에 대해 설명 하 고이 섹션의 다른 배포 문서를 이해 하기 위한 프레임 워크를 제공 하기 위한 것입니다. 특정 배포 단계는 클라이언트 및 서버에 대 한 플랫폼 선택 사항에 따라 달라 집니다.

## <a id="tools"></a>클라이언트 도구

빅 데이터 클러스터에는 특정 클라이언트 도구 집합이 필요 합니다. Kubernetes에 빅 데이터 클러스터를 배포 하기 전에 다음 도구를 설치 해야 합니다.

| 도구 | 설명 |
|---|---|
| **azdata** | 빅 데이터 클러스터를 배포 하 고 관리 합니다. |
| **kubectl** | 기본 Kubernetes 클러스터를 만들고 관리 합니다. |
| **Azure Data Studio** | 빅 데이터 클러스터를 사용 하기 위한 그래픽 인터페이스입니다. |
| **SQL Server 2019 확장** | 빅 데이터 클러스터 기능을 사용할 수 있는 Azure Data Studio 확장입니다. |

다른 도구는 다양 한 시나리오에 필요 합니다. 각 문서에서는 특정 작업을 수행 하기 위한 필수 구성 요소 도구를 설명 해야 합니다. 도구 및 설치 링크의 전체 목록은 [Install SQL Server 2019 빅 data tools](deploy-big-data-tools.md)를 참조 하세요.

## <a name="kubernetes"></a>Kubernetes

빅 데이터 클러스터는 [Kubernetes](https://kubernetes.io/docs/home)에서 관리 되는 일련의 상호 관련 컨테이너로 배포 됩니다. 다양 한 방법으로 Kubernetes를 호스트할 수 있습니다. 기존 Kubernetes 환경이 이미 있는 경우에도 빅 데이터 클러스터에 대 한 관련 요구 사항을 검토 해야 합니다.

- **Azure Kubernetes 서비스 (AKS)** : AKS를 사용 하면 관리 되는 Kubernetes 클러스터를 Azure에 배포할 수 있습니다. 에이전트 노드만 관리 하 고 유지 관리 합니다. AKS를 사용 하면 클러스터에 대 한 자체 하드웨어를 프로 비전 할 필요가 없습니다. 또한 빅 데이터 클러스터 [배포 스크립트](quickstart-big-data-cluster-deploy.md) 를 사용 하 여 AKS 클러스터를 만들고 빅 데이터 클러스터를 한 번에 배포할 수 있습니다. 빅 데이터 클러스터와 함께 AKS를 사용 하는 방법에 대 한 자세한 내용은 Azure Kubernetes Service를 구성 하는 방법에 대 한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터 (미리 보기) 배포](deploy-on-aks.md)

- **여러 컴퓨터**: 물리적 서버 또는 가상 컴퓨터 일 수 있는 여러 Linux 컴퓨터에 Kubernetes를 배포할 수도 있습니다. [Kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) 도구를 사용 하 여 Kubernetes 클러스터를 만들 수 있습니다. 이 방법은 빅 데이터 클러스터에 사용 하려는 기존 인프라가 이미 있는 경우에 적합 합니다. 빅 데이터 클러스터에서 **kubeadm** 배포를 사용 하는 방법에 대 한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터 (미리 보기) 배포에 대해 여러 컴퓨터에서 Kubernetes 구성](deploy-with-kubeadm.md)을 참조 하세요.

- **Minikube**: Minikube를 사용 하면 단일 서버에서 Kubernetes를 로컬로 실행할 수 있습니다. 빅 데이터 클러스터를 시도 하거나 테스트 또는 개발 시나리오에서 사용 해야 하는 경우에 좋은 옵션입니다. Minikube 사용에 대 한 자세한 내용은 [Minikube 설명서](https://kubernetes.io/docs/setup/minikube/)를 참조 하세요. 빅 데이터 클러스터와 함께 Minikube를 사용 하기 위한 특정 요구 사항은 [Configure Minikube for SQL Server 2019 빅 data cluster 배포](deploy-on-minikube.md)를 참조 하세요.

## <a name="deploy-a-big-data-cluster"></a>빅 데이터 클러스터 배포

Kubernetes을 구성한 후에는 `azdata bdc create` 명령을 사용 하 여 빅 데이터 클러스터를 배포 합니다. 배포할 때 여러 가지 방법을 사용할 수 있습니다.

- 개발-테스트 환경에 배포 하는 경우 **azdata**에서 제공 하는 [기본 구성](deployment-guidance.md#deploy) 중 하나를 사용 하도록 선택할 수 있습니다.

- 배포를 사용자 지정 하기 위해 고유한 [배포 구성 파일](deployment-guidance.md#configfile)을 만들고 사용할 수 있습니다.

- 완전 무인 설치를 위해 환경 변수에서 다른 모든 설정을 전달할 수 있습니다. 자세한 내용은 [무인 배포](deployment-guidance.md#unattended)를 참조 하세요.

## <a name="deployment-scripts"></a>배포 스크립트

배포 스크립트를 통해 Kubernetes 및 빅 데이터 클러스터를 한 번에 배포할 수 있습니다. 또한 빅 데이터 클러스터 설정에 대 한 기본값을 제공 하는 경우가 많습니다. Azure Kubernetes 서비스 (AKS)의 빅 데이터 클러스터 배포 스크립트에 대 한 예는 다음 문서를 참조 하세요.

[배포 스크립트 (AKS)를 사용 하 여 SQL Server 2019 빅 데이터 클러스터를 배포](quickstart-big-data-cluster-deploy.md)합니다.

빅 데이터 클러스터 환경 변수를 다르게 구성 하는 고유한 버전을 만들어 모든 배포 스크립트를 사용자 지정할 수 있습니다.

[Azure Data Studio 노트북을 사용 하 여 SQL Server 2019 빅 데이터 클러스터를 배포](deploy-notebooks.md)합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터를 성공적으로 배포한 후에 [는 클러스터에 연결](connect-to-big-data-cluster.md) 하 고 여러 연습에서 사용할 [샘플 데이터를 로드](tutorial-load-sample-data.md) 하는 것이 좋습니다.