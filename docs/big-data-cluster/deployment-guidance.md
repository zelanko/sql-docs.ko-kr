---
title: 배포 지침
titleSuffix: SQL Server Big Data Clusters
description: Kubernetes에 SQL Server 빅 데이터 클러스터를 배포하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 828ad42bd6ecdc31d6e1c99a489fb4cbe8548d0e
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531082"
---
# <a name="how-to-deploy-big-data-clusters-2019-on-kubernetes"></a>Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 빅 데이터 클러스터는 Kubernetes 클러스터에 docker 컨테이너로 배포됩니다. 다음은 설치 및 구성 단계의 개요입니다.

- 단일 VM, VM 클러스터 또는 AKS(Azure Kubernetes Service)에서 Kubernetes 클러스터를 설정합니다.
- 클라이언트 머신에 클러스터 구성 도구 `azdata`를 설치합니다.
- Kubernetes 클러스터에 SQL Server 빅 데이터 클러스터를 배포합니다.

## <a name="install-sql-server-2019-big-data-tools"></a>SQL Server 2019 빅 데이터 도구 설치

SQL Server 2019 빅 데이터 클러스터를 배포하기 전에 먼저 [빅 데이터 도구를 설치](deploy-big-data-tools.md)합니다.

- `azdata`
- `kubectl`
- Azure Data Studio
- Azure Data Studio용 [데이터 가상화 확장](../azure-data-studio/data-virtualization-extension.md)

## <a name="kubernetes-prerequisites"></a><a id="prereqs"></a> Kubernetes 필수 조건

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 사용하려면 서버와 클라이언트 모두에 Kubernetes v1.13 이상이 필요합니다(kubectl).

> [!NOTE]
> 클라이언트 및 서버 Kubernetes 버전은 바로 이전 또는 이후 부 버전 이내여야 합니다. 자세한 내용은 [Kubernetes 릴리스 정보 및 버전 기울이기 SKU 정책](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)을 참조하세요.

### <a name="kubernetes-cluster-setup"></a><a id="kubernetes"></a> Kubernetes 클러스터 설정

위 필수 조건을 충족하는 Kubernetes 클러스터가 이미 있는 경우에는 [배포 단계](#deploy)로 건너뛰어도 됩니다. 이 섹션에서는 Kubernetes 개념에 대한 기본 지식이 있다고 가정합니다.  Kubernetes에 대한 자세한 내용은 [Kubernetes 설명서](https://kubernetes.io/docs/home)를 참조하세요.

다음 세 가지 방법 중 하나로 Kubernetes를 배포할 수 있습니다.

| Kubernetes 배포 위치: | Description | 링크 |
|---|---|---|
| **AKS(Azure Kubernetes Service)** | Azure의 관리되는 Kubernetes 컨테이너 서비스입니다. | [지침](deploy-on-aks.md) |
| **단일 또는 여러 머신(`kubeadm`)** | `kubeadm`을 사용하여 물리적 머신 또는 가상 머신에 배포된 Kubernetes 클러스터입니다. | [지침](deploy-with-kubeadm.md) |

> [!TIP]
> AKS 및 빅 데이터 클러스터의 배포를 한 단계로 스크립팅할 수도 있습니다. 자세한 내용은 [python 스크립트](quickstart-big-data-cluster-deploy.md) 또는 Azure Data Studio [Notebook](notebooks-deploy.md)의 작업 방법을 참조하세요.

### <a name="verify-kubernetes-configuration"></a>Kubernetes 구성 확인

`kubectl` 명령을 실행하여 클러스터 구성을 살펴봅니다. kubectl이 올바른 클러스터 컨텍스트를 가리키는지 확인합니다.

```bash
kubectl config view
```

> [!Important] 
> `kubeadm`을 사용하여 부트스트랩한 다중 노드 Kuberntes 클러스터에 배포하는 경우 빅 데이터 클러스터 배포를 시작하기 전에 배포 대상인 모든 Kubernetes 노드에서 시계가 동기화되는지 확인합니다. 빅 데이터 클러스터에는 시간이 중요한 다양한 서비스에 대한 기본 상태 속성이 있으며 시간이 왜곡되면 상태가 잘못될 수 있습니다.

Kubernetes 클러스터를 구성한 후에는 새로운 SQL Server 빅 데이터 클러스터의 배포를 진행할 수 있습니다. 이전 릴리스에서 업그레이드하는 경우 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 업그레이드하는 방법](deployment-upgrade.md)을 참조하세요.

