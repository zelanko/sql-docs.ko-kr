---
title: Mssqlctl를 사용 하 여 응용 프로그램 배포
titleSuffix: SQL Server 2019 big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 응용 프로그램으로 Python 또는 R 스크립트를 배포 합니다.
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 83dc07ed6336c637aaf17fdcfc1075854fe542b7
ms.sourcegitcommit: d765563ccd03f299544bac233bc35f9b1df3fd47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58434434"
---
# <a name="how-to-deploy-an-app-on-sql-server-2019-big-data-cluster-preview"></a>SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 앱을 배포 하는 방법

이 문서에서는 배포 및 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 내에서 응용 프로그램으로 R 및 Python 스크립트를 관리 하는 방법을 설명 합니다.

## <a name="whats-new-and-improved"></a>새로운 기능 및 향상

- 클러스터 및 앱을 관리 하는 단일 명령줄 유틸리티입니다.
- 사양 파일을 통해 세분화 된 제어 기능을 제공 하는 동안 앱 배포를 간소화 합니다.
- SSIS 및 MLeap (CTP 2.3)에 새로 추가 응용 프로그램 형식 호스팅을 지원합니다
- [VS Code 확장](app-deployment-extension.md) 응용 프로그램 배포를 관리 하려면

응용 프로그램 배포 및 관리를 사용 하 여 `mssqlctl` 명령줄 유틸리티입니다. 이 문서에서는 명령줄에서 앱을 배포 하는 방법의 예제를 제공 합니다. 참조 Visual Studio Code에서이 사용 하는 방법을 알아보려면 [VS Code 확장](app-deployment-extension.md)합니다.

다음과 같은 유형의 앱 지원 됩니다.
- R 및 Python 앱 (함수, 모델 및 앱)
- MLeap 처리
- SSIS(SQL Server Integration Services)

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [mssqlctl 명령줄 유틸리티](deploy-install-mssqlctl.md)

## <a name="capabilities"></a>Capabilities

SQL Server 2019 (미리 보기) CTP 2.3 만들기, 삭제, 설명, 초기화할 수 있습니다, 목록을 실행 하 고 응용 프로그램을 업데이트 합니다. 다음 표에서 사용할 수 있는 응용 프로그램 배포 명령을 **mssqlctl**합니다.

|Command |Description |
|:---|:---|
|`mssqlctl login` | SQL Server 빅 데이터 클러스터에 로그인 |
|`mssqlctl app create` | 응용 프로그램을 만듭니다. |
|`mssqlctl app delete` | 응용 프로그램을 삭제 합니다. |
|`mssqlctl app describe` | 응용 프로그램에 설명 합니다. |
|`mssqlctl app init` | Kickstart 새 응용 프로그램 구조입니다. |
|`mssqlctl app list` | 응용 프로그램을 나열 합니다. |
|`mssqlctl app run` | 응용 프로그램을 실행 합니다. |
|`mssqlctl app update`| 응용 프로그램을 업데이트 합니다. |

사용 하 여 도움말을 볼 수는 `--help` 다음 예제와 같이 매개 변수:

```bash
mssqlctl app create --help
```

다음 섹션에서는 이러한 명령을 자세히 설명합니다.

## <a name="log-in"></a>로그인

배포 하거나 응용 프로그램과 상호 작용 하기 전에 먼저 로그인을 사용 하 여 빅 데이터 클러스터 SQL Server는 `mssqlctl login` 명령입니다. 외부 IP 주소를 지정 합니다 `endpoint-service-proxy` 서비스 (예: `https://ip-address:30777`) 사용자 이름 및 클러스터에는 암호와 함께 합니다.

```bash
mssqlctl login -e https://<ip-address-of-endpoint-service-proxy>:30777 -u <user-name> -p <password>
```

## <a name="aks"></a>AKS

AKS를 사용 하는 경우의 IP 주소를 가져오려면 다음 명령을 실행 하 여 `endpoint-service-proxy` bash 또는 cmd 창에서이 명령을 실행 하 여 서비스:


```bash
kubectl get svc endpoint-service-proxy -n <name of your cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm 하거나 Minikube

클러스터에 대 한 로그인에 IP 주소를 가져오려면 Kubeadm 또는 다음 명령을 실행 하는 Minikube를 사용 중인 경우

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>앱 만들기

사용할 응용 프로그램을 만들려면 `mssqlctl` 사용 하 여는 `app create` 명령입니다. 이러한 파일에서 앱을 만들려는 컴퓨터에 로컬로 상주 합니다.

빅 데이터 클러스터에 새 앱을 만들려면 다음 구문을 사용 합니다.

```bash
mssqlctl app create -n <app_name> -v <version_number> --spec <directory containing spec file>
```

다음 명령은이 명령은 같습니다는 항목의 예를 보여줍니다.

이라는 파일이 있다고 가정 `spec.yaml` 내에서 `addpy` 폴더입니다.
`addpy` 폴더에는 `add.py` 및 `spec.yaml` 는 `spec.yaml` 은 사양 파일에 대 한는 `add.py` 앱.


`add.py` 다음 python 앱을 만듭니다.

```py
#add.py
def add(x,y):
        result = x+y
        return result
