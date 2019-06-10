---
title: 배포 지침
titleSuffix: SQL Server big data clusters
description: Kubernetes에서 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 배포 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 15cd412de1dda9d1245859c27d35a7c7f9f52710
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782246"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Kubernetes에서 SQL Server 빅 데이터 클러스터를 배포 하는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 빅 데이터 클러스터는 Kubernetes 클러스터에 docker 컨테이너로 배포 됩니다. 설치 및 구성 단계 개요는 다음과 같습니다.

- 단일 VM 또는 Azure Kubernetes Service (AKS)에서 Vm의 클러스터에서 Kubernetes 클러스터를 설정 합니다.
- 클러스터 구성 도구를 설치 **mssqlctl** 클라이언트 컴퓨터에 있습니다.
- Kubernetes 클러스터에서 SQL Server 빅 데이터 클러스터를 배포 합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>SQL Server 2019 빅 데이터 도구 설치

먼저 SQL Server 2019 빅 데이터 클러스터를 배포 하기 전에 [big data tools 설치](deploy-big-data-tools.md):

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 확장**

## <a id="prereqs"></a> Kubernetes 필수 구성 요소

SQL Server 빅 데이터 클러스터의 Kubernetes 버전을 이상이 필요 v1.10 서버 및 클라이언트 (kubectl)에 대 한 합니다.

> [!NOTE]
> 클라이언트와 서버가 Kubernetes 버전 + 1 또는-1 부 버전 내에 있어야 합니다. 이때 합니다. 자세한 내용은 [지원 되는 버전 및 구성 요소 기울이기 Kubernetes](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)합니다.

### <a id="kubernetes"></a> Kubernetes 클러스터 설치