## <a name="ensure-you-have-storage-configured"></a>스토리지를 구성했는지 확인

대부분의 빅 데이터 클러스터 배포에는 영구 스토리지가 있어야 합니다. 이번에는 BDC를 배포하기 전에 Kubernetes 클러스터에서 영구 스토리지를 제공하는 방법에 대한 계획이 있는지 확인해야 합니다.

AKS에서 배포하는 경우에는 스토리지를 설치할 필요가 없습니다. AKS는 동적 프로비저닝을 사용하는 기본 제공 스토리지 클래스를 제공합니다. 배포 구성 파일에서 스토리지 클래스(`default` 또는 `managed-premium`)를 사용자 지정할 수 있습니다. 기본 제공 프로필은 `default` 스토리지 클래스를 사용합니다. `kubeadm`을 사용하여 배포한 Kubernetes 클러스터에 배포하는 경우 원하는 크기의 클러스터에 대해 충분한 스토리지를 사용할 수 있는지 사용할 수 있게 구성되어 있는지 확인해야 합니다. 스토리지를 사용하는 방법을 사용자 지정하려는 경우 계속하기 전에 이 작업을 수행해야 합니다. [Kubernetes의 SQL Server 빅 데이터 클러스터를 사용한 데이터 지속성](concept-data-persistence.md)을 참조하세요.

## <a name="deployment-overview"></a><a id="deploy"></a> 배포 개요

대부분의 빅 데이터 클러스터 설정은 JSON 배포 구성 파일에 정의되어 있습니다. `kubeadm`으로 만든 AKS 및 Kubernetes 클러스터에 기본 배포 프로필을 사용해도 되고, 설치 중에 사용할 고유한 배포 구성 파일을 사용자 지정할 수도 있습니다. 보안을 위해 인증 설정은 환경 변수를 통해 전달됩니다.

다음 섹션에서는 빅 데이터 클러스터 배포를 구성하는 방법에 대한 자세한 내용과 일반적인 사용자 지정 예제를 제공합니다. 언제든지 VS Code 등의 편집기를 사용하여 사용자 지정 배포 구성 파일을 편집할 수도 있습니다.

## <a name="default-configurations"></a><a id="configfile"></a> 기본 구성

빅 데이터 클러스터 배포 옵션은 JSON 구성 파일에 정의되어 있습니다. `azdata`에서 사용할 수 있는 기본 제공 배포 프로필에서 클러스터 배포 사용자 지정을 시작할 수 있습니다. 

> [!NOTE]
> 빅 데이터 클러스터 배포에 필요한 컨테이너 이미지는 `mssql/bdc` 리포지토리의 Microsoft Container Registry(`mcr.microsoft.com`)에 호스팅됩니다. 기본적으로 이러한 설정은 `azdata`에 들어 있는 각 배포 프로필의 `control.json` 구성 파일에 이미 포함되어 있습니다. 각 릴리스의 컨테이너 이미지 태그도 동일한 구성 파일로 미리 채워집니다. 컨테이너 이미지를 프라이빗 컨테이너 레지스트리로 끌어오거나 컨테이너 레지스트리/리포지토리 설정을 수정해야 하는 경우 [오프라인 설치 문서](deploy-offline.md)의 지침을 따릅니다.

다음 명령을 실행하여 어떤 템플릿을 사용할 수 있는지 확인합니다.

