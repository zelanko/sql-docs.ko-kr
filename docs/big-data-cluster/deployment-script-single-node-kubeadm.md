---
title: bash 스크립트를 사용하여 단일 노드 kubeadm 클러스터에 배포
titleSuffix: SQL Server big data clusters
description: bash 배포 스크립트를 사용하여 단일 노드 kubeadm 클러스터에 SQL Server 2019 빅 데이터 클러스터(미리 보기)를 배포합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 37017221b636146a003f8af8890c655ed605bca9
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68473075"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>bash 스크립트를 사용하여 단일 노드 kubeadm 클러스터에 배포

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 샘플 bash 배포 스크립트를 통해 kubeadm을 사용하는 단일 노드 Kubernetes 클러스터를 배포하고, 이 클러스터에 SQL Server 빅 데이터 클러스터도 배포합니다.  

## <a name="prerequisites"></a>사전 요구 사항

- vanilla Ubuntu 18.04 또는 16.04 **서버** VM. 모든 종속성은 스크립트에서 설정되며, VM 내에서 스크립트를 실행합니다.

  > [!NOTE]
  > Azure VM은 아직 사용할 수 없습니다.

- VM에는 CPU 8개 이상, 64GB RAM, 100GB 디스크 공간이 있어야 합니다. 빅 데이터 클러스터 Docker 이미지를 모두 끌어오면, 모든 구성 요소에서 사용할 수 있는 데이터 및 로그 공간으로 50GB가 남습니다.

## <a name="instructions"></a>Instructions

1. 배포에 사용하려는 VM에서 스크립트를 다운로드합니다.

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. 다음 명령을 사용하여 스크립트를 실행 파일로 만듭니다.

   ```bash
   chmod +x setup-bdc.sh
   ```

3. **sudo** 권한으로 스크립트를 실행합니다.

   ```bash
   sudo ./setup-bdc.sh
   ```

   메시지가 표시되면 컨트롤러, SQL Server 마스터, 게이트웨이 등의 외부 엔드포인트에 사용할 암호를 입력합니다. 컨트롤러 사용자 이름은 기본적으로 *admin*으로 설정되어 있습니다.

4. **azdata** 도구의 별칭을 설정합니다.

   ```bash
   source ~/.bashrc
   ```

5. 별칭이 작동하는지 확인합니다.

   ```bash
   azdata --version
   ```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 사용을 시작하려면 [이 자습서](tutorial-load-sample-data.md)를 진행합니다.
