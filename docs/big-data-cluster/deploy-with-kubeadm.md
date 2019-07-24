---
title: Kubeadm를 사용 하 여 Kubernetes 구성
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기) 배포에 대 한 여러 Ubuntu 16.04 또는 18.04 컴퓨터 (실제 또는 가상)에서 Kubernetes를 구성 하는 방법에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ea79503869e7d403e4d3f4f960de9c95760eda0f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419451"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>SQL Server 빅 데이터 클러스터 배포를 위해 여러 컴퓨터에서 Kubernetes 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 **kubeadm** 를 사용 하 여 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 배포에 대해 여러 컴퓨터에서 Kubernetes를 구성 하는 방법에 대 한 예제를 제공 합니다. 이 예제에서는 여러 Ubuntu 16.04 또는 18.04 LTS 컴퓨터 (실제 또는 가상)가 대상입니다. 다른 Linux 플랫폼에 배포 하는 경우 일부 명령을 시스템에 맞게 변경 해야 합니다.  

> [!TIP] 
> Kubernetes를 구성 하는 샘플 스크립트는 [Ubuntu 16.04 lts 또는 18.04 lts에서 Kubeadm를 사용 하 여 Kubernetes 클러스터 만들기](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm)를 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

- 최소 3 대의 Linux 물리적 컴퓨터 또는 가상 컴퓨터
- 컴퓨터 당 권장 구성:
   - Cpu 8 개
   - 64 GB의 메모리
   - 100 GB의 저장소

## <a name="prepare-the-machines"></a>컴퓨터 준비

각 컴퓨터에는 몇 가지 필수 구성 요소가 있습니다. Bash 터미널에서 각 컴퓨터에 대해 다음 명령을 실행 합니다.

1. 현재 컴퓨터를 `/etc/hosts` 파일에 추가 합니다.

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. 모든 장치에서 스와핑을 사용 하지 않도록 설정 합니다.

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. 키를 가져오고 Kubernetes에 대 한 리포지토리를 등록 합니다.

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. 컴퓨터에서 docker 및 Kubernetes 필수 구성 요소를 구성 합니다.

   ```bash
   KUBE_DPKG_VERSION=1.11.3-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. `net.bridge.bridge-nf-call-iptables=1`을 설정합니다. Ubuntu 18.04에서 다음 명령은 먼저를 사용 하도록 `br_netfilter`설정 합니다.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Kubernetes 마스터 구성

각 컴퓨터에서 이전 명령을 실행 한 후 Kubernetes 마스터로 사용할 컴퓨터 중 하나를 선택 합니다. 그런 다음 해당 컴퓨터에서 다음 명령을 실행 합니다.

1. 먼저 다음 명령을 사용 하 여 현재 디렉터리에 rbac. yaml 파일을 만듭니다. 

   ```bash
   cat <<EOF > rbac.yaml
   apiVersion: rbac.authorization.k8s.io/v1beta1
   kind: ClusterRoleBinding
   metadata:
     name: default-rbac
   subjects:
   - kind: ServiceAccount
     name: default
     namespace: default
   roleRef:
     kind: ClusterRole
     name: cluster-admin
     apiGroup: rbac.authorization.k8s.io
   EOF
   ```

1. 이 컴퓨터에서 Kubernetes 마스터를 초기화 합니다. Kubernetes 마스터가 성공적으로 초기화 되었다는 출력이 표시 됩니다.

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. 다른 서버에서 Kubernetes 클러스터에 연결 하는 데 사용 해야 하는 명령을확인합니다.`kubeadm join` 나중에 사용 하기 위해이를 복사 합니다.

   ![kubeadm join](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Kubernetes 구성 파일의 홈 디렉터리를 설정 합니다.

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. 클러스터 및 Kubernetes 대시보드를 구성 합니다.

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>Kubernetes 에이전트 구성

다른 컴퓨터는 클러스터에서 Kubernetes 에이전트 역할을 합니다. 

다른 각 컴퓨터에서 이전 섹션에서 복사한 `kubeadm join` 명령을 실행 합니다.

![kubeadm join 에이전트](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>클러스터 상태 보기

클러스터에 대 한 연결을 확인 하려면 [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) 명령을 사용 하 여 클러스터 노드 목록을 반환 합니다.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>다음 단계

이 문서의 단계는 여러 Ubuntu 컴퓨터에서 Kubernetes 클러스터를 구성 했습니다. 다음 단계는 SQL Server 2019 빅 데이터 클러스터를 배포 하는 것입니다. 자세한 지침은 다음 문서를 참조 하세요.

[Kubernetes에 SQL Server 배포](deployment-guidance.md#deploy)
