---
title: minikube 구성
titleSuffix: SQL Server big data clusters
description: 단일 컴퓨터에서 배포에 대해 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] minikube를 구성 하는 방법에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b2022fe6ad8a0aa23c4dd7d917e925ae1daba572
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652402"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>SQL Server 빅 데이터 클러스터 배포에 대해 minikube 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 단일 컴퓨터 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 에서 배포 하도록 **minikube** 를 구성 하는 방법을 설명 합니다. minikube는 노트북 또는 데스크톱과 같은 단일 머신에서 Kubernetes를 간편하게 실행할 수 있는 도구입니다. minikube는 Kubernetes를 사용해 보거나 일상적인 개발 작업에 이용하려는 사용자를 위해 노트북의 VM 내에서 단일 노드 Kubernetes 클러스터를 실행합니다. 

## <a name="prerequisites"></a>사전 요구 사항

- 64 GB의 메모리가 있습니다.

- 머신에 최소 권장 메모리만 있는 경우 컴퓨팅 풀 인스턴스 1개, 데이터 풀 인스턴스 1개, 스토리지 풀 인스턴스 1개만 포함되도록 클러스터 배포를 구성합니다. 이 구성은 데이터의 내구성과 가용성이 중요하지 않은 평가 환경에서만 사용해야 합니다. 데이터 풀, 컴퓨팅 풀, 스토리지 풀의 복제본 수를 구성하기 위해 설정할 환경 변수에 대한 자세한 내용은 [배포 설명서](deployment-guidance.md#configfile)를 참조하세요.

- 컴퓨터의 BIOS에서 VT-x 또는 AMD-v 가상화를 사용하도록 설정해야 합니다.

## <a name="install-dependencies"></a>종속성 설치

1. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)을 설치합니다.

1. 아직 하이퍼바이저가 설치되지 않은 경우 지금 설치합니다.
   - OS X의 경우 [xhyve 드라이버](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 또는 [VMware Fusion](https://www.vmware.com/products/fusion)을 설치합니다.
   - Linux의 경우 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 또는 [KVM](https://www.linux-kvm.org/)을 설치합니다.
   - Windows의 경우 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 또는 [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install)를 설치합니다. Hyper-v에서 구성 된 외부 스위치가 없는 경우 외부 네트워크 액세스 권한이 있는 외부 스위치를 만듭니다. [Minikube 용 hyper-v에서 외부 스위치를 만드는](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/)방법에 대해 알아봅니다.

## <a name="install-minikube"></a>minikube 설치

[V 1.3.0 릴리스에](https://github.com/kubernetes/minikube/releases/tag/v1.3.0)대 한 지침에 따라 minikube 릴리스를 설치 합니다. 는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 버전 v 1.0.0 이상 에서만 작동 합니다.

## <a name="create-a-minikube-cluster"></a>minikube 클러스터 만들기

아래 명령은 Cpu 8 개, 64 GB의 메모리, 100 GB의 디스크 크기를 사용 하 여 Hyper-v VM에 minikube 클러스터를 만듭니다. 디스크 크기는 예약된 공간이 아닙니다.  필요에 따라 디스크에서 해당 크기까지 확장됩니다.  디스크 공간을 100GB 미만으로 변경하지 않는 것이 좋습니다. 테스트 중에 이렇게 변경하면 문제가 발생했습니다. 또한 외부 액세스를 사용 하 여 Hyper-v 스위치를 명시적으로 지정 합니다.

사용 가능한 하드웨어 및 사용 중인 하이퍼바이저에 따라 **--memory** 등의 매개 변수를 적절하게 변경합니다.  **--hyper-v** 가상 스위치 매개 변수 값이 가상 스위치를 만들 때 사용한 이름과 일치하는지 확인합니다.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 65536 --disk-size 100g --hyperv-virtual-switch "External"
```

VirtualBox와 함께 minikube를 사용하는 경우 명령은 다음과 같습니다.

```base
minikube start --cpus 8 --memory 65536 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Hyper-V에서 자동 검사점 사용 안 함

Windows 10에서는 VM에서 자동 검사점이 사용하도록 설정됩니다. PowerShell에서 아래 명령을 실행 하 여 VM에서 자동 검사점을 사용 하지 않도록 설정 하 고 메모리를 정적으로 설정 합니다.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false -StaticMemory
```

## <a name="next-steps"></a>다음 단계

이 문서의 단계에서는 minikube 클러스터를 구성했습니다. 다음 단계는 SQL Server 2019 빅 데이터 클러스터를 배포하는 것입니다. 자세한 내용은 다음 문서를 참조하세요.

[Kubernetes [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 에 배포](deployment-guidance.md#deploy)
