---
title: Azdata를 사용 하 여 응용 프로그램 배포
titleSuffix: SQL Server big data clusters
description: Python 또는 R 스크립트를 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 응용 프로그램으로 배포 합니다.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 06b76e7eb8eec8db1993ca558a1f57355457c4ad
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419488"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-cluster-preview"></a>빅 데이터 클러스터 SQL Server에 앱을 배포 하는 방법 (미리 보기)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 내의 응용 프로그램으로 R 및 Python 스크립트를 배포 하 고 관리 하는 방법을 설명 합니다.

## <a name="whats-new-and-improved"></a>새로운 기능 및 향상 된 기능

- 클러스터와 앱을 관리 하는 단일 명령줄 유틸리티입니다.
- 사양 파일을 통해 세부적인 제어를 제공 하는 동시에 앱 배포를 간소화 합니다.
- 추가 응용 프로그램 형식 호스팅 지원-SSIS 및 MLeap (CTP 2.3의 새로운 기능)
- 응용 프로그램 배포를 관리 하기 위한 [VS Code 확장](app-deployment-extension.md)

응용 프로그램은 명령줄 유틸리티를 `azdata` 사용 하 여 배포 및 관리 됩니다. 이 문서는 명령줄에서 앱을 배포 하는 방법에 대 한 예제를 제공 합니다. 에서이를 사용 하는 방법에 대 한 자세한 내용은 [VS Code 확장](app-deployment-extension.md)을 참조 Visual Studio Code.

지원 되는 앱 유형은 다음과 같습니다.
- R 및 Python 앱 (함수, 모델 및 앱)
- MLeap 서비스
- SSIS(SQL Server Integration Services)

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [azdata 명령줄 유틸리티](deploy-install-azdata.md)

## <a name="capabilities"></a>Capabilities

SQL Server 2019 (미리 보기)에서 응용 프로그램을 만들고, 삭제 하 고, 설명 하 고, 초기화 하 고, 실행 하 고, 업데이트할 수 있습니다. 다음 표에서는 **azdata**와 함께 사용할 수 있는 응용 프로그램 배포 명령을 설명 합니다.

|Command |설명 |
|:---|:---|
|`azdata login` | SQL Server 빅 데이터 클러스터에 로그인 |
|`azdata app create` | 응용 프로그램을 만듭니다. |
|`azdata app delete` | 응용 프로그램을 삭제 합니다. |
|`azdata app describe` | 응용 프로그램을 설명 합니다. |
|`azdata app init` | 새 응용 프로그램 구조를 Kickstart. |
|`azdata app list` | 응용 프로그램을 나열 합니다. |
|`azdata app run` | 응용 프로그램을 실행 합니다. |
|`azdata app update`| 응용 프로그램을 업데이트 합니다. |

다음 예제와 같이 `--help` 매개 변수를 사용 하 여 도움을 받을 수 있습니다.

```bash
azdata app create --help
```

다음 섹션에서는 이러한 명령에 대해 자세히 설명 합니다.

## <a name="sign-in"></a>로그인

응용 프로그램을 배포 하거나 응용 프로그램을 조작 하기 전에 먼저 `azdata login` 명령을 사용 하 여 SQL Server 빅 데이터 클러스터에 로그인 합니다. 클러스터에 대 한 사용자 이름 및 `controller-svc-external` 암호와 함께 서비스의 `https://ip-address:30080`외부 IP 주소 (예:)를 지정 합니다.

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

AKS를 사용 하는 경우 bash 또는 cmd 창에서이 명령을 실행 하 여 `mgmtproxy-svc-external` 서비스의 IP 주소를 가져오려면 다음 명령을 실행 해야 합니다.


