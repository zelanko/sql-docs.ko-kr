---
title: Kubernetes에서 SQL Server에 대 한 빅 데이터 클러스터를 배포 하는 방법 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/08/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: f998c9f9df91f08d3a4e1877942b901ae5d96aeb
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460658"
---
# <a name="how-to-deploy-sql-server-big-data-cluster-on-kubernetes"></a>Kubernetes에서 SQL Server에 대 한 빅 데이터 클러스터를 배포 하는 방법

Kubernetes 클러스터에 docker 컨테이너로 SQL Server에 대 한 빅 데이터 클러스터를 배포할 수 있습니다. 설치 및 구성 단계 개요는 다음과 같습니다.

- 단일 VM, Vm 또는 Azure Container Service 클러스터의 Kubernetes 클러스터를 설정 합니다.
- 클러스터 구성 도구를 설치 `mssqlctl` 클라이언트 컴퓨터에서
- Kubernetes 클러스터에서 SQL Server에 대 한 빅 데이터 클러스터 배포

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Kubernetes 클러스터 필수 구성 요소

SQL Server에 대 한 빅 데이터 클러스터 Kubernetes에 대 한, 서버 및 클라이언트에 대 한 최소 v1.10 버전이 필요합니다. 특정 버전의 kubectl 클라이언트를 설치 하려면 참조 [curl을 통해 이진 kubectl 설치](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl)합니다.  최신 버전의 minikube 및 AKS는 1.10 이상. AKS에 대 한 사용 해야 `--kubernetes-version` 기본값과 다른 버전을 지정 하려면 매개 변수입니다.

> [!NOTE]
> 클라이언트와 서버가 Kubernetes 버전 + 1 또는-1 부 버전 되도록 참고 합니다. 자세한 내용은 [지원 되는 버전 및 구성 요소 기울이기 Kubernetes](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)합니다.

## <a id="kubernetes"></a> Kubernetes 클러스터 설치

