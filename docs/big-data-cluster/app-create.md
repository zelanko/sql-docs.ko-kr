---
title: azdata를 사용하여 애플리케이션 배포
titleSuffix: SQL Server Big Data Clusters
description: Python 또는 R 스크립트를 SQL Server 2019 빅 데이터 클러스터에 애플리케이션으로 배포합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8e91315b5ec79c136b4d84a7fbc36a707cc3d82f
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257313"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터에 앱을 배포하는 방법

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

SQL Server BDC(빅 데이터 클러스터)에 배포된 애플리케이션은 클러스터의 계산 기능과 같은 많은 이점을 얻을 수 있을 뿐만 아니라 클러스터에서 사용할 수 있는 대규모 데이터에도 액세스할 수 있습니다. 앱이 데이터와 동일한 클러스터에 상주하므로 성능이 크게 향상됩니다.

이 문서에서는 SQL Server 빅 데이터 클러스터 내의 애플리케이션으로 R 및 Python 스크립트를 배포하고 관리하는 방법을 설명합니다.

## <a name="whats-new-and-improved"></a>새로운 기능 및 향상된 기능

- 클러스터와 앱을 관리하기 위한 단일 명령줄 유틸리티
- 사양 파일을 통해 세부적인 제어 기능을 제공하는 동시에 간소화된 앱 배포
- 추가 애플리케이션 유형, 즉 SSIS(SQL Server Integration Services) 및 MLeap 호스팅을 지원합니다.
- 애플리케이션 배포를 관리하기 위한 [Visual Studio Code 확장](app-deployment-extension.md).

애플리케이션은 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]를 사용하여 배포되고 관리됩니다. 이 문서에서는 명령줄에서 앱을 배포하는 방법의 예제를 제공합니다. Visual Studio Code에서 이를 사용하는 방법에 대해 알아보려면 [Visual Studio Code 확장](app-deployment-extension.md)을 참조하세요.

지원되는 앱 유형은 다음과 같습니다.

- **Python** - 데이터 엔지니어, 데이터 과학자 또는 DevOps 엔지니어와 같은 다양한 사용자에게 가장 널리 사용되는 일반 프로그래밍 언어 중 하나로, 데이터 랭글링, 자동화, 프로토타입 생성 등 다양한 시나리오를 지원하며, 다양한 비즈니스 요구 사항을 해결하기 위해 Flask 및 Django와 같은 웹 개발 프레임워크와 함께 작동하는 엔터프라이즈급 애플리케이션을 프로그래밍하는 데도 사용됩니다.  
- **R** – 데이터 엔지니어링 및 데이터 과학자를 위한 또 하나의 인기 있는 프로그래밍 언어입니다. Python과 비교하여 R은 통계 계산 및 그래픽에 보다 치중한 프로그래밍 언어입니다.  
- **SSIS(SQL Server Integration Services)** - ETL 패키지를 빌드하고 디버그하기 위한 고성능 데이터 통합 솔루션으로, 데이터베이스 간 데이터 마이그레이션 및 외부 데이터 원본 통합을 처리하기 위한 지침을 저장하는 XML 기반 파일 형식인 DTSX(Data Transformation Services Package File Format)를 사용합니다.   
- **MLeap** - 일반적인 직렬화 형식으로, SparkML 파이프라인 및 기타 파이프라인을 실행하고 직렬화하는 데 필요한 모든 항목을 제공하며 런타임에 로드되어 ML 채점 작업을 데이터에 근접하여 거의 실시간으로 처리할 수 있습니다.  

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>기능

SQL Server 2019에서 애플리케이션을 만들고, 삭제, 설명, 초기화, 나열, 실행 및 업데이트할 수 있습니다. 다음 표에서는 **azdata** 와 함께 사용할 수 있는 애플리케이션 배포 명령을 설명합니다.

|명령 |Description |
|:---|:---|
|`azdata login` | SQL Server 빅 데이터 클러스터에 로그인합니다. |
|`azdata app create` | 애플리케이션을 만듭니다. |
|`azdata app delete` | 애플리케이션을 삭제합니다. |
|`azdata app describe` | 애플리케이션을 설명합니다. |
|`azdata app init` | 새 애플리케이션 구조를 시작합니다. |
|`azdata app list` | 애플리케이션을 나열합니다. |
|`azdata app run` | 애플리케이션을 실행합니다. |
|`azdata app update`| 애플리케이션을 업데이트합니다. |

다음 예제와 같이 `--help` 매개 변수를 사용하여 도움말을 볼 수 있습니다.

```bash
azdata app create --help
```

다음 섹션에서는 이러한 명령을 자세히 설명합니다.

## <a name="sign-in"></a>로그인

애플리케이션을 배포하거나 조작하기 전에 먼저 `azdata login` 명령을 사용하여 SQL Server 빅 데이터 클러스터에 로그인합니다. 클러스터에 대한 사용자 이름 및 암호와 함께 `controller-svc-external` 서비스의 외부 IP 주소(예: `https://ip-address:30080`)를 지정합니다.

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="azure-kubernetes-service-aks"></a>AKS(Azure Kubernetes Service)

