---
title: 배포 하는 방법
titleSuffix: SQL Server 2019 big data clusters
description: Kubernetes에서 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 배포 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 817ffcc1ea17a8526304b4bc9064c1becfff90f9
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161647"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Kubernetes에서 SQL Server 빅 데이터 클러스터를 배포 하는 방법

Kubernetes 클러스터에 docker 컨테이너로 SQL Server 빅 데이터 클러스터를 배포할 수 있습니다. 설치 및 구성 단계 개요는 다음과 같습니다.

- 단일 VM 또는 Azure Kubernetes Service (AKS)에서 Vm의 클러스터에서 Kubernetes 클러스터를 설정 합니다.
- 클러스터 구성 도구를 설치 **mssqlctl** 클라이언트 컴퓨터에 있습니다.
- Kubernetes 클러스터에서 SQL Server 빅 데이터 클러스터를 배포 합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Kubernetes 클러스터 필수 구성 요소

SQL Server 빅 데이터 클러스터의 Kubernetes 버전을 이상이 필요 v1.10 서버 및 클라이언트 (kubectl)에 대 한 합니다.

> [!NOTE]
> 클라이언트와 서버가 Kubernetes 버전 + 1 또는-1 부 버전 되도록 참고 합니다. 자세한 내용은 [지원 되는 버전 및 구성 요소 기울이기 Kubernetes](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)합니다.

## <a id="kubernetes"></a> Kubernetes 클러스터 설치

