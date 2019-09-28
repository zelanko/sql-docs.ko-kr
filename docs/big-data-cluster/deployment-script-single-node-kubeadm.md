---
title: bash 스크립트를 사용하여 단일 노드 kubeadm 클러스터에 배포
titleSuffix: SQL Server big data clusters
description: Bash 배포 스크립트를 사용 하 여 단일 노드 kubeadm 클러스터에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]을 배포 합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2379f96e3b5288fc33f5c925613bf9fd5d35612d
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71341843"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>bash 스크립트를 사용하여 단일 노드 kubeadm 클러스터에 배포

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 샘플 bash 배포 스크립트를 통해 kubeadm을 사용하는 단일 노드 Kubernetes 클러스터를 배포하고, 이 클러스터에 SQL Server 빅 데이터 클러스터도 배포합니다.  

## <a name="prerequisites"></a>사전 요구 사항

- 바닐라 Ubuntu 18.04 또는 16.04 **서버** 가상 또는 물리적 컴퓨터입니다. 모든 종속성은 스크립트에서 설정되며, VM 내에서 스크립트를 실행합니다.

  > [!NOTE]
  > Azure Linux Vm을 사용 하는 것은 아직 지원 되지 않습니다.

- VM에는 8 개 이상의 Cpu, 64 GB RAM 및 100 GB의 디스크 공간이 있어야 합니다. 빅 데이터 클러스터 Docker 이미지를 모두 끌어오면, 모든 구성 요소에서 사용할 수 있는 데이터 및 로그 공간으로 50GB가 남습니다.

- 다음 명령을 사용 하 여 기존 패키지를 업데이트 하 여 OS 이미지가 최신 상태 인지 확인 합니다.

   ``` bash
   sudo apt update && sudo apt upgrade -y
   sudo systemctl reboot
   ```

## <a name="recommended-virtual-machine-settings"></a>권장 되는 가상 컴퓨터 설정

1. 가상 컴퓨터에 대 한 정적 메모리 구성을 사용 합니다. 예를 들어 Hyper-v 설치에서 동적 메모리 할당을 사용 하지 않고 대신 권장 64 g b 이상을 할당 합니다.

1. 가상 컴퓨터를 클린 상태로 롤백하려면 hyper-v에서 검사점 또는 스냅숏 기능을 사용 합니다.


## <a name="instructions-to-deploy-sql-server-big-data-cluster"></a>빅 데이터 클러스터 SQL Server를 배포 하기 위한 지침

1. 배포에 사용하려는 VM에서 스크립트를 다운로드합니다.

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. 다음 명령을 사용하여 스크립트를 실행 파일로 만듭니다.

   ```bash
   chmod +x setup-bdc.sh
   ```

3. 스크립트를 실행 합니다 ( *sudo*를 사용 하 여 실행 하 고 있는지 확인).

   ```bash
   sudo ./setup-bdc.sh
   ```

   메시지가 표시되면 컨트롤러, SQL Server 마스터, 게이트웨이 등의 외부 엔드포인트에 사용할 암호를 입력합니다. 암호는 SQL Server 암호에 대 한 기존 규칙에 따라 충분히 복잡 해야 합니다. 컨트롤러 사용자 이름은 기본적으로 *admin*으로 설정되어 있습니다.

4. **azdata** 도구의 별칭을 설정합니다.

   ```bash
   source ~/.bashrc
   ```

5. Azdata에 대 한 별칭 설치를 새로 고칩니다.

   ```bash
   azdata --version
   ```

## <a name="cleanup"></a>정리

[Cleanup-bdc.sh](https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/cleanup-bdc.sh) 스크립트는 필요한 경우 환경을 다시 설정 하기 위한 편의를 위해 제공 됩니다. 그러나 테스트 목적으로 가상 컴퓨터를 사용 하 고 하이퍼바이저에서 스냅숏 기능을 사용 하 여 가상 컴퓨터를 클린 상태로 롤백하는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 사용을 시작 하려면 [ 자습서를 참조 하세요. SQL Server 빅 데이터 클러스터에 샘플 데이터를 로드 @ no__t-0.