```bash
kubectl get svc mgmtproxy-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm 또는 Minikube

Kubeadm 또는 Minikube를 사용 하는 경우 다음 명령을 실행 하 여 클러스터에 로그인 하는 데 사용할 IP 주소를 가져옵니다.

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>앱 만들기

응용 프로그램을 만들려면 `azdata` `app create` 명령과 함께를 사용 합니다. 이러한 파일은 앱을 만들 컴퓨터에 로컬로 상주 합니다.

다음 구문을 사용 하 여 빅 데이터 클러스터에 새 앱을 만듭니다.

```bash
azdata app create --spec <directory containing spec file>
```

다음 명령은이 명령의 예를 보여 줍니다.

```bash
azdata app create --spec ./addpy
```

여기서는 응용 프로그램이 `addpy` 폴더에 저장 되어 있다고 가정 합니다. 이 폴더에는 이라는 `spec.yaml`응용 프로그램에 대 한 사양 파일도 포함 되어야 합니다. `spec.yaml` 파일에 대 한 자세한 내용은 [응용 프로그램 배포 페이지를](concept-application-deployment.md) 참조 하세요.

이 앱 샘플 앱을 배포 하려면 라는 `addpy`디렉터리에 다음 파일을 만듭니다.

- `add.py`항목을 참조하세요. 다음 Python 코드를이 파일에 복사 합니다.
   ```py
   #add.py
   def add(x,y):
        result = x+y
        return result
    result=add(x,y)
   ```
- `spec.yaml`. 다음 코드를이 파일에 복사 합니다.
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

그런 다음 아래 명령을 실행 합니다.

```bash
azdata app create --spec ./addpy
```

List 명령을 사용 하 여 앱을 배포할지 여부를 확인할 수 있습니다.

```bash
azdata app list
```

배포가 완료 되지 않은 경우 다음 예제와 같이 `state` 표시 `WaitingforCreate` 됩니다.

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

배포가 성공적으로 완료 되 면 `state` `Ready` 상태가 다음과 같이 변경 됩니다.

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

`app list` 명령을 사용 하 여 성공적으로 생성 된 모든 앱을 나열할 수 있습니다.

다음 명령을 사용 하 여 빅 데이터 클러스터에서 사용 가능한 모든 응용 프로그램을 나열 합니다.

```bash
azdata app list
```

이름 및 버전을 지정 하면 특정 앱 및 해당 상태 (만들기 또는 준비)가 나열 됩니다.

```bash
azdata app list --name <app_name> --version <app_version>
```

다음 예제에서는이 명령을 보여 줍니다.

```bash
azdata app list --name add-app --version v1
```

다음 예제와 유사한 출력이 표시 됩니다.

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

앱이 `Ready` 상태 이면 지정 된 입력 매개 변수를 사용 하 여 앱을 실행할 수 있습니다. 앱을 실행 하려면 다음 구문을 사용 합니다.

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

다음 예제 명령은 run 명령을 보여 줍니다.

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

실행에 성공 하면 앱을 만들 때 지정한 대로 출력이 표시 됩니다. 다음은 예제입니다.

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

Init 명령은 앱을 배포 하는 데 필요한 관련 아티팩트와 함께 스 캐 폴드를 제공 합니다. 아래 예제에서는 다음 명령을 실행 하 여이 작업을 수행할 수 있는 hello를 만듭니다.

```bash
azdata app init --name hello --version v1 --template python
```

이렇게 하면 hello 라는 폴더가 만들어집니다.  디렉터리에 `cd` 대 한 파일을 만들고 폴더에 생성 된 파일을 검사할 수 있습니다. 사양. yaml은 이름, 버전 및 소스 코드와 같은 앱을 정의 합니다. 사양을 편집 하 여 이름, 버전, 입력 및 출력을 변경할 수 있습니다.

다음은 폴더에 표시 되는 init 명령의 샘플 출력입니다.

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>앱 설명

설명 명령은 클러스터의 끝점을 포함 하 여 앱에 대 한 자세한 정보를 제공 합니다. 이는 일반적으로 앱 개발자가 swagger 클라이언트를 사용 하 여 앱을 빌드하고 RESTful 방식으로 앱과 상호 작용 하는 웹 서비스를 사용 하는 데 사용 됩니다. 자세한 내용은 [빅 데이터 클러스터에서 응용 프로그램 사용](big-data-cluster-consume-apps.md) 을 참조 하세요.

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
    "app": "https://10.1.1.3:30777/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30777/api/app/add-app/v1/swagger.json"
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

빅 데이터 클러스터에서 앱을 삭제 하려면 다음 구문을 사용 합니다.

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>다음 단계

[빅 데이터 클러스터에서 응용 프로그램을 사용](big-data-cluster-consume-apps.md) 하는 방법에 대 한 자세한 내용은 응용 프로그램에서 SQL Server 빅 데이터 클러스터에 배포 된 앱을 통합 하는 방법을 알아봅니다. [앱 배포 샘플](https://aka.ms/sql-app-deploy)에서 추가 샘플을 확인할 수도 있습니다.

빅 데이터 클러스터 SQL Server 하는 방법에 대 한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터 란?](big-data-cluster-overview.md)을 참조 하세요.
