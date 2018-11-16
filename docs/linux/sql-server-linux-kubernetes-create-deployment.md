---
title: SQL Server Always On 가용성 그룹에서 kubernetes에 대 한 배포 스크립트 만들기
description: 이 문서는 SQL Server Always On 가용성 그룹에서 kubernetes에 대 한 배포 스크립트를 작성 하는 방법에 설명
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6541cae5271e35fd5ad0030ffc8625fc97a46149
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659092"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>SQL Server Always On 가용성 그룹에 대 한 배포 스크립트 만들기

이 문서에는 예제 배포 스크립트를 사용 하 여 단일 명령으로 Kubernetes 클러스터에서 가용성 그룹을 배포 하는 방법을 설명 합니다. `deploy-ag.py` 만드는 Python 스크립트를 `.yaml` 클러스터에 대 한 파일 및 Kubernetes 클러스터에 적용할 수 있습니다.

파일에서 파일 다운로드 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script)합니다.

## <a name="before-you-start"></a>시작하기 전 주의 사항

워크스테이션에서 다음 도구를 설치 합니다.

* [Python](https://www.python.org/downloads/) (3.5 또는 3.6)
* [PyYAML](https://pyyaml.org/) -Python 패키지
* [Kubernetes 클라이언트](https://github.com/kubernetes-client/python) -Python 패키지

(Windows)에 대 한 환경 변수에 python 경로 추가 합니다.

### <a name="install-the-required-components"></a>필수 구성 요소 설치

다음 예제에서는 위의 Python 용 PyYAML 및 Kubernetes 클라이언트 패키지를 설치합니다.

Python을 설치한 후 다운로드 하 고 샘플 폴더를 추출 합니다. 

필요한 파일을 구성 하려면 다음 명령을 실행 합니다. 대체 `<path>` 추출 된 샘플 파일의 위치입니다.

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>클러스터 만들기 및 구성 파일 다운로드

다음 예제에서는 Azure Kubernetes Service (AKS)에서 클러스터를 만듭니다.

꺾쇠 괄호-에서 값을 업데이트 하는 스크립트를 실행 하기 전에 `<>`입니다.

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>가용성 그룹에는 Kubernetes 버전 1.11.0 필요 이상. 이 예제에서는 1.11.1를 지정합니다.

## <a name="run-the-deployment-script"></a>배포 스크립트를 실행 합니다.

다음 예제에서는 실행 하는 방법을 보여 줍니다 `deploy-ag.py`합니다.

### <a name="help"></a>도움말

```cmd
python ./deploy-ag.py --help
```

* **사용 현황**: `deploy-ag.py [-h] {deploy | failover} ...`
* **선택적 인수**:
  * `-h, --help` 이 도움말 메시지 및 종료를 표시 합니다.
* **하위**:
  * K8s 에이전트에 대 한 작업 {배포 | 장애 조치}

  `deploy`

   가용성 그룹에 있는 SQL 서버의 집합 배포

  `failover`

   대상 복제본으로 장애 조치 합니다.

### <a name="deploy-help"></a>배포 도움말

```cmd
python ./deploy-ag.py deploy --help
```

* **사용 현황**:

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  SQL Server 및 k8s namespace(AG name) 에이전트 배포

* **선택적 인수**:
  
  `-h, --help`
  
  이 도움말 메시지 및 종료를 표시 합니다.
  
  `--verbose, -v`
  
  출력의 자세한 정도
  
  `--ag AG`
  
  가용성 그룹의 이름입니다. 기본 ag1 =
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  k8s 네임 스페이스의 이름입니다. AG 이름 지정 되지 않은 경우 기본값은입니다.

  `--dry-run`
  
  매니페스트를 만들지만 적용 되지 마십시오.
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  SQL Server 인스턴스의 이름 (최대 5, 공백으로 구분 하 여) 기본 = ['mssql1', 'mssql2', 'mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  SA 암호입니다. 기본 'SAPassword2018' =
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  네임 스페이스 만들기를 건너뜁니다.

### <a name="failover-help"></a>장애 조치 도움말

```cmd
python ./deploy-ag.py failover --help
```
* **사용 현황**: 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  수동으로 장애 조치

* **위치 인수**: `target_replica`

  대상 SQL Server 복제본의 장애 조치에 대 한 이름

* **선택적 인수**:

  `-h, --help`
  
  이 도움말 메시지 및 종료를 표시 합니다.

  `--verbose, -v`
  
  출력의 자세한 정도

  `--ag AG`
  
  가용성 그룹의 이름입니다. 기본 ag1 =

  `--namespace NAMESPACE`

  k8s 네임 스페이스의 이름입니다. 기본적으로 AG 이름 지정 되지 않은 경우

  `--dry-run`
  
  를 만들지만 매니페스트는 적용 되지 마십시오.

### <a name="create-the-manifests---dont-apply"></a>매니페스트 만들기-적용 되지 마십시오

다음 스크립트는 매니페스트 파일을 만들지만 적용 되지 않습니다.

```cmd
python ./deploy-ag.py deploy --dry-run
```

다음 예제에서는 네임 스페이스에서 가용성 그룹에 대 한 매니페스트 `AG1` 세 개의 복제본을 사용 하 여 합니다. 스크립트를 실행 하기 전에 대체 `<MyC0m91exP@55w0r!>` 복잡 한 암호를 사용 하 여 합니다.

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

이전 명령은 샘플 yaml 파일 디렉터리를 생성합니다.

이 경우 명령 출력에서는 매니페스트 파일은 생성 되는 위치를 보여 줍니다.

![스크립트 출력](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>매니페스트 만들기 및 적용

다음 예제에서는 네임 스페이스에서 가용성 그룹에 대 한 매니페스트 `ag1` 세 개의 복제본을 사용 하 여 Kubernetes 클러스터에 적용 합니다. 클러스터는 가용성 그룹을 만든 됩니다. 스크립트를 실행 하기 전에 대체 `<MyC0m91exP@55w0r!>` 복잡 한 암호를 사용 하 여 합니다.

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

스크립트가 완료 되 면 Kubernetes 연산자는 storage, SQL Server 인스턴스, 부하 분산 장치 서비스를 만듭니다. 사용 하 여 배포를 모니터링할 수 있습니다 [Kubernetes 대시보드](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)합니다.

Kubernetes 후 SQL Server 컨테이너를 만듭니다.

1. [연결](sql-server-linux-kubernetes-connect.md) 클러스터의 SQL Server 인스턴스에 있습니다.

1. 데이터베이스를 만듭니다.

1. 전체 로그 체인을 시작 하려면 데이터베이스 백업을 수행 합니다.

1. 가용성 그룹에 데이터베이스를 추가 합니다.

가용성 그룹 자동 시드로 하므로 SQL Server는 적절 한 복제본에서 보조 데이터베이스를 만들 자동으로 만들어집니다.

### <a name="manually-failover"></a>수동으로 장애 조치

다음 예에서는 주 복제본 장애 실패합니다.

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>다음 단계

[Kubernetes 클러스터에서 SQL Server 가용성 그룹](sql-server-ag-kubernetes.md)