result=add(x,y)
```

다음 스크립트는 샘플에 대 한 내용의 `spec.yaml`:

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

이 사용 하려면 위 코드 줄을 디렉터리에 두 개의 파일 복사 `addpy` 으로 `add.py` 및 `spec.yaml` 아래 명령을 실행 합니다.

```bash
mssqlctl app create --spec ./addpy
```

> [!NOTE]
> `spec.yaml` 파일 둘 다 지정 된 `poolsize` 및 다양 한 `replicas`. 수가 `replicas` 배포 해야 하는 서비스의 복사본 수를 지정 합니다. `poolsize` 복제본 당 만들려는 풀 수를 지정 합니다. 이러한 설정을 배포 병렬로 처리할 수 있는 요청 양을 영향을 줍니다. 특정된 한 번에 요청의 최대 수는과 동일한 `replicas` 번 `poolsize`, 즉 5 개의 복제본 및 복제본 당 2 개의 풀에 있는 경우 배포에 10 개의 요청을 병렬로 처리할 수 있습니다. 그래픽 표현 아래 이미지를 참조 하세요 `replicas` 고 `poolsize`: ![Poolsize 및 복제본](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

명령 목록을 사용 하 여 앱이 배포를 확인할 수 있습니다.

```bash
mssqlctl app list
```

배포 불완전 한 경우 표시 되어야 합니다 `state` 표시 `WaitingforCreate` 다음 예제와 같이:

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

배포에 성공한 후 표시 되어야 합니다 `state` 변경 `Ready` 상태:

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>앱 목록

성공적으로 사용 하 여 만든 모든 앱을 표시 하는 `app list` 명령입니다.

다음 명령은 빅 데이터 클러스터에 사용 가능한 모든 응용 프로그램을 나열합니다.

```bash
mssqlctl app list
```

이름 및 버전을 지정 하면 해당 특정 앱 및 (만드는 중 또는 준비) 상태를 나열 합니다.

```bash
mssqlctl app list --name <app_name> --version <app_version>
```

다음 예제에서는이 명령을 보여 줍니다.

```bash
mssqlctl app list --name add-app --version v1
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

앱의 경우는 `Ready` 상태 지정된 하는 입력된 매개 변수를 사용 하 여 실행 하 여 사용할 수 있습니다. 앱을 실행 하려면 다음 구문을 사용 합니다.

```bash
mssqlctl app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

다음 예제 명령은 실행된 명령을 보여 줍니다.

```bash
mssqlctl app run --name add-app --version v1 --inputs x=1,y=2
```

실행에 성공 하면 앱을 만들 때 지정 된 출력이 표시 됩니다. 다음은 예제입니다.

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

## <a name="create-an-app-skeleton"></a>앱 구조를 만들려면

Init 명령은 스 캐 폴드를 관련 아티팩트를 사용 하 여 앱 배포에 필요한를 제공 합니다. 아래 예제에서는 다음 명령을 실행 하면 hello를 만듭니다.

```bash
mssqlctl app init --name hello --version v1 --template python
```

Hello 라는 이름의 폴더를 만듭니다.  있습니다 `cd` 디렉터리로 폴더에 생성된 된 파일을 검사 합니다. spec.yaml 이름, 버전 및 소스 코드와 같은 앱을 정의합니다. 이름, 버전, 입력 및 출력을 변경 하려면 사양은 편집할 수 있습니다.

다음은 폴더에 표시 되는 init 명령의 샘플 출력

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>앱 설명

Describe 명령을 클러스터의 끝점을 포함 하 여 앱에 대 한 자세한 정보를 제공 합니다. 일반적으로 swagger 클라이언트 및 웹 서비스를 사용 하 여 RESTful 방식으로 앱과 상호 작용 하는 앱을 빌드하는 앱 개발자가 사용 됩니다. 참조 [빅 데이터 클러스터에 응용 프로그램을 사용](big-data-cluster-consume-apps.md) 자세한 내용은 합니다.

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
mssqlctl app delete --name add-app --version v1
```

## <a name="next-steps"></a>다음 단계

SQL Server에서 응용 프로그램에서 빅 데이터 클러스터에 배포 된 앱을 통합 하는 방법에 대해 [빅 데이터 클러스터에 응용 프로그램을 사용](big-data-cluster-consume-apps.md) 자세한 내용은 합니다. 추가 샘플에서 확인할 수 있습니다 [응용 프로그램 배포 샘플](https://aka.ms/sql-app-deploy)합니다.

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
