---
title: 앱을 배포 하는 방법
titleSuffix: SQL Server 2019 big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 응용 프로그램으로 Python 또는 R 스크립트를 배포 합니다.
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 12/11/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: f37267083e0e56dd6e3c0e06c1d80ed79c0d9969
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241934"
---
# <a name="how-to-deploy-an-app-on-sql-server-2019-big-data-cluster-preview"></a>SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 앱을 배포 하는 방법

이 문서에서는 배포 및 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 내에서 응용 프로그램으로 R 및 Python 스크립트를 관리 하는 방법을 설명 합니다.

R 및 Python 응용 프로그램 배포 및 관리 합니다 **mssqlctl-pre** CTP 2.2에 포함 된 명령줄 유틸리티입니다. 이 문서에서는 명령줄에서 앱으로 이러한 R 및 Python 스크립트를 배포 하는 방법의 예제를 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

구성 된 SQL Server 2019 빅 데이터 클러스터가 있어야 합니다. 자세한 내용은 [빅 데이터에서 kubernetes 클러스터는 SQL Server를 배포 하는 방법을](deployment-guidance.md)합니다. 

## <a name="installation"></a>설치

합니다 **mssqlctl-pre** 명령줄 유틸리티는 미리 보기에 Python 및 R 응용 프로그램 배포 기능 제공 됩니다. 유틸리티를 설치 하려면 다음 명령을 사용 합니다.

```cmd
pip install -r https://private-repo.microsoft.com/python/ctp-2.2/mssqlctlpre/mssqlctlpre.txt --trusted-host https://private-repo.microsoft.com
```

## <a name="capabilities"></a>Capabilities

CTP 2.2의 있습니다 수 만들기, 삭제, 나열 및 R 또는 Python 응용 프로그램을 실행 합니다. 다음 표에서 사용할 수 있는 응용 프로그램 배포 명령을 **mssqlctl-pre**합니다.

| Command | Description |
|---|---|
| `mssqlctl-pre login` | SQL Server 빅 데이터 클러스터에 로그인 |
| `mssqlctl-pre app create` | 앱 만들기 |
| `mssqlctl-pre app list` | 배포 된 앱 목록 |
| `mssqlctl-pre app delete` | 앱 삭제 |
| `mssqlctl-pre app run` | 실행 중인 앱 목록 |

사용 하 여 도움말을 볼 수는 `--help` 다음 예제와 같이 매개 변수:

```bash
mssqlctl-pre app create --help
```

다음 섹션에서는 이러한 명령을 자세히 설명합니다.

## <a name="log-in"></a>로그인

R 및 Python 응용 프로그램을 구성 하기 전에 먼저 사용 하 여 빅 데이터 클러스터에 SQL Server에 로그인 합니다 `mssqlctl-pre login` 명령입니다. 외부 IP 주소를 지정 합니다 `service-proxy-lb` 또는 `service-proxy-nodeport` 서비스 (예를 들어: `https://ip-address:30777`) 사용자 이름 및 클러스터에는 암호와 함께 합니다.

IP 주소를 가져올 수는 **서비스-프록시-lb** 하거나 **nodeport-프록시 서비스-** bash 또는 cmd 창에서이 명령을 실행 하 여 서비스:

```bash 
kubectl get svc service-proxy-lb -n <name of your cluster>
```

```bash
mssqlctl-pre login -e https://<ip-address-of-service-proxy-lb>:30777 -u <user-name> -p <password>
```

## <a name="create-an-app"></a>앱 만들기

Python 또는 R 코드 파일을 전달 하면 응용 프로그램을 만들려면 **mssqlctl-pre** 사용 하 여는 `app create` 명령입니다. 이러한 파일에서 앱을 만들려는 컴퓨터에 로컬로 상주 합니다.

빅 데이터 클러스터에 새 앱을 만들려면 다음 구문을 사용 합니다.

```bash
mssqlctl-pre app create -n <app_name> -v <version_number> -r <runtime> -i <path_to_code_init> -c <path_to_code> --inputs <input_params> --outputs <output_params> 
```

다음 명령은이 명령은 같습니다는 항목의 예를 보여줍니다.

```py
#add.py
def add(x,y):
        result = x+y
        return result;
result=add(x,y)
```
이 사용 하려면 위 코드 줄으로 로컬 디렉터리에 저장 `add.py` 아래 명령을 실행 하 고

```bash
mssqlctl-pre app create --name add-app --version v1 --runtime Python --code ./add.py  --inputs x=int,y=int --outputs result=int 
```

명령 목록을 사용 하 여 앱이 배포를 확인할 수 있습니다.

```bash
mssqlctl-pre app list
```

배포 불완전 한 경우는 "state" 표시 "만들기" 나타나야 합니다. 

```
[
  {
    "name": "add-app",
    "state": "Creating",
    "version": "v1"
  }
]
```

"상태"를 참조 해야 성공적으로 배포 된 후 "준비" 상태로 변경 합니다.

```
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
mssqlctl-pre app list
```

이름 및 버전을 지정 하면 해당 특정 앱 및 (만드는 중 또는 준비) 상태를 나열 됩니다.

```bash
mssqlctl-pre app list --name <app_name> --version <app_version>
```

다음 예제에서는이 명령을 보여 줍니다.

```bash
mssqlctl-pre app list --name add-app --version v1
```

다음 예제와 유사한 출력이 표시 됩니다.

```
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>앱 실행

"준비" 상태의 앱 인 경우에 지정 된 입력된 매개 변수를 사용 하 여 실행 하 여 사용할 수 있습니다. 앱을 실행 하려면 다음 구문을 사용 합니다.

```bash
mssqlctl-pre app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

다음 예제 명령은 실행된 명령을 보여 줍니다.

```bash
mssqlctl-pre app run --name add-app --version v1 --inputs x=1,y=2
```

실행에 성공 하면 앱을 만들 때 지정 된 출력이 표시 됩니다. 다음은 예제입니다.

```
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

## <a name="delete-an-app"></a>앱 삭제

빅 데이터 클러스터에서 앱을 삭제 하려면 다음 구문을 사용 합니다.

```bash
mssqlctl-pre app delete --name add-app --version v1
```

## <a name="next-steps"></a>다음 단계

추가 샘플에서 확인할 수 있습니다 [ https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster)합니다. 

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