위의 필수 구성 요소를 충족 하는 Kubernetes 클러스터가 이미 있는 경우 직접 건너뛸 수 있습니다 합니다 [배포 단계](#deploy)합니다. 이 섹션에서는 Kubernetes 개념의 기본 지식이 있다고 가정 합니다.  Kubernetes에 대 한 자세한 내용은 참조는 [Kubernetes 설명서](https://kubernetes.io/docs/home)합니다.

세 가지 방법 중 하나로 Kubernetes 배포를 선택할 수 있습니다.

| Kubernetes에 배포 합니다. | Description | 링크 |
|---|---|---|
| **Minikube** | VM에서 단일 노드 Kubernetes 클러스터입니다. | [지침](deploy-on-minikube.md) |
| **Azure Kubernetes 서비스 (AKS)** | Azure의 관리 되는 Kubernetes 컨테이너 서비스입니다. | [지침](deploy-on-aks.md) |
| **여러 컴퓨터** | 물리적 컴퓨터 또는 가상 컴퓨터를 사용 하 여 배포 된 Kubernetes 클러스터의 **kubeadm** | [지침](deploy-with-kubeadm.md) |
  
> [!TIP]
> AKS와 SQL Server 빅 데이터 클러스터를 배포 하는 샘플 python 스크립트를 참조 하세요 [빅 데이터 클러스터 Azure Kubernetes Service (AKS)에서 SQL Server 배포](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks)합니다.

## <a name="deploy-sql-server-2019-big-data-tools"></a>SQL Server 2019 빅 데이터 도구 배포

먼저 SQL Server 2019 빅 데이터 클러스터를 배포 하기 전에 [big data tools 설치](deploy-big-data-tools.md):
- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 확장**

## <a id="deploy"></a> SQL Server 빅 데이터 클러스터를 배포 합니다.

Kubernetes 클러스터를 구성한 후에 SQL Server 빅 데이터 클러스터에 대 한 배포를 사용 하 여 진행할 수 있습니다. 

> [!NOTE]
> 이전 릴리스에서 업그레이드 하는 경우를 참조 하십시오 합니다 [이 문서의 섹션 업그레이드](#upgrade)합니다.

개발/테스트 환경에 대 한 모든 기본 구성 사용 하 여 Azure에서 빅 데이터 클러스터를 배포 하려면이 문서의 지침을 따릅니다.

[빠른 시작: Kubernetes에서 SQL Server 빅 데이터 클러스터를 배포 합니다.](quickstart-big-data-cluster-deploy.md)

빅 데이터 클러스터 워크 로드에 따라 배포를 사용자 지정 하려는 경우 요구,이 문서의 나머지 부분에 지침을 따릅니다.

## <a name="verify-kubernetes-configuration"></a>Kubernetes 구성 확인

실행 합니다 **kubectl** 클러스터 구성을 보려면 명령입니다. 해당 kubectl 가리키는 올바른 클러스터 컨텍스트를 확인 합니다.

```bash
kubectl config view
```

## <a id="env"></a> 환경 변수를 정의 합니다.

에 전달 되는 환경 변수 집합을 사용 하 여 클러스터 구성을 사용자 지정할 수는 `mssqlctl create cluster` 명령입니다. 대부분의 환경 변수는 아래 따라 기본값을 사용 하 여 선택적입니다. 사용자 입력을 요구 하는 자격 증명 같은 환경 변수는 note 합니다.

| 환경 변수 | 필수 | 기본값 | Description |
|---|---|---|---|
| **ACCEPT_EULA** | 사용자 계정 컨트롤 | 해당 사항 없음 | SQL Server 사용권 계약 (예: 'Yes')에 동의 합니다.  |
| **CLUSTER_NAME** | 사용자 계정 컨트롤 | 해당 사항 없음 | 빅 데이터 클러스터에 sql Server를 배포 하려면 Kubernetes 네임 스페이스의 이름입니다. |
| **CLUSTER_PLATFORM** | 사용자 계정 컨트롤 | 해당 사항 없음 | Kubernetes 클러스터가 배포 된 플랫폼입니다. 일 수 있습니다 `aks`, `minikube`, `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | 아니요 | 1 | 빌드할 계산 풀 복제본의 수입니다. Ctp 2.3 반환만 허용 되는 1입니다. |
| **CLUSTER_DATA_POOL_REPLICAS** | 아니요 | 2 | 풀 구축 하는 복제본에서 데이터의 수입니다. |
| **CLUSTER_STORAGE_POOL_REPLICAS** | 아니요 | 2 | 저장소 풀 복제본의 수입니다. |
| **DOCKER_REGISTRY** | 사용자 계정 컨트롤 | TBD | 클러스터를 배포 하는 데 사용 되는 이미지가 저장 된 개인 레지스트리입니다. |
| **DOCKER_REPOSITORY** | 사용자 계정 컨트롤 | TBD | 이미지가 저장 된 위의 레지스트리 내 개인 저장소.  것 필요한 것은 제어 된 체크 인된 공개 미리 보기 기간에 대 한 합니다. |
| **DOCKER_USERNAME** | 사용자 계정 컨트롤 | 해당 사항 없음 | 개인 저장소에 저장 됩니다 하는 경우 컨테이너 이미지에 액세스 하려면 사용자 이름입니다. 것 필요한 것은 제어 된 체크 인된 공개 미리 보기 기간에 대 한 합니다. |
| **DOCKER_PASSWORD** | 사용자 계정 컨트롤 | 해당 사항 없음 | 위의 개인 리포지토리에 액세스 하기 위한 암호입니다. 것 필요한 것은 제어 된 체크 인된 공개 미리 보기 기간에 대 한 합니다.|
| **DOCKER_EMAIL** | 사용자 계정 컨트롤 | 해당 사항 없음 | 전자 메일 주소입니다. |
| **DOCKER_IMAGE_TAG** | 아니요 | 최신 | 이미지 태그를 지정 하는 데 사용 되는 레이블. |
| **DOCKER_IMAGE_POLICY** | 아니요 | Always | 이미지 끌어오기를 항상 강제로 적용 합니다.  |
| **DOCKER_PRIVATE_REGISTRY** | 사용자 계정 컨트롤 | 해당 사항 없음 | 제어 된 체크 인된 공개 미리 보기 기간에 대 한이 값을 "1"로 설정 해야 합니다. |
| **CONTROLLER_USERNAME** | 사용자 계정 컨트롤 | 해당 사항 없음 | 클러스터 관리자의 사용자 이름입니다. |
| **CONTROLLER_PASSWORD** | 사용자 계정 컨트롤 | 해당 사항 없음 | 클러스터 관리자의 암호입니다. |
| **KNOX_PASSWORD** | 사용자 계정 컨트롤 | 해당 사항 없음 | Knox 사용자에 대 한 암호입니다. |
| **MSSQL_SA_PASSWORD** | 사용자 계정 컨트롤 | 해당 사항 없음 | 마스터 SQL 인스턴스 SA 사용자의 암호입니다. |
| **USE_PERSISTENT_VOLUME** | 아니요 | true | `true` Kubernetes 영구적 볼륨을 사용 하려면 pod 저장소에 대 한 클레임입니다.  `false` pod 저장소에 대 한 임시 호스트 저장소를 사용 하 합니다. 참조 된 [데이터 지 속성](concept-data-persistence.md) 을 참조 하십시오. 빅 데이터 클러스터 minikube를 SQL Server 및 USE_PERSISTENT_VOLUME를 배포 하는 경우 = true를 설정 해야 값 `STORAGE_CLASS_NAME=standard`합니다. |
| **STORAGE_CLASS_NAME** | 아니요 | 기본 | 하는 경우 `USE_PERSISTENT_VOLUME` 는 `true` 사용할 Kubernetes 저장소 클래스의 이름을 나타냅니다. 참조 된 [데이터 지 속성](concept-data-persistence.md) 을 참조 하십시오. SQL Server minikube의 빅 데이터 클러스터를 배포 하는 경우 기본 저장소 클래스 이름이 다릅니다 및 설정 하 여 재정의 해야 `STORAGE_CLASS_NAME=standard`합니다. |
| **CONTROLLER_PORT** | 아니요 | 30080 | 컨트롤러 서비스를 공용 네트워크에서 수신 하는 TCP/IP 포트입니다. |
| **MASTER_SQL_PORT** | 아니요 | 31433 | 마스터 SQL 인스턴스는 공용 네트워크에서 수신 대기 하는 TCP/IP 포트입니다. |
| **KNOX_PORT** | 아니요 | 30443 | Apache Knox 공용 네트워크에서 수신 대기 하는 TCP/IP 포트입니다. |
| **PROXY_PORT** | 아니요 | 30777 | 공용 네트워크에서 프록시 서비스가 수신 대기 하는 TCP/IP 포트입니다. 이 포털을 계산 하는 데 포트 URL입니다. |
| **GRAFANA_PORT** | 아니요 | 30888 | 응용 프로그램 모니터링 Grafana 공용 네트워크에서 수신 대기 하는 TCP/IP 포트입니다. |
| **KIBANA_PORT** | 아니요 | 30999 | Kibana 로그 검색 응용 프로그램은 공용 네트워크에서 수신 대기 하는 TCP/IP 포트입니다. |


> [!IMPORTANT]
>1. 제한 된 비공개 미리 보기 기간에 대 한 개인 Docker 레지스트리에 대 한 자격 증명은 시 제공 해야 할 심사 하 [EAP 등록](https://aka.ms/eapsignup)합니다.
>1. 온-프레미스 클러스터를 사용 하 여 작성에 대 한 **kubeadm**, 환경 변수에 대해 값 `CLUSTER_PLATFORM` 는 `kubernetes`합니다. 또한 때 `USE_PERSISTENT_VOLUME=true`, Kubernetes 저장소 클래스를 사전 프로 비전 하 고 사용 하 여 전달 해야 합니다는 `STORAGE_CLASS_NAME`합니다.
>1. 모든 특수 문자를 포함 하는 경우 큰따옴표로 암호를 배치 해야 합니다. 원하는 MSSQL_SA_PASSWORD를 설정할 수 있습니다 하지만 해야 충분히 복잡 하지 사용 하는 `!`, `&` 또는 `'` 문자입니다. 큰따옴표로 구분 기호에만 작동 하는 bash 명령입니다.
>1. 클러스터의 이름에는 소문자 영숫자 문자만 공백 없이 이어야 합니다. 클러스터와 동일한 이름 가진 네임 스페이스의 클러스터에 대 한 모든 Kubernetes 아티팩트 (컨테이너, pod, 상태 집합, 서비스)를 만들 수는 지정 된 이름입니다.
>1. 합니다 **SA** 계정은 설치 중에 생성 되는 SQL Server Master 인스턴스의 시스템 관리자입니다. 실행 하 여 검색할 수는 SQL Server 컨테이너를 지정한 MSSQL_SA_PASSWORD 환경 변수 만들기 후 컨테이너에서 $MSSQL_SA_PASSWORD 에코 합니다. 보안상의 이유로 설명 된 모범 사례에 따라 SA 암호를 변경 [여기](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)합니다.

Windows 또는 Linux 클라이언트를 사용 하는 여부에 따라 다른 빅 데이터 클러스터를 배포 하는 데 필요한 환경 변수를 설정 합니다.  사용 중인 운영 체제에 따라 아래 단계를 선택 합니다.

다음 환경 변수를 초기화는 클러스터를 배포 하는 데 필요 합니다.

### <a name="windows"></a>Windows

창 (PowerShell이 아님), CMD를 사용 하 여 다음 환경 변수를 구성 합니다. 값 주위에 따옴표를 사용 하지 마세요.

```cmd
SET ACCEPT_EULA=yes
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username, credentials provided by Microsoft>
SET DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
SET DOCKER_EMAIL=<your email address>
SET DOCKER_PRIVATE_REGISTRY=1
```

### <a name="linux"></a>Linux

다음 환경 변수를 초기화 합니다. Bash에서 각 값 주위에 따옴표를 사용할 수 있습니다.

```bash
export ACCEPT_EULA="yes"
export CLUSTER_PLATFORM="<minikube or aks or kubernetes>"

export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="<your username, credentials provided by Microsoft>"
export DOCKER_PASSWORD="<your password, credentials provided by Microsoft>"
export DOCKER_EMAIL="<your email address>"
export DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="minikube-settings"></a>Minikube 설정

Minikube에서 배포 하는 경우 및 `USE_PERSISTENT_VOLUME=true` (기본값)를 재정의 해야 기본값이 `STORAGE_CLASS_NAME` 환경 변수입니다.

Windows에서 다음 명령을 사용 하 여 minikube 배포:

```cmd
SET STORAGE_CLASS_NAME=standard
```

Linux에서 다음 명령을 사용 하 여 minikube 배포:

```bash
export STORAGE_CLASS_NAME=standard
```

Minikube에서 영구적 볼륨을 사용 하 여 설정 하 여 무시할 수 또는 `USE_PERSISTENT_VOLUME=false`합니다.

### <a name="kubadm-settings"></a>Kubadm 설정

Kubernetes 저장소 클래스를 사전 프로 비전 하 고 사용 하 여 통과 해야 kubeadm 고유한 물리적 컴퓨터 또는 가상 컴퓨터를 배포 하는 경우는 `STORAGE_CLASS_NAME`합니다. 영구적 볼륨을 사용 하 여 설정 하 여 무시할 수 또는 `USE_PERSISTENT_VOLUME=false`합니다. 영구 저장소에 대 한 자세한 내용은 참조 하세요. [빅 데이터에서 kubernetes 클러스터는 SQL Server를 사용 하 여 데이터 지 속성](concept-data-persistence.md)합니다.

## <a name="deploy-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터 배포

클러스터 만들기 API Kubernetes 네임 스페이스를 초기화 하 고 네임 스페이스에 모든 응용 프로그램 pod를 배포에 사용 됩니다. Kubernetes 클러스터에서 SQL Server 빅 데이터 클러스터를 배포 하려면 다음 명령을 실행 합니다.

```bash
mssqlctl cluster create --name <your-cluster-name>
```

클러스터 부트스트랩 하는 동안 클라이언트 명령 창에는 배포 상태를 출력 합니다. 배포 과정에서 컨트롤러 pod에 대 한 기다리고 있는 일련의 메시지를 표시 됩니다.

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

10 ~ 20 분 후 있습니다 알려야 컨트롤러 pod가 실행 중인지:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> 전체 배포는 빅 데이터 클러스터의 구성 요소에 대 한 컨테이너 이미지를 다운로드 하는 데 필요한 시간 때문에 시간이 걸릴 수 있습니다. 그러나 하지 몇 시간이 걸립니다. 배포 문제가 발생 하는 경우 참조를 [문제 해결](#troubleshoot) 모니터링 및 배포를 검사 하는 방법을 알아보려면이 문서의 섹션입니다.

배포가 완료 되 면 출력 성공 하면 알립니다.

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

## <a id="masterip"></a> 빅 데이터 클러스터 끝점 가져오기

배포 스크립트를 성공적으로 완료 된 후에 아래 설명 된 단계를 사용 하 여 SQL Server 마스터 인스턴스의 IP 주소를 얻을 수 있습니다. 이 IP 주소와 포트 번호 31433를 사용 하 여 SQL Server 마스터 인스턴스에 연결할 됩니다 (예:  **\<ip-address-of-endpoint-master-pool\>31433,**). 마찬가지로, 빅 데이터 클러스터 (Spark HDFS/게이트웨이) IP와 연결 된 SQL Server를 연결할 수 있습니다 합니다 **끝점 보안** 서비스입니다.

Kubectl 명령을 빅 데이터 클러스터에 대 한 공용 끝점을 검색합니다.

```bash
kubectl get svc endpoint-master-pool -n <your-cluster-name>
kubectl get svc endpoint-security -n <your-cluster-name>
kubectl get svc endpoint-service-proxy -n <your-cluster-name>
```

검색할 합니다 **EXTERNAL-IP** 각 서비스에 할당 되는 값입니다.

모든 클러스터 끝점에 설명 되어는 **서비스 끝점** 클러스터 관리 포털을 탭 합니다. 외부 IP 주소 및 포트 번호를 사용 하 여 포털에 액세스할 수 있습니다 합니다 `endpoint-service-proxy` (예: **https://\<ip-address-of-endpoint-service-proxy\>: 30777/포털**). 값은 관리 포털 액세스에 대 한 자격 증명 `CONTROLLER_USERNAME` 고 `CONTROLLER_PASSWORD` 위에 제공 된 환경 변수입니다. 또한 배포를 모니터링 하려면 클러스터 관리 포털을 사용할 수 있습니다.

연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [Azure Data Studio를 사용 하 여 빅 데이터 클러스터를 SQL Server에 연결](connect-to-big-data-cluster.md)합니다.

### <a name="minikube"></a>Minikube

Minikube를 사용 하는 경우에 연결 해야 합니다. IP 주소를 가져오려면 다음 명령을 실행 해야 합니다. IP에 외에도 연결 해야 하는 끝점에 대 한 포트를 지정 합니다. 에 대 한 모든 서비스 끝점을 가져오려면 

```bash
minikube ip
```

플랫폼에 관계 없이 실행 하는 Kubernetes 클러스터에서 클러스터에 대해 실행 명령 다음에 배포 된 모든 서비스 끝점을 가져오려면:
```bash
kubectl get svc -n <your-cluster-name>
```

## <a id="upgrade"></a> 새 릴리스로 업그레이드

현재 빅 데이터 클러스터를 새 릴리스로 업그레이드 하는 유일한 방법은 수동으로 제거 하 고 클러스터를 다시 만듭니다. 에 고유한 버전의 각 릴리스에 **mssqlctl** 는 이전 버전과 호환 되지 않습니다. 또한 새 노드에서 이미지를 다운로드 하는 이전 클러스터 있으면 최신 이미지 클러스터에서 이전 이미지와 호환 되지 않을 수 있습니다. 최신 버전으로 업그레이드 하려면 다음 단계를 사용 합니다.

1. 이전 클러스터를 삭제 하기 전에 SQL Server 마스터 인스턴스 및 HDFS에서 데이터를 백업 합니다. SQL Server 마스터 인스턴스를 사용할 수 있습니다 [SQL Server 백업 및 복원](data-ingestion-restore-database.md)합니다. HDFS에 대 한 있습니다 [사용 하 여 데이터를 복사할 수 있습니다 **curl**](data-ingestion-curl.md)합니다.

1. 사용 하 여 이전 클러스터를 삭제 합니다 `mssqlctl delete cluster` 명령입니다.

   ```bash
    mssqlctl cluster delete --name <old-cluster-name>
   ```

   > [!Important]
   > 버전을 사용 하 여 **mssqlctl** 일치 하는 클러스터입니다. 최신 버전을 사용 하 여 이전 클러스터를 삭제 하지 마세요 **mssqlctl**합니다.

1. 이전 버전을 모두 제거 **mssqlctl**합니다.

   ```bash
   pip3 uninstall mssqlctl
   ```

   > [!IMPORTANT]
   > 새 버전을 설치 하지 해야 **mssqlctl** 이전 버전을 먼저 제거 하지 않고 있습니다.

1. 최신 버전의 설치 **mssqlctl**합니다. 

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt --user
   ```

   > [!IMPORTANT]
   > 각 릴리스에 대 한 경로 대 한 **mssqlctl** 변경 합니다. 이전에 설치한 경우에 **mssqlctl**, 최신 경로에서 새 클러스터를 만들기 전에 다시 설치 해야 합니다.

1. 지침을 사용 하 여 최신 릴리스를 설치 합니다 [배포 섹션](#deploy) 이 문서의. 

## <a id="troubleshoot"></a> 모니터링 및 문제 해결

를 모니터링 하거나 배포 문제 해결 **kubectl** 클러스터의 상태를 검사 하 고 잠재적인 문제를 찾아내는 합니다. 배포 중 언제 든 다음 테스트를 실행 하려면 다른 명령 창을 열면 됩니다.

1. 클러스터의 pod의 상태를 검사 합니다.

   ```cmd
   kubectl get pods -n <your-cluster-name>
   ```

   배포 하는 동안 사용 하 여 포드를 **상태** 의 **ContainerCreating** 여전히 발생 됩니다. 배포에 어떤 이유로 중지 되는 경우이 수 알 수 있습니다 위치 문제일 수 있습니다. 살펴볼 수도 합니다 **준비** 열입니다. 그러면 pod에 얼마나 많은 컨테이너가 시작 합니다. Note는 배포 구성 및 네트워크에 따라 30 분 이상 걸릴 수 있습니다. 다양 한 구성 요소에 대 한 컨테이너 이미지를 다운로드 하는 데 소요 된이 시간의 대부분입니다. 다음 표에서 배포 중 두 개의 컨테이너의 출력을 편집 하는 예를 보여 줍니다.

   ```output
   PS C:\> kubectl get pods -n sbdc8
   NAME                                     READY   STATUS              RESTARTS   AGE
   mssql-controller-h79ft                   4/4     Running             0          13m
   mssql-storage-pool-default-0             0/7     ContainerCreating   0          6m
   ```

1. 자세한 내용은 개별 포드를 설명 합니다. 다음 명령은 검사는 `mssql-storage-pool-default-0` pod입니다.

   ```cmd
   kubectl describe pod mssql-storage-pool-default-0 -n <your-cluster-name>
   ```

   이 최근 이벤트를 포함 하 여 pod에 대 한 자세한 정보를 출력 합니다. 오류가 발생 하는 경우 때로는 여기서 오류를 찾을 수 있습니다.

1. Pod에서 실행 중인 컨테이너에 대 한 로그를 검색 합니다. 다음 명령은 명명 된 pod에서 실행 중인 모든 컨테이너에 대 한 로그 검색 `mssql-storage-pool-default-0` 파일 이름으로 출력 `pod-logs.txt`:

   ```cmd
   kubectl logs mssql-storage-pool-default-0 --all-containers=true -n <your-cluster-name> > pod-logs.txt
   ```

1. 다음 명령 사용 하 여 배포 전후 동안 클러스터 서비스를 검토 합니다.

   ```cmd
   kubectl get svc -n <your-cluster-name>
   ```

   이러한 서비스는 빅 데이터 클러스터에 대 한 내부 및 외부 연결을 지원합니다. 외부 연결을 위해 다음 서비스가 사용 됩니다.

   | 서비스 | Description |
   |---|---|
   | **endpoint-master-pool** | 마스터 인스턴스에 대 한 액세스를 제공합니다.<br/>(**EXTERNAL-IP 31433** 하며 **SA** 사용자) |
   | **endpoint-controller** | 도구 및 클러스터를 관리 하는 클라이언트를 지원 합니다. |
   | **endpoint-service-proxy** | 에 대 한 액세스를 제공 합니다 [클러스터 관리 포털](cluster-admin-portal.md)합니다.<br/>(https://**EXTERNAL-IP**: 30777/포털)|
   | **endpoint-security** | HDFS/Spark gateway에 대 한 액세스를 제공합니다.<br/>(**EXTERNAL-IP** 하며 **루트** 사용자) |

1. 사용 하 여는 [클러스터 관리 포털](cluster-admin-portal.md) 에서 배포를 모니터링 하는 **배포** 탭 합니다. 기다릴 필요가 합니다 **끝점 서비스 프록시** 서비스를 배포의 시작 부분에 사용할 수 없게 되므로이 포털에 액세스 하기 전에 시작 합니다.

> [!TIP]
> 클러스터 문제 해결에 대 한 자세한 내용은 참조 하세요. [모니터링 및 SQL Server 빅 데이터 클러스터 문제 해결에 대 한 Kubectl 명령을](cluster-troubleshooting-commands.md)합니다.

## <a name="next-steps"></a>다음 단계

배우고 새 기능 중 일부를 사용해 보세요 [SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법을](notebooks-guidance.md)합니다.
