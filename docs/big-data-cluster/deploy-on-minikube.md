---
title: SQL Server 2019 CTP 2.0 배포용 Minikube 구성 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 1f20f2adc916a456e4a1975804fac1640ee95f69
ms.sourcegitcommit: 8aecafdaaee615b4cd0a9889f5721b1c7b13e160
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2018
ms.locfileid: "48818051"
---
# <a name="configure-minikube-for-sql-server-2019-ctp-20"></a>SQL Server 2019 CTP 2.0에 대 한 Minikube 구성

Minikube는 쉽게 데스크톱 이나 랩톱 같은 단일 컴퓨터에서 Kubernetes를 실행 하는 도구입니다. Minikube VM 내에서 단일 노드 Kubernetes 클러스터에서 실행 Kubernetes 사용해 또는를 사용 하 여 개발 하려는 사용자에 대 한 노트북 일상적인 됩니다. 

## <a name="prerequisites"></a>사전 요구 사항

- Minikube 클러스터 SQL Server 2019 CTP 2.0에 대 한 SQL 빅 데이터 클러스터 구성에서를 실행 하려면 컴퓨터에 있는 최소 32GB의 RAM이 좋습니다.

   > [!TIP] 
   > 컴퓨터에 메모리가 부족 한 다음 클러스터 구성을 수정는 3 개의 인스턴스가 만들어집니다: 하나의 마스터 인스턴스와 두 개의 계산 인스턴스.

- 컴퓨터의 BIOS에서 VT x 또는 amd-v 가상화를 활성화 되어야 합니다.

## <a name="install-dependencies"></a>종속성 설치

1. 아직 설치 하지 않았으면, 로컬에서 git을 설치 [Windows](https://git-for-windows.github.io/)하십시오 [Linux 또는 Mac](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)합니다.

1. 설치할 [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)합니다.

1. Python 3를 설치 합니다.
   - Pip가 없는 경우 다운로드 한 다음 [get clspip.py](https://bootstrap.pypa.io/get-pip.py) 실행 하 고 `python get-pip.py`입니다.
   - 설치 패키지를 사용 하 여 요청 `python -m pip install requests`합니다.

1. 하이퍼바이저를 설치 하는 아직 없는 경우 지금 설치 합니다.
   - OS X 설치 [xhyve 드라이버](https://git.k8s.io/minikube/docs/drivers.md)하십시오 [VirtualBox](https://www.virtualbox.org/wiki/Downloads), 또는 [VMware Fusion](https://www.vmware.com/products/fusion)합니다.
   - Linux의 경우 설치 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 하거나 [KVM](http://www.linux-kvm.org/)합니다.
   - Windows를 설치 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 하거나 [Hyper-v](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install)합니다. Hyper-v에서 구성 된 외부 스위치가 없으면 그런 다음 외부 네트워크 액세스 권한이 있는 하나를 만듭니다.  참조 하는 방법 [minikube 용 hyper-v의 외부 스위치를 만드는](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/)합니다.

## <a name="install-minikube"></a>Minikube를 설치 합니다.

에 대 한 지침에 따라 Minikube를 설치 합니다 [v0.28.2 릴리스](https://github.com/kubernetes/minikube/releases/tag/v0.28.2)합니다. SQL Server 2019 CTP 2.0 빅 데이터 클러스터 버전 v0.24.1와 등록에 작동합니다.

## <a name="create-a-minikube-cluster"></a>Minikube 클러스터 만들기

아래 명령을 cpu가 8 개를 사용 하 여 Hyper-v VM, 28GB의 메모리 및 100GB의 디스크 크기 minikube 클러스터를 만듭니다. 디스크 크기의 예약 된 공간이 하지 않습니다.  크기가 해당 크기로 디스크에서 필요에 따라 합니다.  디스크를 변경 하지 않는 것이 좋습니다 공간 자체를 100GB 미만의 테스트에서 문제가 발생 했습니다. 이 또한 하이퍼-v 스위치는 외부 액세스를 사용 하 여 명시적으로 지정 합니다.

와 같은 매개 변수를 변경할 **-메모리** 및 사항에 따라 사용 가능한 하드웨어는 필요에 따라 하이퍼바이저를 사용 하는 합니다.  있는지 확인 합니다 **-hyper-v** 가상 스위치 매개 변수 값이 가상 스위치를 만들 때 사용한 이름과 일치 합니다.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

VirtualBox를 사용 하 여 Minikube를 사용 하는 경우 명령은 다음과 같이 보입니다.

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Hyper-v를 사용 하 여 자동 검사점을 사용 하지 않도록 설정

Windows 10에서 자동 검사점을 VM에 사용 됩니다. VM에서 자동 검사점을 사용 하지 않도록 설정 하는 PowerShell에서 아래 명령을 실행 합니다.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>다음 단계

이 문서의 단계 Minikube 클러스터를 구성 합니다. SQL Server 2019 CTP 2.0 클러스터에 배포 하려면 다음 단계가입니다.

[SQL Server 2019 CTP 2.0 Kubernetes에 배포](deployment-guidance.md#deploy)