AKS를 사용하는 경우 bash 또는 cmd 창에서 다음 명령을 실행하여 `controller-svc-external` 서비스의 IP 주소를 가져와야 합니다.


```bash
kubectl get svc controller-svc-external -n <name of your big data cluster>
```

## <a name="kubernetes-clusters-created-with-kubeadm"></a>Kubeadm으로 만든 Kubernetes 클러스터

다음 명령을 실행하여 클러스터에 로그인할 IP 주소를 가져옵니다.

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app-skeleton"></a>앱 구조 만들기

**azdata app init** 명령은 앱을 배포하는 데 필요한 관련 아티팩트와 함께 스캐폴드를 제공합니다. 아래 예제에서는 다음 명령을 실행하여 이 작업을 수행할 수 있는 add-app을 만듭니다.

```bash
azdata app init --name add-app --version v1 --template python
```

이렇게 하면 hello라는 폴더가 만들어집니다.  `cd` 명령을 사용하여 디렉터리를 전환하고 폴더에 생성된 파일을 검사할 수 있습니다. spec.yaml은 이름, 버전 및 소스 코드와 같은 앱을 정의합니다. 사양을 편집하여 이름, 버전, 입력 및 출력을 변경할 수 있습니다.

다음은 폴더에 표시되는 init 명령의 샘플 출력입니다.

```
add-app.py
run-spec.yaml
spec.yaml
```

## <a name="create-an-app"></a>앱 만들기

애플리케이션을 만들려면 `app create` 명령과 함께 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]를 사용합니다. 이 파일은 앱을 만들 때 사용한 머신에 로컬로 상주합니다.

다음 구문을 사용하여 빅 데이터 클러스터에 새 앱을 만듭니다.

```bash
azdata app create --spec <directory containing spec file>
```

다음 명령은 이 명령이 표시되는 모양의 예를 보여 줍니다.

```bash
azdata app create --spec ./addpy
```

이 명령은 애플리케이션이 `addpy` 폴더에 저장되어 있다고 가정합니다. 이 폴더에는 `spec.yaml`이라는 애플리케이션 사양 파일도 들어 있어야 합니다. 자세한 내용은 `spec.yaml` 파일에서 [애플리케이션 배포 페이지](concept-application-deployment.md)를 참조하세요.

이 샘플 앱을 배포하려면 `addpy`라는 디렉터리에 다음 파일을 만듭니다.

- `add.py`. 다음 Python 코드를 이 파일에 복사합니다.
   ```py
   #add.py
  def add(x, y):
    result = x+y
    return result
  result=add(x,y)
   ```
- `spec.yaml`. 다음 코드를 이 파일에 복사합니다.
   ```yaml
   #spec.yaml
   name: add-app #name of your python script
   version: v1  #version of the app
   runtime: Python #the language this app uses (R or Python)
   src: ./add.py #full path to the location of the app
   entrypoint: add #the function that will be called upon execution
   replicas: 1  #number of replicas needed
   poolsize: 1  #the pool size that you need your app to scale
   inputs:  #input parameters that the app expects and the type
     x: int
     y: int
   output: #output parameter the app expects and the type
     result: int
   ```

그런 다음, 아래 명령을 실행합니다.

```bash
azdata app create --spec ./addpy
```

list 명령을 사용하여 앱이 배포되었는지 확인할 수 있습니다.

```bash
azdata app list
```

배포가 완료되지 않은 경우 다음 예제와 같이 `state`가 `WaitingforCreate`로 표시됩니다.

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

배포가 성공적으로 완료되면 `state`가 `Ready` 상태로 바뀝니다.

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>앱 나열

`app list` 명령을 사용하여 성공적으로 생성된 앱을 모두 나열할 수 있습니다.

다음 명령은 빅 데이터 클러스터에서 사용 가능한 애플리케이션을 모두 나열합니다.

```bash
azdata app list
```

이름 및 버전을 지정하면 특정 앱과 해당 상태(Creating 또는 Ready)가 나열됩니다.

```bash
azdata app list --name <app_name> --version <app_version>
```

다음 예제에서는 이 명령을 보여 줍니다.

```bash
azdata app list --name add-app --version v1
```

다음 예제와 비슷한 내용이 출력됩니다.

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="delete-an-app"></a>앱 삭제

빅 데이터 클러스터에서 앱을 삭제하려면 다음 구문을 사용합니다.

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 배포된 앱을 자체 애플리케이션에 통합하는 방법을 살펴봅니다. 자세한 내용은 [빅 데이터 클러스터에서 애플리케이션 실행](app-run.md) 및 [빅 데이터 클러스터에서 애플리케이션 사용](app-consume.md)을 참조하세요. [앱 배포 샘플](https://aka.ms/sql-app-deploy)에서 추가 샘플을 확인할 수도 있습니다.

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.