위의 필수 구성 요소를 충족 하는 Kubernetes 클러스터가 이미 있는 경우 직접 건너뛸 수 있습니다 합니다 [배포 단계](#deploy)합니다. 이 섹션에서는 Kubernetes 개념의 기본 지식이 있다고 가정 합니다.  Kubernetes에 대 한 자세한 내용은 참조는 [Kubernetes 설명서](https://kubernetes.io/docs/home)합니다.

세 가지 방법 중 하나로 Kubernetes 배포를 선택할 수 있습니다.

| Kubernetes에 배포 합니다. | Description | 링크 |
|---|---|---|
| **Azure Kubernetes 서비스 (AKS)** | Azure의 관리 되는 Kubernetes 컨테이너 서비스입니다. | [지침](deploy-on-aks.md) |
| **여러 컴퓨터 (kubeadm)** | 물리적 컴퓨터 또는 가상 컴퓨터를 사용 하 여 배포 된 Kubernetes 클러스터의 **kubeadm** | [지침](deploy-with-kubeadm.md) |
| **Minikube** | VM에서 단일 노드 Kubernetes 클러스터입니다. | [지침](deploy-on-minikube.md) |

> [!TIP]
> AKS 및 빅 데이터를 한 번에에서 클러스터 된 SQL Server를 배포 하는 샘플 python 스크립트를 참조 하세요. [빠른 시작: 빅 데이터 클러스터 Azure Kubernetes Service (AKS)에서 SQL Server 배포](quickstart-big-data-cluster-deploy.md)합니다.

### <a name="verify-kubernetes-configuration"></a>Kubernetes 구성 확인

실행 합니다 **kubectl** 클러스터 구성을 보려면 명령입니다. 해당 kubectl 가리키는 올바른 클러스터 컨텍스트를 확인 합니다.

```bash
kubectl config view
```

Kubernetes 클러스터를 구성한 후에 새 SQL Server 빅 데이터 클러스터를 배포 하 여 진행할 수 있습니다. 이전 릴리스에서 업그레이드 하는 경우를 참조 하세요 [SQL Server 빅 데이터 클러스터를 업그레이드 하는 방법](deployment-upgrade.md)합니다.

## <a id="deploy"></a> 배포 개요

CTP 2.5 부터는 대부분의 빅 데이터 클러스터 설정은 JSON 배포 구성 파일에서 정의 됩니다. AKS, kubeadm에 대 한 기본 배포 프로필을 사용할 수 있습니다 하거나 minikube 하거나 설치 중에 사용할 고유한 배포 구성 파일을 사용자 지정할 수 있습니다. 보안상의 이유로 인증 설정 환경 변수를 통해 전달 됩니다.

다음 섹션에서는 빅 데이터를 구성 하는 방법에 대 한 자세한 내용은 클러스터 배포 뿐만 아니라 일반적인 사용자 지정의 예제를 제공 합니다. 또한 항상 VSCode 편집기를 사용 하 여 예를 들어 사용자 지정 배포 구성 파일을 편집할 수 있습니다.

## <a id="configfile"></a> 기본 구성

빅 데이터 클러스터 배포 옵션은 JSON 구성 파일에 정의 되어 있습니다. 개발/테스트 환경에 대 한 기본 설정 사용 하 여 세 개의 표준 배포 프로필 가지가 있습니다.

| 배포 프로필 | Kubernetes 환경 |
|---|---|
| **aks-dev-test.json** | AKS (azure Kubernetes Service) |
| **kubeadm-dev-test.json** | 여러 컴퓨터 (kubeadm) |
| **minikube-dev-test.json** | Minikube |

실행 하 여 빅 데이터 클러스터를 배포할 수 있습니다 **mssqlctl 클러스터 만들기**합니다. 다음 배포 과정을 기본 구성 중 하나를 선택 하 라는 메시지가 표시 됩니다.

```bash
mssqlctl cluster create
```

이 시나리오에서는 암호와 같은 기본 구성에 포함 되지 않는 모든 설정에 대 한 라는 메시지가 표시 됩니다. Docker 정보를 SQL Server 2019의 일부로 microsoft에 제공 되는 참고 [Early Adoption Program](https://aka.ms/eapsignup)합니다.

> [!IMPORTANT]
> 빅 데이터 클러스터의 기본 이름은 **mssql 클러스터**합니다. 이 실행 하기 위해 알아야 합니다 **kubectl** 명령을 사용 하 여 Kubernetes 네임 스페이스를 지정 하는 `-n` 매개 변수입니다.

## <a id="customconfig"></a> 사용자 지정 구성

고유한 배포 구성 파일 사용자 지정도 가능 합니다. 다음 단계를 사용 하 여이 수행할 수 있습니다.

1. Kubernetes 환경과 일치 하는 표준 배포 프로필 중 하나를 사용 하 여 시작 합니다. 사용할 수는 **mssqlctl 클러스터 구성 목록** 나열 하는 명령:

   ```bash
   mssqlctl cluster config list
   ```

1. 배포를 사용자 지정 하려면 사용 하 여 배포 프로필의 복사본을 만듭니다는 **mssqlctl 클러스터 구성 init** 명령입니다. 예를 들어 다음 명령은의 복사본을 만듭니다는 **aks-dev-test.json** 현재 디렉터리에 배포 구성 파일:

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

1. 배포 구성 파일에서 설정을 사용자 지정 하는 VS Code와 같은 json 문서를 편집 하기 위한 좋은 도구에서 편집할 수 있습니다. 자동화 스크립트를 편집할 수 있습니다 사용 하 여 사용자 지정 구성 파일 **mssqlctl 클러스터 구성 섹션 집합** 명령입니다. 예를 들어, 다음 명령을 변경 기본값에서 배포 된 클러스터의 이름을 변경 하려면 사용자 지정 구성 파일 (**mssql 클러스터**)를 **테스트 클러스터**:  

   ```bash
   mssqlctl cluster config section set --config-file custom.json --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > JSON 경로 찾는 데 유용한 도구를 [JSONPath 온라인 계산기](https://jsonpath.com/)합니다.

   키-값 쌍을 전달 하는 것 외에도 JSON 값 인라인을 제공 하거나 JSON 패치 파일을 전달할 수도 있습니다. 자세한 내용은 [빅 데이터 클러스터에 대 한 배포 설정을 구성](deployment-custom-configuration.md)합니다.

1. 사용자 지정 구성 파일을 전달한 **mssqlctl 클러스터 만들기**합니다. 필수 설정 해야 합니다 [환경 변수](#env), 그렇지 않으면 메시지가 표시 됩니다 값:

   ```bash
   mssqlctl cluster create --config-file custom.json --accept-eula yes
   ```

> [!TIP]
> 배포 구성 파일의 구조에 대 한 자세한 내용은 참조는 [배포 구성 파일 참조](reference-deployment-config.md)합니다. 자세한 구성 예제를 참조 하세요 [빅 데이터 클러스터에 대 한 배포 설정을 구성](deployment-custom-configuration.md)합니다.

## <a id="env"></a> 환경 변수

다음 환경 변수는 배포 구성 파일에 저장 되지 않은 보안 설정에 사용 됩니다. 자격 증명을 제외 하 고 Docker 설정 구성 파일에서 설정할 수 있는 참고 합니다.

| 환경 변수 | Description |
|---|---|---|---|
| **DOCKER_USERNAME** | 개인 저장소에 저장 됩니다 하는 경우 컨테이너 이미지에 액세스 하려면 사용자 이름입니다. |
| **DOCKER_PASSWORD** | 위의 개인 리포지토리에 액세스 하기 위한 암호입니다. |
| **CONTROLLER_USERNAME** | 클러스터 관리자의 사용자 이름입니다. |
| **CONTROLLER_PASSWORD** | 클러스터 관리자의 암호입니다. |
| **KNOX_PASSWORD** | Knox 사용자에 대 한 암호입니다. |
| **MSSQL_SA_PASSWORD** | 마스터 SQL 인스턴스 SA 사용자의 암호입니다. |

이러한 환경 변수를 호출 하기 전에 설정 해야 합니다 **mssqlctl 클러스터 만들기**합니다. 모든 변수를 설정 하지 않으면 해당 메시지가 표시 됩니다.

다음 예제에서는 Linux (bash) 및 Windows (PowerShell)에 대 한 환경 변수를 설정 하는 방법을 보여 줍니다.

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
export DOCKER_USERNAME=<docker-username>
export DOCKER_PASSWORD=<docker-password>
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
SET DOCKER_USERNAME=<docker-username>
SET DOCKER_PASSWORD=<docker-password>
```

환경 변수를 설정에 따라 실행 해야 `mssqlctl cluster create` 배포를 트리거하도록 합니다. 이 예제에서는 위에서 만든 클러스터 구성 파일을 사용 합니다.

```
mssqlctl cluster create --config-file custom.json --accept-eula yes
```

다음 지침을 note 하십시오.

- 이때 개인 Docker 레지스트리에 대 한 자격 증명 됩니다 시 제공 해야 할 심사 하 [Early Adoption Program 등록](https://aka.ms/eapsignup)합니다. SQL Server 빅 데이터 클러스터를 테스트 하려면 초기 Adoption Program 등록이 필요 합니다.
- 모든 특수 문자를 포함 하는 경우 큰따옴표로 암호를 배치 해야 합니다. 설정할 수 있습니다 합니다 **MSSQL_SA_PASSWORD** 하 무엇이 든 처럼 있지만 암호가 충분히 복잡 한 인지 확인을 사용 하지는 `!`를 `&` 또는 `'` 문자입니다. 큰따옴표로 구분 기호에만 작동 하는 bash 명령입니다.
- 합니다 **SA** 가 설치 중에 생성 되는 SQL Server 마스터 인스턴스에서 시스템 관리자에 로그인 합니다. SQL Server 컨테이너를 만든 후 합니다 **MSSQL_SA_PASSWORD** 지정한 환경 변수를 실행 하 여 검색할 수 $MSSQL_SA_PASSWORD 컨테이너에 출력 합니다. 보안상의 이유로 설명 된 모범 사례에 따라 SA 암호를 변경 [여기](../linux/quickstart-install-connect-docker.md#sapassword)합니다.

## <a id="unattended"></a> 무인된 설치

무인 배포의 경우 모든 필수 환경 변수, 구성 파일을 사용 및 호출을 설정 해야 합니다 `mssqlctl cluster create` 명령과 `--accept-eula yes` 매개 변수입니다. 이전 섹션의 예제에서는 무인된 설치에 대 한 구문을 보여 줍니다.

## <a id="monitor"></a> 배포 모니터링

클러스터 부트스트랩 하는 동안 클라이언트 명령 창에는 배포 상태를 출력 합니다. 배포 과정에서 컨트롤러 pod에 대 한 기다리고 있는 일련의 메시지를 표시 됩니다.

```output
2019-04-12 14:40:10.0129 UTC | INFO | Waiting for controller pod to be up...
```

15 ~ 30 분 이내에 있습니다 알려야 컨트롤러 pod가 실행 중인지:

```output
2019-04-12 15:01:10.0809 UTC | INFO | Waiting for controller pod to be up. Checkthe mssqlctl.log file for more details.
2019-04-12 15:01:40.0861 UTC | INFO | Controller pod is running.
2019-04-12 15:01:40.0884 UTC | INFO | Controller Endpoint: https://<ip-address>:30080
```

> [!IMPORTANT]
> 전체 배포는 빅 데이터 클러스터의 구성 요소에 대 한 컨테이너 이미지를 다운로드 하는 데 필요한 시간 때문에 시간이 걸릴 수 있습니다. 그러나 하지 몇 시간이 걸립니다. 배포 문제가 발생 하는 경우 참조 [모니터링 및 SQL Server 빅 데이터 클러스터 문제 해결](cluster-troubleshooting-commands.md)합니다.

배포가 완료 되 면 출력 성공 하면 알립니다.

```output
2019-04-12 15:37:18.0271 UTC | INFO | Monitor and track your cluster at the Portal Endpoint: https://<ip-address>:30777/portal/
2019-04-12 15:37:18.0271 UTC | INFO | Cluster deployed successfully.
```

URL을 확인 합니다 **포털 끝점** 다음 섹션에서 사용 하기 위해 이전 출력에 있습니다.

> [!TIP]
> 배포 된 빅 데이터 클러스터에 대 한 기본 이름은 `mssql-cluster` 사용자 지정 구성에서 수정 하지 않는 한 합니다.

## <a id="endpoints"></a> 끝점 검색

배포 스크립트를 성공적으로 완료 된 후에 다음 단계를 사용 하 여 빅 데이터 클러스터에 대 한 외부 끝점의 IP 주소를 가져올 수 있습니다.

1. 배포 후 다음의 외부 IP 출력을 보면 컨트롤러 끝점의 IP 주소를 찾으려면 **kubectl** 명령:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 사용 하 여 배포 하는 동안 기본 이름을 변경 하지 않은, 경우 `-n mssql-cluster` 이전 명령에서. **mssql 클러스터** 빅 데이터 클러스터에 대 한 기본 이름입니다.

1. 사용 하 여 빅 데이터 클러스터에 로그인 **mssqlctl 로그인**합니다. 설정 된 **-컨트롤러 끝점** 컨트롤러 끝점의 외부 IP 주소 매개 변수입니다.

   ```bash
   mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   배포 하는 동안 사용자 이름 및 컨트롤러 (CONTROLLER_USERNAME 및 CONTROLLER_PASSWORD)에 대해 구성한 암호를 지정 합니다.

1. 실행할 **mssqlctl 클러스터 끝점 목록** 각 끝점 및 해당 IP 주소 및 포트 값에 대 한 설명 사용 하 여 목록을 가져올 수 있습니다. 

   ```bash
   mssqlctl cluster endpoint list
   ```

   다음은이 명령의 샘플 출력을 보여 줍니다.

   ```output
   Name               Description                                             Endpoint                                                   Ip              Port    Protocol
   -----------------  ------------------------------------------------------  ---------------------------------------------------------  --------------  ------  ----------
   gateway            Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  30443   https
   spark-history      Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  30443   https
   yarn-ui            Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  30443   https
   app-proxy          Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  30778   https
   management-proxy   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  30777   https
   portal             Management Portal                                       https://11.111.111.111:30777/portal                        11.111.111.111  30777   https
   log-search-ui      Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  30777   https
   metrics-ui         Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  30777   https
   controller         Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  30080   https
   sql-server-master  SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  31433   tcp
   webhdfs            HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  30443   https
   livy               Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  30443   https
   ```

### <a name="minikube"></a>Minikube

Minikube를 사용 하는 경우에 연결 해야 합니다. IP 주소를 가져오려면 다음 명령을 실행 해야 합니다. IP에 외에도 연결 해야 하는 끝점에 대 한 포트를 지정 합니다.

```bash
minikube ip
```

플랫폼에 관계 없이 실행 하는 Kubernetes 클러스터에서 클러스터에 대해 실행 명령 다음에 배포 된 모든 서비스 끝점을 가져오려면:

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

## <a id="connect"></a> 클러스터에 연결

빅 데이터 클러스터에 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [Azure Data Studio를 사용 하 여 빅 데이터 클러스터를 SQL Server에 연결](connect-to-big-data-cluster.md)합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [빅 데이터 클러스터에 대 한 배포 설정을 구성 합니다.](deployment-custom-configuration.md)
- [SQL Server 빅 데이터 클러스터를 오프 라인 배포를 수행 합니다.](deploy-offline.md)
- [워크숍: Microsoft SQL Server 빅 데이터 클러스터 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
