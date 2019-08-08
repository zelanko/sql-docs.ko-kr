---
title: Kubernetes의 SQL Server Always On 가용성 그룹에 대한 배포 스크립트 만들기
description: 이 문서에서는 Kubernetes의 SQL Server Always On 가용성 그룹에 대한 배포 스크립트를 만드는 방법을 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 181773a19e87c34a1931cae05f5a329aedbc1239
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000135"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>SQL Server Always On 가용성 그룹에 대한 배포 스크립트 만들기

이 문서에서는 예제 배포 스크립트를 사용하여 단일 명령으로 Kubernetes 클러스터에서 가용성 그룹을 배포하는 방법을 설명합니다. `deploy-ag.py`는 클러스터에 대한 `.yaml` 파일을 만들고 Kubernetes 클러스터에 적용할 수 있는 Python 스크립트입니다.

[sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script)에서 파일을 다운로드합니다.

## <a name="before-you-start"></a>시작하기 전 주의 사항

워크스테이션에 다음 도구를 설치합니다.

* [Python](https://www.python.org/downloads/)(3.5 또는 3.6)
* [PyYAML](https://pyyaml.org/) - Python 패키지
* [Kubernetes Client](https://github.com/kubernetes-client/python) - Python 패키지

환경 변수에 python 경로를 추가합니다(Windows의 경우).

### <a name="install-the-required-components"></a>필수 구성 요소 설치

다음 예제에서는 Python용 PyYAML 및 Kubernetes Client 패키지를 설치합니다.

Python을 설치한 후 샘플 폴더를 다운로드하고 압축을 풉니다. 

필요한 파일을 구성하려면 다음 명령을 실행합니다. `<path>`를 압축을 푼 샘플 파일의 위치로 바꿉니다.

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>클러스터 만들기 및 구성 파일 다운로드

다음 예제에서는 AKS(Azure Kubernetes Service)에서 클러스터를 만듭니다.

이 스크립트를 실행하기 전에 꺾쇠 괄호(`<>`)로 묶은 값을 업데이트 합니다.

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>가용성 그룹에는 Kubernetes 버전 1.11.0 이상이 필요합니다. 이 예제에서는 1.11.1을 지정합니다.

## <a name="run-the-deployment-script"></a>배포 스크립트 실행

다음 예제는 `deploy-ag.py` 실행 방법을 보여 줍니다.

### <a name="help"></a>도움말

```cmd
python ./deploy-ag.py --help
```

* **사용법**: `deploy-ag.py [-h] {deploy | failover} ...`
* **선택적 인수**:
  * `-h, --help`는 이 도움말 메시지를 표시하고 종료됩니다.
* **하위 명령**:
  * Actions on k8s agent {deploy | failover}

  `deploy`

   가용성 그룹에 SQL Server 세트를 배포합니다.

  `failover`

   대상 복제본으로 장애 조치(failover)합니다.

### <a name="deploy-help"></a>배포 도움말

```cmd
python ./deploy-ag.py deploy --help
```

* **사용법**:

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  네임스페이스에 SQL Server 및 k8s 에이전트 배포(AG 이름)

* **선택적 인수**:
  
  `-h, --help`
  
  이 도움말 메시지를 표시하고 종료됩니다.
  
  `--verbose, -v`
  
  출력의 자세한 정도입니다.
  
  `--ag AG`
  
  가용성 그룹의 이름입니다. 기본값=ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  k8s 네임스페이스의 이름입니다. 지정하지 않으면 기본값은 AG 이름입니다.

  `--dry-run`
  
  매니페스트를 만들지만 적용하지는 않습니다.
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  SQL Server 인스턴스의 이름입니다(최대 5개, 공백으로 구분) 기본값=['mssql1', 'mssql2', 'mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  SA 암호입니다. 기본값='SAPassword2018'
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  네임스페이스 만들기를 건너뜁니다.

### <a name="failover-help"></a>장애 조치(Failover) 도움말

```cmd
python ./deploy-ag.py failover --help
```
* **사용법**: 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  수동 장애 조치(failover)

* **위치 인수**: `target_replica`

  장애 조치(failover)를 위한 대상 SQL Server 복제본의 이름입니다.

* **선택적 인수**:

  `-h, --help`
  
  이 도움말 메시지를 표시하고 종료됩니다.

  `--verbose, -v`
  
  출력의 자세한 정도입니다.

  `--ag AG`
  
  가용성 그룹의 이름입니다. 기본값=ag1

  `--namespace NAMESPACE`

  k8s 네임스페이스의 이름입니다. 지정하지 않으면 기본값은 AG 이름입니다.

  `--dry-run`
  
  매니페스트를 만들지만 적용하지는 않습니다.

### <a name="create-the-manifests---dont-apply"></a>매니페스트 만들기 - 적용 안 함

다음 스크립트는 매니페스트 파일을 만들지만 적용하지는 않습니다.

```cmd
python ./deploy-ag.py deploy --dry-run
```

다음 예제에서는 세 개의 복제본을 사용하여 네임스페이스 `AG1` 아래에 가용성 그룹의 매니페스트를 만듭니다. 스크립트를 실행하기 전에 `<MyC0m91exP@55w0r!>`를 복잡한 암호로 바꿉니다.

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

이전 명령은 샘플 yaml 파일 디렉터리를 생성합니다.

이 경우 명령 출력은 매니페스트 파일이 생성되는 위치를 보여 줍니다.

![스크립트 출력](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>매니페스트 만들기 및 적용

다음 예제에서는 세 개의 복제본을 사용하여 네임스페이스 `ag1` 아래에 가용성 그룹의 매니페스트를 만들고 Kubernetes 클러스터에 적용합니다. 그런 다음, 클러스터에서 가용성 그룹을 만듭니다. 스크립트를 실행하기 전에 `<MyC0m91exP@55w0r!>`를 복잡한 암호로 바꿉니다.

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

스크립트가 완료되면 Kubernetes 작업자는 스토리지, SQL Server 인스턴스, 부하 분산 장치 서비스를 만듭니다. [Kubernetes 대시보드](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)를 사용하여 배포를 모니터링할 수 있습니다.

Kubernetes가 SQL Server 컨테이너를 만든 후 다음을 수행합니다.

1. 클러스터의 SQL Server 인스턴스에 [연결](sql-server-linux-kubernetes-connect.md)합니다.

1. 데이터베이스를 만듭니다.

1. 데이터베이스의 전체 백업을 수행하여 로그 체인을 시작합니다.

1. 가용성 그룹에 데이터베이스를 추가합니다.

SQL Server가 자동으로 해당 복제본에 보조 데이터베이스를 만들도록 자동 시드를 사용하여 가용성 그룹을 만듭니다.

### <a name="manually-failover"></a>수동 장애 조치(failover)

다음 예제에서는 주 복제본을 장애 조치(failover)합니다.

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>다음 단계

[Kubernetes 클러스터의 SQL Server 가용성 그룹](sql-server-ag-kubernetes.md)