```
azdata bdc config list -o table 
```

예를 들어 SQL Server 2019 RTM 서비스 업데이트(GDR1) 릴리스의 경우 위의 명령이 다음을 반환합니다.

```
Result
----------------
aks-dev-test
aks-dev-test-ha
kubeadm-dev-test
kubeadm-prod
```

| 배포 프로필 | Kubernetes 환경 |
|---|---|
| `aks-dev-test` | AKS(Azure Kubernetes Service)에 SQL Server 빅 데이터 클러스터 배포|
| `aks-dev-test-ha` | AKS(Azure Kubernetes Service)에 SQL Server 빅 데이터 클러스터를 배포합니다. SQL Server 마스터 및 HDFS 이름 노드와 같은 중요 업무용 서비스는 고가용성 중심으로 구성됩니다.|
| `kubeadm-dev-test` | 단일 또는 여러 물리적 머신이나 가상 머신을 사용하여 kubeadm으로 만든 Kubernetes 클러스터에 SQL Server 빅 데이터 클러스터를 배포합니다.|
| `kubeadm-prod`| 단일 또는 여러 물리적 머신이나 가상 머신을 사용하여 kubeadm으로 만든 Kubernetes 클러스터에 SQL Server 빅 데이터 클러스터를 배포합니다. 이 템플릿을 사용하여 빅 데이터 클러스터 서비스를 Active Directory와 통합할 수 있습니다. SQL Server 마스터 인스턴스 및 HDFS 이름 노드와 같은 중요 업무용 서비스는 고가용성 구성으로 배포됩니다.  |

`azdata bdc create`를 실행하여 빅 데이터 클러스터를 배포할 수 있습니다. 기본 구성 중 하나를 선택하라는 메시지가 표시되고 배포 과정이 안내됩니다.

`azdata`를 처음 실행하는 경우 `--accept-eula=yes`를 포함하여 EULA(최종 사용자 사용권 계약)에 동의해야 합니다.

```bash
azdata bdc create --accept-eula=yes
```

이 시나리오에서는 기본 구성에 포함되지 않는 설정(예: 암호)을 묻는 메시지가 표시됩니다. 

> [!IMPORTANT]
> 빅 데이터 클러스터의 기본 이름은 `mssql-cluster`입니다. `-n` 매개 변수를 사용하여 Kubernetes 네임스페이스를 지정하는 `kubectl` 명령을 실행하려면 이 이름을 알고 있어야 합니다.

## <a name="custom-configurations"></a><a id="customconfig"></a> 사용자 지정 구성

또한 실행하려는 워크로드에 맞게 배포를 사용자 지정할 수 있습니다. 배포 후 빅 데이터 클러스터 서비스의 크기(복제본 수) 또는 스토리지 설정을 변경할 수 없으므로, 용량 이슈가 없도록 배포 구성을 신중하게 계획해야 합니다. 배포를 사용자 지정하려면 다음 단계를 수행합니다.

1. Kubernetes 환경과 일치하는 표준 배포 프로필 중 하나로 시작합니다. 다음과 같이 `azdata bdc config list` 명령을 사용하여 프로필을 나열할 수 있습니다.

   ```bash
   azdata bdc config list
   ```

1. 배포를 사용자 지정하려면 `azdata bdc config init` 명령을 사용하여 배포 프로필의 복사본을 만듭니다. 예를 들어 다음 명령은 `custom`이라는 대상 디렉터리에 `aks-dev-test` 배포 구성 파일의 복사본을 만듭니다.

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   >[!TIP]
   >`--target`은 `--source` 매개 변수에 따라 구성 파일 `bdc.json` 및 `control.json`이 포함된 디렉터리를 지정합니다.

