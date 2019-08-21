---
title: azdata를 사용하여 애플리케이션 배포
titleSuffix: SQL Server big data clusters
description: Python 또는 R 스크립트를의 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]응용 프로그램으로 배포 합니다.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 18e97a3567b50982bd2be11dcc3493951dfe8fa9
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653150"
---
# <a name="how-to-deploy-an-app-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>앱을 배포 하는 방법[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 2019 빅 데이터 클러스터 내에서 R 및 Python 스크립트를 응용 프로그램으로 배포 하 고 관리 하는 방법을 설명 합니다.

## <a name="whats-new-and-improved"></a>새로운 기능 및 향상된 기능

- 클러스터와 앱을 관리하기 위한 단일 명령줄 유틸리티
- 사양 파일을 통해 세부적인 제어 기능을 제공하는 동시에 간소화된 앱 배포
- 추가 응용 프로그램 형식 호스팅 지원-SSIS 및 MLeap (CTP 2.3의 새로운 기능)
- 응용 프로그램 배포를 관리 하기 위한 [확장을 Visual Studio Code](app-deployment-extension.md) 합니다.

애플리케이션은 `azdata` 명령줄 유틸리티를 사용하여 배포 및 관리합니다. 이 문서에서는 명령줄에서 앱을 배포하는 방법의 예제를 제공합니다. 에서이를 사용 하는 방법에 대 한 자세한 내용은 [Visual Studio Code 확장](app-deployment-extension.md)을 참조 Visual Studio Code.

지원되는 앱 유형은 다음과 같습니다.
- R 및 Python 앱 (함수, 모델 및 앱)
- MLeap Serving
- SSIS(SQL Server Integration Services)

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [azdata 명령줄 유틸리티](deploy-install-azdata.md)

## <a name="capabilities"></a>Capabilities

SQL Server 2019(미리 보기)에서 애플리케이션을 만들고, 삭제, 설명, 초기화, 나열, 실행 및 업데이트할 수 있습니다. 다음 표에서는 **azdata**와 함께 사용할 수 있는 애플리케이션 배포 명령을 설명합니다.

|명령 |설명 |
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

## <a name="aks"></a>AKS

AKS를 사용하는 경우 bash 또는 cmd 창에서 다음 명령을 실행하여 `controller-svc-external` 서비스의 IP 주소를 가져와야 합니다.


```bash
kubectl get svc controller-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm 또는 Minikube

Kubeadm 또는 Minikube를 사용 하는 경우 다음 명령을 실행 하 여 클러스터에 로그인 하는 데 사용할 IP 주소를 가져옵니다.

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>앱 만들기

애플리케이션을 만들려면 `app create` 명령과 함께 `azdata`를 사용합니다. 이 파일은 앱을 만들 때 사용한 머신에 로컬로 상주합니다.

다음 구문을 사용하여 빅 데이터 클러스터에 새 앱을 만듭니다.

```bash
azdata app create --spec <directory containing spec file>
```

다음 명령은 이 명령이 표시되는 모양의 예를 보여 줍니다.

```bash
azdata app create --spec ./addpy
```

이 명령은 애플리케이션이 `addpy` 폴더에 저장되어 있다고 가정합니다. 이 폴더에는 `spec.yaml`이라는 애플리케이션 사양 파일도 들어 있어야 합니다. `spec.yaml` 파일에 대 한 자세한 내용은 [응용 프로그램 배포 페이지를](concept-application-deployment.md) 참조 하세요.

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

## <a name="run-an-app"></a>앱 실행

앱이 `Ready` 상태이면 지정된 입력 매개 변수와 함께 실행하여 앱을 사용할 수 있습니다. 다음 구문을 사용하여 앱을 실행합니다.

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

다음 예제 명령은 run 명령을 보여 줍니다.

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

실행이 성공적으로 완료되면 앱을 만들 때 지정한 대로 출력됩니다. 다음은 예제입니다.

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```

## <a name="create-an-app-skeleton"></a>앱 구조 만들기

init 명령은 앱을 배포하는 데 필요한 관련 아티팩트와 함께 스캐폴드를 제공합니다. 아래 예제에서는 다음 명령을 실행하여 이 작업을 수행할 수 있는 hello를 만듭니다.

```bash
azdata app init --name hello --version v1 --template python
```

이렇게 하면 hello라는 폴더가 만들어집니다.  디렉터리로 `cd`하고 폴더에 생성된 파일을 검사할 수 있습니다. 사양. yaml은 이름, 버전 및 소스 코드와 같은 앱을 정의 합니다. 사양을 편집 하 여 이름, 버전, 입력 및 출력을 변경할 수 있습니다.

다음은 폴더에 표시되는 init 명령의 샘플 출력입니다.

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>앱 설명

describe 명령은 클러스터의 엔드포인트를 포함하여 앱에 대한 자세한 정보를 제공합니다. 이 정보는 일반적으로 앱 개발자가 Swagger 클라이언트 및 RESTful 방식으로 앱과 상호 작용하는 웹 서비스를 사용하여 앱을 빌드하는 데 사용됩니다. 자세한 내용은 [빅 데이터 클러스터에서 애플리케이션 사용](big-data-cluster-consume-apps.md)을 참조하세요.

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30080/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30080/api/app/add-app/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

## <a name="delete-an-app"></a>앱 삭제

빅 데이터 클러스터에서 앱을 삭제하려면 다음 구문을 사용합니다.

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>다음 단계

자세한 내용은 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] [빅 데이터 클러스터에서 응용 프로그램 사용](big-data-cluster-consume-apps.md) 에서 응용 프로그램에 배포 된 앱을 통합 하는 방법을 알아봅니다. [앱 배포 샘플](https://aka.ms/sql-app-deploy)에서 추가 샘플을 확인할 수도 있습니다.

에 대 한 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]자세한 내용은 [무엇 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]인가요?](big-data-cluster-overview.md)를 참조 하세요.