위의 필수 구성 요소를 충족 하는 Kubernetes 클러스터가 이미 있는 경우 직접 건너뛸 수 있습니다 합니다 [배포 단계](#deploy)합니다. 이 섹션에서는 Kubernetes 개념의 기본 지식이 있다고 가정 합니다.  Kubernetes에 대 한 자세한 내용은 참조는 [Kubernetes 설명서](https://kubernetes.io/docs/home)합니다.

세 가지 방법 중 하나로 Kubernetes 배포를 선택할 수 있습니다.

| Kubernetes에 배포 합니다. | Description |
|---|---|
| **Minikube** | VM에서 단일 노드 Kubernetes 클러스터입니다. |
| **Azure Kubernetes 서비스 (AKS)** | Azure의 관리 되는 Kubernetes 컨테이너 서비스입니다. |
| **여러 Vm** | Kubeadm를 사용 하 여 Vm에 배포 된 Kubernetes 클러스터 |

를 구성 하는 SQL Server에 대 한 빅 데이터 클러스터에 대 한 다음 Kubernetes 클러스터 중 하나에 대 한 다음 문서 중 하나를 참조 하세요.

   - [Minikube를 구성 합니다.](deploy-on-minikube.md)
   - [Azure Kubernetes Service에서 Kubernetes 구성](deploy-on-aks.md)
   
> [!TIP]
> AKS와 SQL Server 빅 데이터 클러스터를 배포 하는 샘플 python 스크립트를 참조 하세요 [빅 데이터 클러스터 Azure Kubernetes Service (AKS)에서 SQL Server 배포](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks)합니다.

## <a id="deploy"></a> SQL Server에 대 한 빅 데이터 클러스터 배포

Kubernetes 클러스터를 구성한 후에 SQL Server에 대 한 빅 데이터 클러스터에 대 한 배포를 사용 하 여 진행할 수 있습니다. 개발/테스트 환경에 대 한 모든 기본 구성 사용 하 여 빅 데이터 클러스터를 배포 하려면이 문서의 지침을 따릅니다.

[빠른 시작: SQL Server 빅 데이터에서 kubernetes 클러스터 배포](quickstart-big-data-cluster-deploy.md)

워크 로드 요구 사항에 따라 빅 데이터 클러스터 구성을 사용자 지정할 수 하려는 경우 다음 일련의 지침을 따릅니다.

## <a name="verify-kubernetes-configuration"></a>Kubernetes 구성 확인

실행 된 아래 클러스터 구성을 보려면 kubectl 명령을 합니다. 해당 kubectl 가리키는 올바른 클러스터 컨텍스트를 확인 합니다.

```bash
kubectl config view
```

## <a name="install-mssqlctl-cli-management-tool-for-sql-server-big-data-cluster"></a>SQL Server에 대 한 빅 데이터 클러스터에 대 한 mssqlctl CLI 관리 도구 설치
`mssqlctl` 명령줄 유틸리티를 사용 하면 클러스터 관리자가 부트스트랩 REST Api를 통해 빅 데이터 클러스터를 관리 하는 Python 작성 됩니다. 필요한 최소 Python 버전 v3.5 됩니다. 또한 있어야 `pip` 다운로드 및 설치 하는 데 사용 되는 `mssqlctl` 도구입니다. Windows 클라이언트에서 필요한 Python 패키지를 다운로드할 수 있습니다 [ https://www.python.org/downloads/ ](https://www.python.org/downloads/)합니다. Python3.5.3 이상에서는 Python을 설치할 때는 pip3도 설치 됩니다. 설치할 때 설치 경로에 추가 작업을 선택할 수 없습니다. 다음은 pip3 있고 경로에 수동으로 추가 위치를 찾을 수 있습니다.
Linux (WSL 또는 Ubuntu 클라이언트 예를 들어)에서 이러한 명령을 3.5 최신 Python 및 pip 설치 됩니다.

```bash
sudo apt-get update
sudo apt-get install python3
sudo apt-get install python3-pip
sudo pip3 install --upgrade pip
```

> [!NOTE]
Python 설치를 사용할 수 없는 경우는 `requests` 패키지를 설치한 `requests` 사용 하 여 `python -m pip install requests`입니다. 이미 있는 경우는 `requests` 패키지 설치, 실행 하 여 최신 버전이 있는지 `python -m pip install requests --upgrade`합니다.

실행 된 아래 명령을 msqlctl를 설치 하려면:

```bash
pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl
```

## <a name="define-environment-variables"></a>환경 변수를 정의 합니다.

에 전달 되는 환경 변수 집합을 사용 하 여 클러스터 구성을 사용자 지정할 수는 `mssqlctl create cluster` 명령입니다. 대부분의 환경 변수는 아래 당 기본 avalues를 사용 하 여 선택적입니다. 사용자 입력을 요구 하는 자격 증명 같은 환경 변수는 note 합니다.

| 환경 변수 | 필수 | 기본값 | Description |
|---|---|---|---|
| **ACCEPT_EULA** | 사용자 계정 컨트롤 | 해당 사항 없음 | SQL Server 사용권 계약 (예: ' Y')에 동의 합니다.  |
| **CLUSTER_NAME** | 사용자 계정 컨트롤 | 해당 사항 없음 | Kubernetes 네임 스페이스에 SQLServer 빅 데이터 클러스터 배포의 이름입니다. |
| **CLUSTER_PLATFORM** | 사용자 계정 컨트롤 | 해당 사항 없음 | Kubernetes 클러스터가 배포 된 플랫폼입니다. 일 수 있습니다 `aks`, `minikube`, `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | 아니요 | 1 | 빌드할 계산 풀 복제본의 수입니다. CTP2.0 반환만 허용 되는 1입니다. |
| **CLUSTER_DATA_POOL_REPLICAS** | 아니요 | 2 | 풀 구축 하는 복제본에서 데이터의 수입니다. |
| **CLUSTER_STORAGE_POOL_REPLICAS** | 아니요 | 2 | 저장소 풀 복제본의 수입니다. |
| **DOCKER_REGISTRY** | 사용자 계정 컨트롤 | TBD | 클러스터를 배포 하는 데 사용 되는 이미지가 저장 된 개인 레지스트리입니다. |
| **DOCKER_REPOSITORY** | 사용자 계정 컨트롤 | TBD | 이미지가 저장 된 위의 레지스트리 내 개인 저장소.  것 필요한 것은 제어 된 체크 인된 공개 미리 보기 기간에 대 한 합니다. |
| **DOCKER_USERNAME** | 사용자 계정 컨트롤 | 해당 사항 없음 | 개인 저장소에 저장 됩니다 하는 경우 컨테이너 이미지에 액세스 하려면 사용자 이름입니다. 것 필요한 것은 제어 된 체크 인된 공개 미리 보기 기간에 대 한 합니다. |
| **DOCKER_PASSWORD** | 사용자 계정 컨트롤 | 해당 사항 없음 | 위의 개인 리포지토리에 액세스 하기 위한 암호입니다. 것 필요한 것은 제어 된 체크 인된 공개 미리 보기 기간에 대 한 합니다.|
| **DOCKER_EMAIL** | 사용자 계정 컨트롤 | 해당 사항 없음 | 위의 개인 리포지토리와 연결 된 전자 메일입니다. 것 필요한 것은 제어 된 체크 인된 비공개 미리 보기 기간에 대 한 합니다. |
| **DOCKER_IMAGE_TAG** | 아니요 | 최신 | 레이블 이미지 태그를 지정 하는 데 사용 합니다. |
| **DOCKER_IMAGE_POLICY** | 아니요 | 항상 | 이미지 끌어오기를 항상 강제로 적용 합니다.  |
| **DOCKER_PRIVATE_REGISTRY** | 사용자 계정 컨트롤 | 1 | 제어 된 체크 인된 공개 미리 보기 기간에 대 한이 값을 1로 설정 해야 합니다. |
| **CONTROLLER_USERNAME** | 사용자 계정 컨트롤 | 해당 사항 없음 | 클러스터 관리자의 사용자 이름입니다. |
| **CONTROLLER_PASSWORD** | 사용자 계정 컨트롤 | 해당 사항 없음 | 클러스터 관리자의 암호입니다. |
| **KNOX_PASSWORD** | 사용자 계정 컨트롤 | 해당 사항 없음 | Knox 사용자에 대 한 암호입니다. |
| **MSSQL_SA_PASSWORD** | 사용자 계정 컨트롤 | 해당 사항 없음 | 마스터 SQL 인스턴스 SA 사용자의 암호입니다. |
| **USE_PERSISTENT_VOLUME** | 아니요 | true | `true` Kubernetes 영구적 볼륨을 사용 하려면 pod 저장소에 대 한 클레임입니다.  `false` pod 저장소에 대 한 임시 호스트 저장소를 사용 하 합니다. 참조를 [데이터 지 속성](concept-data-persistence.md) 자세한 세부 정보에 대 한 항목입니다. 빅 데이터 클러스터 minikube를 SQL Server 및 USE_PERSISTENT_VOLUME를 배포 하는 경우 = true를 설정 해야 값 `STORAGE_CLASS_NAME=standard`합니다. |
| **STORAGE_CLASS_NAME** | 아니요 | 기본 | 하는 경우 `USE_PERSISTENT_VOLUME` 는 `true` 사용할 Kubernetes 저장소 클래스의 이름을 나타냅니다. 참조를 [데이터 지 속성](concept-data-persistence.md) 자세한 세부 정보에 대 한 항목입니다. SQL Server minikube의 빅 데이터 클러스터를 배포 하는 경우 기본 저장소 클래스 이름이 다릅니다 및 설정 하 여 재정의 해야 `STORAGE_CLASS_NAME=standard`합니다. |
| **MASTER_SQL_PORT** | 아니요 | 31433 | 마스터 SQL 인스턴스는 공용 네트워크에서 수신 대기 하는 TCP/IP 포트입니다. |
| **KNOX_PORT** | 아니요 | 30443 | Apache Knox 공용 네트워크에서 수신 대기 하는 TCP/IP 포트입니다. |
| **GRAFANA_PORT** | 아니요 | 30888 | 응용 프로그램 모니터링 Grafana 공용 네트워크에서 수신 대기 하는 TCP/IP 포트입니다. |
| **KIBANA_PORT** | 아니요 | 30999 | Kibana 로그 검색 응용 프로그램은 공용 네트워크에서 수신 대기 하는 TCP/IP 포트입니다. |



> [!IMPORTANT]
>1. 제한 된 비공개 미리 보기 기간에 대 한 개인 Docker 레지스트리에 대 한 자격 증명은 시 제공 해야 할 심사 하 [EAP 등록](https://aka.ms/eapsignup)합니다.
>1. 온-프레미스 클러스터의 kubeadm, 환경 변수 값을 사용 하 여 빌드한 `CLUSTER_PLATFORM` 는 `kubernetes`합니다. 또한, USE_PERSISTENT_STORAGE = true 인 경우 Kubernetes 저장소 클래스를 사전 프로 비전 하 고는 STORAGE_CLASS_NAME를 사용 하 여 통과 해야 합니다.
>1. 모든 특수 문자를 포함 하는 경우 큰따옴표로 암호를 배치 해야 합니다. 원하는 MSSQL_SA_PASSWORD를 설정할 수 있습니다 하지만 해야 충분히 복잡 하지 사용 하는 `!`, `&` 또는 `‘` 문자입니다. 큰따옴표로 구분 기호에만 작동 하는 bash 명령입니다.
>1. 클러스터의 이름에는 소문자 영숫자 문자만 공백 없이 이어야 합니다. 클러스터와 동일한 이름 가진 네임 스페이스의 클러스터에 대 한 모든 Kubernetes 아티팩트 (컨테이너, pod, 상태 집합, 서비스)를 만들 수는 지정 된 이름입니다.
>1. 합니다 **SA** 계정은 설치 중에 생성 되는 SQL Server Master 인스턴스의 시스템 관리자입니다. 실행 하 여 검색할 수는 SQL Server 컨테이너를 지정한 MSSQL_SA_PASSWORD 환경 변수 만들기 후 컨테이너에서 $MSSQL_SA_PASSWORD 에코 합니다. 보안상의 이유로 설명 된 모범 사례에 따라 SA 암호를 변경 [여기](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)합니다.

Windows 또는 Linux 클라이언트를 사용 하는 여부에 따라 달라 집니다 클러스터 Aris 배포에 필요한 환경 변수를 설정 합니다.  사용 중인 운영 체제에 따라 아래 단계를 선택 합니다.

다음 환경 변수를 초기화는 클러스터를 배포 하는 데 필요 합니다.

### <a name="windows"></a>Windows

창 (PowerShell이 아님), CMD를 사용 하 여 다음 환경 변수를 구성 합니다.

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name – can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instances>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username>
SET DOCKER_PASSWORD=<your password>
SET DOCKER_EMAIL=<your Docker email, use same as username provided>
SET DOCKER_PRIVATE_REGISTRY="1"
```

Minikube를에서 경우 USE_PERSISTENT_VOLUME = true (기본값) 이면 오른쪽 STORAGE_CLASS_NAME 환경 변수의 기본값도 해야 합니다.
```
SET STORAGE_CLASS_NAME=standard
```

또는 minikube에서 영구적 볼륨을 사용 하 여 비호환에 수행할 수 있습니다.
```
SET USE_PERSISTENT_VOLUME=false
```
### <a name="linux"></a>Linux

다음 환경 변수를 초기화 합니다.

```bash
export ACCEPT_EULA=Y
export CLUSTER_PLATFORM=<minikube or aks or kubernetes>

export CONTROLLER_USERNAME=<controller_admin_name – can be anything>
export CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
export KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
export MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instances>

export DOCKER_REGISTRY=private-repo.microsoft.com
export DOCKER_REPOSITORY=mssql-private-preview
export DOCKER_USERNAME=<your username>
export DOCKER_PASSWORD=<your password>
export DOCKER_EMAIL=<your Docker email, use same as username provided>
export DOCKER_PRIVATE_REGISTRY="1"
```

Minikube를에서 경우 USE_PERSISTENT_VOLUME = true (기본값) 이면 오른쪽 STORAGE_CLASS_NAME 환경 변수의 기본값도 해야 합니다.
```
SET STORAGE_CLASS_NAME=standard
```

또는 minikube에서 영구적 볼륨을 사용 하 여 비호환에 수행할 수 있습니다.
```
SET USE_PERSISTENT_VOLUME=false
```
## <a name="deploy-sql-server-big-data-cluster"></a>SQL Server에 대 한 빅 데이터 클러스터 배포

클러스터 만들기 API Kubernetes 네임 스페이스를 초기화 하 고 네임 스페이스에 모든 응용 프로그램 pod를 배포에 사용 됩니다. Kubernetes 클러스터에서 SQL Server에 대 한 빅 데이터 클러스터를 배포 하려면 다음 명령을 실행 합니다.

```bash
mssqlctl create cluster <name of your cluster>
```

클러스터 부트스트랩 하는 동안 클라이언트 명령 창 배포 상태 출력을 됩니다. 또한 다른 cmd 창에서 다음이 명령을 실행 하 여 배포 상태를 확인할 수 있습니다.

```bash
kubectl get all -n <name of your cluster>
kubectl get pods -n <name of your cluster>
kubectl get svc -n <name of your cluster>
```

보다 세부적인 상태 및 각 pod에 대 한 구성을 실행 하 여 확인할 수 있습니다.
```bash
kubectl describe pod <pod name> -n <name of your cluster>
```

컨트롤러 pod가 실행 되 면 배포를 모니터링 하려면 클러스터 관리 포털에서 배포 탭을 활용할 수 있습니다.

## <a id="masterip"></a> SQL Server 마스터 인스턴스와 SQL Server에 대 한 빅 데이터 클러스터 IP 주소 가져오기

배포 스크립트를 성공적으로 완료 된 후에 아래 설명 된 단계를 사용 하 여 SQL Server 마스터 인스턴스의 IP 주소를 얻을 수 있습니다. 이 IP 주소와 포트 번호 31433를 사용 하 여 SQL Server 마스터 인스턴스에 연결할 됩니다 (예:  **\<ip 주소\>31433,**). 마찬가지로, SQL Server 빅 데이터에 대 한 클러스터 IP입니다. 모든 클러스터 끝점은 클러스터 관리 포털에서 서비스 끝점 탭에 나와 있습니다. 배포를 모니터링 하려면 클러스터 관리 포털을 사용할 수 있습니다. 외부 IP 주소 및 포트 번호를 사용 하 여 포털에 액세스할 수 있습니다 합니다 `service-proxy-lb` (예: **https://\<ip 주소\>: 30777**). 값은 관리 포털 액세스에 대 한 자격 증명 `CONTROLLER_USERNAME` 고 `CONTROLLER_PASSWORD` 위에 제공 된 환경 변수입니다.

### <a name="aks"></a>AKS

AKS를 사용 하는 경우 Azure는 Azure 부하 분산 장치 서비스를 제공 합니다. 다음 명령을 실행 합니다.

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
kubectl get svc service-proxy-lb -n <name of your cluster>
```

검색할 합니다 **EXTERNAL-IP** 서비스에 할당 되는 값입니다. 그런 다음 포트 31433에서 IP 주소를 사용 하 여 SQL Server 마스터 인스턴스에 연결 (예:  **\<ip 주소\>, 31433**) 및 SQL Server에 대 한 빅 데이터 클러스터에 대 한 외부 IP를 사용 하 여 끝점 `service-security-lb` 서비스. 

### <a name="minikube"></a>Minikube

Minikube를 사용 하는 경우에 연결 해야 합니다. IP 주소를 가져오려면 다음 명령을 실행 해야 합니다. IP에 외에도 연결 해야 하는 끝점에 대 한 포트를 지정 합니다. 에 대 한 모든 서비스 끝점을 가져오려면 

```bash
minikube ip
```

플랫폼에 관계 없이 실행 하는 Kubernetes 클러스터에서 클러스터에 대해 실행 명령 다음에 배포 된 모든 서비스 끝점을 가져오려면:
```bash
kubectl get svc -n <name of your cluster>
```

## <a name="next-steps"></a>다음 단계

Kubernetes 클러스터 SQL Server에 대 한 빅 데이터를 성공적으로 배포한 [빅 데이터 도구를 설치](deploy-big-data-tools.md) 새로운 기능 중 일부를 사용 하 고 알아봅니다 [SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법을](notebooks-guidance.md)합니다.