1. 배포 구성 프로필의 설정을 사용자 지정하려면 JSON 파일을 편집하는 데 적합한 VS Code 등의 도구에서 배포 구성 파일을 편집할 수 있습니다. 스크립팅된 자동화를 위해 `azdata bdc config` 명령을 사용하여 사용자 지정 배포 프로필을 편집할 수도 있습니다. 예를 들어 다음 명령은 사용자 지정 배포 프로필을 변경하여 배포된 클러스터의 이름을 기본값(`mssql-cluster`)에서 `test-cluster`로 변경합니다.  

   ```bash
   azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > *azdata create bdc* 명령의 *--name* 매개 변수를 사용하여 배포 시 클러스터 이름을 전달할 수도 있습니다. 명령의 매개 변수는 구성 파일의 값보다 우선합니다.
   >
   > JSON 경로를 찾는 데 유용한 도구는 [JSONPath Online Evaluator](https://jsonpath.com/)입니다.
   >
   키-값 쌍을 전달하는 것 외에도 인라인 JSON 값을 제공하거나 JSON 패치 파일을 전달할 수 있습니다. 자세한 내용은 [빅 데이터 클러스터의 배포 설정 구성](deployment-custom-configuration.md)을 참조하세요.

1. 사용자 지정 구성 파일을 `azdata bdc create`에 전달합니다. 필수 [환경 변수](#env)를 설정해야 합니다. 설정하지 않으면 다음과 같이 터미널에서 값을 요구합니다.

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> 배포 구성 파일의 구조에 대한 자세한 내용은 [배포 구성 파일 참조](reference-deployment-config.md)를 참조하세요. 더 많은 구성 예제를 보려면 [빅 데이터 클러스터의 배포 설정 구성](deployment-custom-configuration.md)을 참조하세요.

## <a name="environment-variables"></a><a id="env"></a> 환경 변수

다음 환경 변수는 배포 구성 파일에 저장되지 않은 보안 설정에 사용됩니다. 자격 증명을 제외한 Docker 설정은 구성 파일에서 설정할 수 있습니다.

| 환경 변수 | 요구 사항 |Description |
|---|---|---|
| `AZDATA_USERNAME` | 필수 |SQL Server 빅 데이터 클러스터 관리자의 사용자 이름입니다. 이름이 같은 sysadmin 로그인이 SQL Server 마스터 인스턴스에 만들어집니다. 보안 모범 사례에 따라 `sa` 계정은 사용하지 않도록 설정됩니다. |
| `AZDATA_PASSWORD` | 필수 |위에서 만든 사용자 계정의 암호입니다. Knox 게이트웨이 및 HDFS를 보호하는 데 사용되는 것과 동일한 암호가 `root` 사용자에게 사용됩니다. |
| `ACCEPT_EULA`| `azdata`를 처음 사용하는 경우 필수| "예"로 설정합니다. 환경 변수로 설정하면 SQL Server와 `azdata`에 모두 EULA가 적용됩니다. 환경 변수로 설정하지 않을 경우 `azdata`를 처음 사용할 때 `--accept-eula=yes`를 포함할 수 있습니다.|
| `DOCKER_USERNAME` | 옵션 | 프라이빗 리포지토리에 저장된 컨테이너 이미지에 액세스하는 데 사용할 사용자 이름입니다. 빅 데이터 클러스터 배포에서 프라이빗 Docker 리포지토리를 사용하는 방법에 대한 자세한 내용은 [오프라인 배포](deploy-offline.md) 항목을 참조하세요.|
| `DOCKER_PASSWORD` | 옵션 |위 프라이빗 리포지토리에 액세스하는 데 사용할 암호입니다. |

`azdata bdc create`를 호출하기 전에 이러한 환경 변수를 설정해야 합니다. 변수를 설정하지 않으면 변수를 입력하라는 메시지가 표시됩니다.

다음 예제에서는 Linux(bash) 및 Windows(PowerShell)의 환경 변수를 설정하는 방법을 보여 줍니다.

```bash
export AZDATA_USERNAME=admin
export AZDATA_PASSWORD=<password>
export ACCEPT_EULA=yes
```

```PowerShell
SET AZDATA_USERNAME=admin
SET AZDATA_PASSWORD=<password>
```

> [!NOTE]
> 위의 암호를 사용하여 Knox 게이트웨이에 `root` 사용자를 사용해야 합니다. `root`는 이 기본 인증(사용자 이름/암호)에서 유일하게 지원되는 사용자입니다.
> 기본 인증을 사용하여 SQL Server에 연결하려면 AZDATA_USERNAME 및 AZDATA_PASSWORD [환경 변수](#env)와 동일한 값을 사용합니다. 


환경 변수를 설정한 후에는 `azdata bdc create`를 실행하여 배포를 트리거해야 합니다. 이 예제에서는 위에서 만든 클러스터 구성 프로필을 사용합니다.

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

다음 지침에 유의하세요.

- 특수 문자를 포함하는 경우 암호를 큰따옴표로 묶어야 합니다. `AZDATA_PASSWORD`를 원하는 대로 설정할 수 있지만, 암호가 충분히 복잡해야 하며 `!`, `&` 또는 `'` 문자를 사용하지 않도록 주의해야 합니다. 큰따옴표 구분 기호는 bash 명령에서만 작동합니다.
- `AZDATA_USERNAME` 로그인은 설치 중에 생성되는 SQL Server 마스터 인스턴스의 시스템 관리자입니다. SQL Server 컨테이너를 만든 후 컨테이너에서 `echo $AZDATA_PASSWORD`를 실행하여 지정한 `AZDATA_PASSWORD` 환경 변수를 검색할 수 있습니다. 보안을 위해 암호를 변경하는 것이 좋습니다.

