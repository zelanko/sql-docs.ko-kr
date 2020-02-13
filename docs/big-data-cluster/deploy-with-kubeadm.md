---
title: Kubeadm을 사용하여 Kubernetes 구성
titleSuffix: SQL Server Big Data Clusters
description: 여러 Ubuntu 16.04 또는 18.04 머신(물리적 또는 가상)에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 배포에 대해 Kubernetes를 구성하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6b5f2c8dac062f147326a0b9fcfb7120f0648729
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74165432"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>여러 머신에서 SQL Server 빅 데이터 클러스터 배포에 대해 Kubernetes 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 **kubeadm**을 사용하여 여러 머신에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 배포에 대해 Kubernetes를 구성하는 방법의 예제를 제공합니다. 이 예제에서는 여러 Ubuntu 16.04 또는 18.04 LTS 머신(물리적 또는 가상)이 대상입니다. 다른 Linux 플랫폼에 배포하는 경우 일부 명령을 시스템에 맞게 변경해야 합니다.  

> [!TIP] 
> Kubernetes를 구성하는 샘플 스크립트는 [Ubuntu 16.04 LTS 또는 18.04 LTS에서 Kubeadm을 사용하여 Kubernetes 클러스터 만들기](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm)를 참조하세요.
또한 VM에서 단일 노드 kubeadm 배포를 자동화한 이후 그 위에 빅 데이터 클러스터의 기본 구성을 배포하는 샘플 스크립트는 [해당 항목](deployment-script-single-node-kubeadm.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

- Linux 물리적 머신 또는 가상 머신 3대 이상
- 머신당 권장 구성:
   - CPU 8개
   - 64GB 메모리
   - 100GB 스토리지
 
> [!Important] 
> 빅 데이터 클러스터 배포를 시작하기 전에 배포 대상인 모든 Kubernetes 노드에서 시계가 동기화되는지 확인합니다. 빅 데이터 클러스터에는 시간이 중요한 다양한 서비스에 대한 기본 상태 속성이 있으며 시간이 왜곡되면 상태가 잘못될 수 있습니다.

## <a name="prepare-the-machines"></a>머신 준비

각 머신에 대한 몇 가지 필수 조건이 있습니다. Bash 터미널을 통해 각 머신에서 다음 명령을 실행합니다.

1. 현재 머신을 `/etc/hosts` 파일에 추가합니다.

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. 모든 디바이스에서 교환을 사용하지 않도록 설정합니다.

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. 키를 가져오고 Kubernetes의 리포지토리에 등록합니다.

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. 머신에서 docker 및 Kubernetes 필수 조건을 구성합니다.

   ```bash
   KUBE_DPKG_VERSION=1.15.0-00 #or your other target K8s version, which should be at least 1.13.
   sudo apt-get update && \
   sudo apt-get install -y ebtables ethtool && \
   sudo apt-get install -y docker.io && \
   sudo apt-get install -y apt-transport-https && \
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && \
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. `net.bridge.bridge-nf-call-iptables=1`을 설정합니다. Ubuntu 18.04에서 다음 명령은 먼저 `br_netfilter`를 사용하도록 설정합니다.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Kubernetes 마스터 구성

각 머신에서 이전 명령을 실행한 후 머신 중 하나를 Kubernetes 마스터로 선택합니다. 해당 머신에서 다음 명령을 실행합니다.

1. 먼저 다음 명령을 사용하여 현재 디렉터리에 rbac.yaml 파일을 만듭니다. 

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

1. 이 머신에서 Kubernetes 마스터를 초기화합니다. 아래 예제 스크립트는 Kubernetes 버전 `1.15.0`을 지정합니다. 사용하는 버전은 Kubernetes 클러스터에 따라 다릅니다.

   ```bash
   KUBE_VERSION=1.15.0
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

   Kubernetes 마스터가 초기화되었다는 출력이 표시됩니다.

1. Kubernetes 클러스터를 조인할 다른 서버에서 사용해야 하는 `kubeadm join` 명령을 확인합니다. 나중에 사용하기 위해 이 명령을 복사합니다.

   ![kubeadm join](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Kubernetes 구성 파일에서 홈 디렉터리를 설정합니다.

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. 클러스터 및 Kubernetes 대시보드를 구성합니다.

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>Kubernetes 에이전트 구성

다른 머신은 클러스터에서 Kubernetes 에이전트 역할을 합니다. 

이전 섹션에서 복사한 `kubeadm join` 명령을 다른 머신에서 각각 실행합니다.

![kubeadm join 에이전트](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>클러스터 상태 보기

클러스터에 대한 연결을 확인하려면 [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) 명령을 사용하여 클러스터 노드 목록을 반환합니다.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>다음 단계

이 문서의 단계에서는 여러 Ubuntu 머신에서 Kubernetes 클러스터를 구성했습니다. 다음 단계는 SQL Server 2019 빅 데이터 클러스터를 배포하는 것입니다. 자세한 내용은 다음 문서를 참조하세요.

[Kubernetes에 SQL Server 배포](deployment-guidance.md#deploy)
