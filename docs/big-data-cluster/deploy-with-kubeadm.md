---
title: Kubernetes kubeadm를 사용 하 여 구성
titleSuffix: SQL Server big data clusters
description: 여러 Ubuntu 16.04의 Kubernetes 또는 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 배포에 대 한 18.04 컴퓨터 (물리적 또는 가상)를 구성 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 4e79c74851dae2d86b74064799b053d57b1a17db
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488270"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>SQL Server 빅 데이터 클러스터 배포에 대 한 여러 컴퓨터에서 Kubernetes 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서를 사용 하는 방법의 예가 **kubeadm** SQL Server 2019 빅 데이터 클러스터 (미리 보기) 배포에 대 한 여러 컴퓨터에서 Kubernetes 구성 합니다. 이 예제에서는 여러 Ubuntu 16.04 또는 18.04 LTS 컴퓨터 (물리적 또는 가상)의 대상이 됩니다. 다른 Linux 플랫폼에 배포 하는 경우 시스템에 맞게 명령 중 일부를 변경 해야 합니다.  

> [!TIP] 
> Kubernetes를 구성 하는 샘플 스크립트를 참조 하세요 [Kubeadm를 사용 하 여 Ubuntu 16.04 LTS 또는 18.04 LTS에서 Kubernetes 클러스터를 만드는](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm)합니다.

## <a name="prerequisites"></a>사전 요구 사항

- 최소 3 Linux 물리적 컴퓨터 또는 가상 컴퓨터
- 컴퓨터당 권장된 구성:
   - 8 개의 Cpu
   - 32GB의 메모리가
   - 100GB의 저장소

## <a name="prepare-the-machines"></a>컴퓨터 준비

각 컴퓨터에 필요한 필수 구성 요소를 여러 가지입니다. Bash 터미널에서 각 컴퓨터에서 다음 명령을 실행 합니다.

1. 현재 컴퓨터를 추가 합니다 `/etc/hosts` 파일:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. 모든 장치에서 교환 하는 사용 하지 않도록 설정 합니다.

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. 키 가져오기 및 Kubernetes에 대 한 리포지토리를 등록 합니다.

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
 
1. `net.bridge.bridge-nf-call-iptables=1`을 설정합니다. Ubuntu 18.04에서 다음 명령을 먼저 사용 하도록 설정 `br_netfilter`합니다.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Kubernetes 마스터 구성

각 컴퓨터에서 이전 명령 실행 후 Kubernetes 마스터 할 컴퓨터 중 하나를 선택 합니다. 해당 컴퓨터에서 다음 명령을 실행 합니다.

1. 먼저, 다음 명령 사용 하 여 현재 디렉터리에 rbac.yaml 파일을 만듭니다. 

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

1. 이 컴퓨터에서 Kubernetes 마스터를 초기화 합니다. Kubernetes 마스터 성공적으로 초기화 된 출력이 표시 됩니다.

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. 참고는 `kubeadm join` 명령은 Kubernetes 클러스터에 연결할 다른 서버에서 사용 해야 합니다. 나중에 사용할이 복사 합니다.

   ![kubeadm 조인](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Kubernetes 구성 파일을 홈 디렉터리를 설정 합니다.

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. 클러스터와 Kubernetes 대시보드를 구성 합니다.

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>Kubernetes 에이전트 구성

다른 컴퓨터는 클러스터의 Kubernetes 에이전트 처럼 작동 합니다. 

각각의 다른 컴퓨터에서 실행 하는 `kubeadm join` 이전 섹션에서 복사한 명령입니다.

![kubeadm 조인 에이전트](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>클러스터 상태 확인

클러스터에 대 한 연결을 확인 하려면 사용 합니다 [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) 클러스터 노드의 목록을 반환 하는 명령입니다.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>다음 단계

이 문서의 단계를 여러 Ubuntu 컴퓨터에서 Kubernetes 클러스터를 구성 합니다. 다음 단계는 SQL Server 2019 빅 데이터 클러스터를 배포 하는 것입니다. 자세한 내용은 다음 문서를 참조 합니다.

[Kubernetes에서 SQL Server 배포](deployment-guidance.md#deploy)
