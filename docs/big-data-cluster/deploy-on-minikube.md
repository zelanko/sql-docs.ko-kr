---
title: minikube 구성
titleSuffix: SQL Server big data clusters
description: 단일 머신에서 SQL Server 2019 빅 데이터 클러스터(미리 보기) 배포에 대해 minikube를 구성하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6c2261b5cfbbe590c76ce410da4b95ee678a20b5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958470"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>SQL Server 빅 데이터 클러스터 배포에 대해 minikube 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 단일 머신에서 SQL Server 2019 빅 데이터 클러스터(미리 보기) 배포에 대해 **minikube**를 구성하는 방법을 설명합니다. minikube는 노트북 또는 데스크톱과 같은 단일 머신에서 Kubernetes를 간편하게 실행할 수 있는 도구입니다. minikube는 Kubernetes를 사용해 보거나 일상적인 개발 작업에 이용하려는 사용자를 위해 노트북의 VM 내에서 단일 노드 Kubernetes 클러스터를 실행합니다. 

## <a name="prerequisites"></a>사전 요구 사항

- 32GB 메모리(64GB 권장)

- 머신에 최소 권장 메모리만 있는 경우 컴퓨팅 풀 인스턴스 1개, 데이터 풀 인스턴스 1개, 스토리지 풀 인스턴스 1개만 포함되도록 클러스터 배포를 구성합니다. 이 구성은 데이터의 내구성과 가용성이 중요하지 않은 평가 환경에서만 사용해야 합니다. 데이터 풀, 컴퓨팅 풀, 스토리지 풀의 복제본 수를 구성하기 위해 설정할 환경 변수에 대한 자세한 내용은 [배포 설명서](deployment-guidance.md#configfile)를 참조하세요.

- 컴퓨터의 BIOS에서 VT-x 또는 AMD-v 가상화를 사용하도록 설정해야 합니다.

## <a name="install-dependencies"></a>종속성 설치

1. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)을 설치합니다.

1. Python 3을 설치합니다.
   - pip가 누락되면 [get-clspip.py](https://bootstrap.pypa.io/get-pip.py)를 다운로드하고 `python get-pip.py`를 실행합니다.
   - `python -m pip install requests`를 사용하여 요청 패키지를 설치합니다.

1. 아직 하이퍼바이저가 설치되지 않은 경우 지금 설치합니다.
   - OS X의 경우 [xhyve 드라이버](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 또는 [VMware Fusion](https://www.vmware.com/products/fusion)을 설치합니다.
   - Linux의 경우 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 또는 [KVM](https://www.linux-kvm.org/)을 설치합니다.
   - Windows의 경우 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 또는 [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install)를 설치합니다. hyper-v에 외부 스위치가 구성되지 않은 경우 외부 네트워크 액세스 권한이 있는 외부 스위치를 만듭니다.  [hyper-v에서 minikube용 외부 스위치를 만드는](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/) 방법을 참조하세요.

## <a name="install-minikube"></a>minikube 설치

[v0.28.2 릴리스](https://github.com/kubernetes/minikube/releases/tag/v0.28.2) 지침에 따라 minikube를 설치합니다. SQL Server 2019 빅 데이터 클러스터(미리 보기)는 버전 v0.24.1 이상에서만 작동합니다.

## <a name="create-a-minikube-cluster"></a>minikube 클러스터 만들기

아래 명령은 CPU 8개, 28GB 메모리, 100GB 디스크 크기의 Hyper-V VM에서 minikube 클러스터를 만듭니다. 디스크 크기는 예약된 공간이 아닙니다.  필요에 따라 디스크에서 해당 크기까지 확장됩니다.  디스크 공간을 100GB 미만으로 변경하지 않는 것이 좋습니다. 테스트 중에 이렇게 변경하면 문제가 발생했습니다. 또한 이 명령은 외부 액세스 권한이 있는 hyper-v 스위치를 명시적으로 지정합니다.

사용 가능한 하드웨어 및 사용 중인 하이퍼바이저에 따라 **--memory** 등의 매개 변수를 적절하게 변경합니다.  **--hyper-v** 가상 스위치 매개 변수 값이 가상 스위치를 만들 때 사용한 이름과 일치하는지 확인합니다.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

VirtualBox와 함께 minikube를 사용하는 경우 명령은 다음과 같습니다.

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Hyper-V에서 자동 검사점 사용 안 함

Windows 10에서는 VM에서 자동 검사점이 사용하도록 설정됩니다. VM에서 자동 검사점을 사용하지 않으려면 PowerShell에서 아래 명령을 실행합니다.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>다음 단계

이 문서의 단계에서는 minikube 클러스터를 구성했습니다. 다음 단계는 SQL Server 2019 빅 데이터 클러스터를 배포하는 것입니다. 자세한 내용은 다음 문서를 참조하세요.

[Kubernetes에 SQL Server 2019 빅 데이터 클러스터 배포](deployment-guidance.md#deploy)