## <a name="unattended-install"></a><a id="unattended"></a> 무인 설치

무인 배포의 경우 모든 필수 환경 변수를 설정하고 구성 파일을 사용한 다음, `--accept-eula yes` 매개 변수를 사용하여 `azdata bdc create` 명령을 호출해야 합니다. 이전 섹션의 예제에서는 무인 설치 구문을 보여 줍니다.

## <a name="monitor-the-deployment"></a><a id="monitor"></a> 배포 모니터링

클러스터 부트스트랩 중에 클라이언트 명령 창에 배포 상태가 반환됩니다. 배포 프로세스 중에 컨트롤러 Pod를 대기 중이라는 일련의 메시지가 표시됩니다.

```output
Waiting for cluster controller to start.
```

15~30분 후에 컨트롤러 Pod가 실행되고 있다는 알림을 받습니다.

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> 빅 데이터 클러스터 구성 요소의 컨테이너 이미지를 다운로드하는 데 필요한 시간 때문에 전체 배포는 시간이 오래 걸릴 수 있습니다. 그러나 몇 시간이 걸리면 안 됩니다. 배포에 문제가 있는 경우 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 모니터링 및 문제 해결](cluster-troubleshooting-commands.md)을 참조하세요.

배포가 완료되면 출력에 성공 알림이 표시됩니다.

```output
Cluster deployed successfully.
```

> [!TIP]
> 사용자 지정 구성에서 수정되지 않은 경우 배포된 빅 데이터 클러스터의 기본 이름은 `mssql-cluster`입니다.

## <a name="retrieve-endpoints"></a><a id="endpoints"></a> 엔드포인트 검색

배포 스크립트가 성공적으로 완료되면 다음 단계에 따라 빅 데이터 클러스터의 외부 엔드포인트 주소를 가져올 수 있습니다.

1. 배포 후에 배포 표준 출력에서 또는 다음 `kubectl` 명령의 EXTERNAL-IP 출력을 통해 컨트롤러 엔드포인트의 IP 주소를 찾습니다.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 배포 중에 기본 이름을 변경하지 않은 경우에는 위 명령에서 `-n mssql-cluster`를 사용합니다. `mssql-cluster`는 빅 데이터 클러스터의 기본 이름입니다.

