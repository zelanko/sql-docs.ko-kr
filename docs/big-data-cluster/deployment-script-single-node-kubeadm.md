---
title: 단일 노드 kubeadm 클러스터 배포
titleSuffix: SQL Server Big Data Clusters
description: bash 배포 스크립트를 사용하여 단일 노드 kubeadm 클러스터에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]를 배포합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f60256e58339387323f923c85d2b880459455663
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75252096"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>bash 스크립트를 사용하여 단일 노드 kubeadm 클러스터에 배포

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 샘플 bash 배포 스크립트를 통해 kubeadm을 사용하는 단일 노드 Kubernetes 클러스터를 배포하고, 이 클러스터에 SQL Server 빅 데이터 클러스터도 배포합니다.

## <a name="prerequisites"></a>사전 요구 사항

- vanilla Ubuntu 18.04 또는 16.04 **서버** 가상 또는 물리적 머신 모든 종속성은 스크립트에서 설정되며, VM 내에서 스크립트를 실행합니다.

  > [!NOTE]
  > Azure Linux VM은 아직 사용할 수 없습니다.

- VM에는 CPU 8개 이상, 64GB RAM, 100GB 디스크 공간이 있어야 합니다. 빅 데이터 클러스터 Docker 이미지를 모두 끌어오면, 모든 구성 요소에서 사용할 수 있는 데이터 및 로그 공간으로 50GB가 남습니다.

- 다음 명령으로 기존 패키지를 업데이트하여 OS 이미지가 최신 상태인지 확인합니다.

   ``` bash
   sudo apt update && sudo apt upgrade -y
   sudo systemctl reboot
   ```

## <a name="recommended-virtual-machine-settings"></a>권장되는 가상 머신 설정

1. 가상 머신에 대해 정적 메모리 구성을 사용합니다. 예를 들어, Hyper-V 설치에서는 동적 메모리 할당을 사용하지 말고, 대신 권장되는 64GB 이상을 할당합니다.

1. 가상 머신을 클린 상태로 롤백하려면 하이퍼바이저에서 검사점 또는 스냅샷 기능을 사용합니다.


## <a name="instructions-to-deploy-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터를 배포하기 위한 지침

1. 배포에 사용하려는 VM에서 스크립트를 다운로드합니다.

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. 다음 명령을 사용하여 스크립트를 실행 파일로 만듭니다.

   ```bash
   chmod +x setup-bdc.sh
   ```

3. 스크립트를 실행합니다(*sudo*를 사용하여 실행하고 있는지 확인).

   ```bash
   sudo ./setup-bdc.sh
   ```

   메시지가 표시되면 컨트롤러, SQL Server 마스터, 게이트웨이 등의 외부 엔드포인트에 사용할 암호를 입력합니다. 암호는 SQL Server 암호에 대한 기존 규칙에 따라 충분히 복잡해야 합니다. 컨트롤러 사용자 이름은 기본적으로 *admin*으로 설정되어 있습니다.

4. **azdata** 도구의 별칭을 설정합니다.

   ```bash
   source ~/.bashrc
   ```

5. azdata에 대한 별칭 설정을 새로 고칩니다.

   ```bash
   azdata --version
   ```

## <a name="cleanup"></a>정리

[cleanup-bdc.sh](https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/cleanup-bdc.sh) 스크립트는 필요한 경우 환경을 다시 설정할 수 있도록 편의상 제공됩니다. 그러나 테스트 목적으로 가상 머신을 사용하고 하이퍼바이저에서 스냅샷 기능을 사용하여 가상 머신을 클린 상태로 롤백하는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 사용을 시작하려면 [자습서: SQL Server 빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)를 참조하세요.