1. [azdata login](reference-azdata.md)을 사용하여 빅 데이터 클러스터에 로그인합니다. `--endpoint` 매개 변수를 컨트롤러 엔드포인트의 외부 IP 주소로 설정합니다.

   ```bash
   azdata login --endpoint https://<ip-address-of-controller-svc-external>:30080 --username <user-name>
   ```

   배포 중에 빅 데이터 클러스터 관리자에 대해 구성한 사용자 이름 및 암호(AZDATA_USERNAME 및 AZDATA_PASSWORD)를 지정합니다.

   > [!TIP]
   > Kubernetes 클러스터 관리자이고 클러스터 구성 파일(kube config 파일)에 액세스할 수 있는 경우 대상 Kubernetes 클러스터를 가리키도록 현재 컨텍스트를 구성할 수 있습니다. 이 경우 `azdata login -n <namespaceName>`를 사용하여 로그인 할 수 있으며, 여기서 `namespace`는 빅 데이터 클러스터 이름입니다. 로그인 명령 내에서 지정하지 않으면 자격 증명을 입력하라는 메시지가 표시됩니다.
   
1. [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md)를 실행하여 각 엔드포인트에 대한 설명과 해당 IP 주소 및 포트 값이 포함된 목록을 가져옵니다. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   다음 목록은 이 명령의 샘플 출력을 보여 줍니다.

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

다음 `kubectl` 명령을 실행하여 클러스터에 대해 배포된 서비스 엔드포인트를 모두 가져올 수도 있습니다.

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

## <a name="verify-the-cluster-status"></a><a id="status"></a> 클러스터 상태 확인

배포 후에 [azdata bdc status show](reference-azdata-bdc-status.md) 명령을 사용하여 클러스터 상태를 확인할 수 있습니다.

```bash
azdata bdc status show
```

> [!TIP]
> 상태 명령을 실행하려면 먼저 이전 엔드포인트 섹션에 표시된 `azdata login` 명령을 사용하여 로그인해야 합니다.

다음은 이 명령의 샘플 출력을 보여 줍니다.

```output
Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 sql            ready    healthy         -
 hdfs           ready    healthy         -
 spark          ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Sql Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Hdfs Services: ready                                                                                                                                                                                                Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 nmnode-0        ready    healthy         StatefulSet nmnode-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         -
 control         ready    healthy         -
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

다음 명령을 사용하여 자세한 상태를 가져올 수도 있습니다.

- [azdata bdc control status show](reference-azdata-bdc-control-status.md)는 컨트롤 관리 서비스와 연결된 모든 구성 요소의 상태를 반환합니다.
```
azdata bdc control status show
```
샘플 출력:
```output
Control: ready                                                                                                                                                                                                      Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         -
 control         ready    healthy         -
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
```

- `azdata bdc sql status show`는 SQL Server 서비스가 있는 모든 리소스의 상태를 반환합니다.
```
azdata bdc sql status show
```
샘플 출력:
```output
Sql: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
```

> [!IMPORTANT]
> `--all` 매개 변수를 사용하는 경우 이러한 명령의 출력에는 자세한 분석을 위한 Kibana 및 Grafana 대시보드의 URL이 포함되어 있습니다.

`azdata` 외에도 Azure Data Studio를 사용하여 엔드포인트 및 상태 정보를 모두 확인할 수 있습니다. `azdata` 및 Azure Data Studio를 사용하여 클러스터 상태를 보는 방법에 대한 자세한 내용은 [빅 데이터 클러스터의 상태를 보는 방법](view-cluster-status.md)을 참조하세요.

## <a name="connect-to-the-cluster"></a><a id="connect"></a> 클러스터에 연결

빅 데이터 클러스터에 연결하는 방법에 대한 자세한 내용은 [Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [빅 데이터 클러스터의 배포 설정 구성](deployment-custom-configuration.md)
- [SQL Server 빅 데이터 클러스터의 오프라인 배포 수행](deploy-offline.md)
- [워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
