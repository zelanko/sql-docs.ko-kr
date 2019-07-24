---
title: 배포 지침
titleSuffix: SQL Server big data clusters
description: Kubernetes에서 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 배포 하는 방법에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e6f2eefd37c45753e3051722448b80d88712df26
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419414"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Kubernetes에서 SQL Server 빅 데이터 클러스터를 배포 하는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 빅 데이터 클러스터는 Kubernetes 클러스터에 docker 컨테이너로 배포 됩니다. 다음은 설치 및 구성 단계에 대 한 개요입니다.

- 단일 VM, Vm 클러스터 또는 AKS (Azure Kubernetes Service)에서 Kubernetes 클러스터를 설정 합니다.
- 클라이언트 컴퓨터에 **azdata** 클러스터 구성 도구를 설치 합니다.
- Kubernetes 클러스터에 SQL Server 빅 데이터 클러스터를 배포 합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>SQL Server 2019 빅 데이터 도구 설치

SQL Server 2019 빅 데이터 클러스터를 배포 하기 전에 먼저 [빅 데이터 도구를 설치 합니다](deploy-big-data-tools.md).

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 확장**

## <a id="prereqs"></a>Kubernetes 필수 구성 요소

빅 데이터 클러스터 SQL Server 서버 및 클라이언트 (kubectl) 모두에 대해 최소 Kubernetes 버전의 v 1.10이 필요 합니다.

> [!NOTE]
> 클라이언트 및 서버 Kubernetes 버전은 + 1 또는-1 부 버전 내에 있어야 합니다. 자세한 내용은 [Kubernetes 릴리스 정보 및 버전 기울이기 SKU 정책](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)을 참조 하세요.

### <a id="kubernetes"></a>Kubernetes 클러스터 설정

위의 필수 구성 요소를 충족 하는 Kubernetes 클러스터가 이미 있는 경우 [배포 단계로](#deploy)바로 건너뛸 수 있습니다. 이 섹션에서는 Kubernetes 개념을 기본적으로 이해 하 고 있다고 가정 합니다.  Kubernetes에 대 한 자세한 내용은 [Kubernetes 설명서](https://kubernetes.io/docs/home)를 참조 하세요.

다음 세 가지 방법 중 하나로 Kubernetes를 배포 하도록 선택할 수 있습니다.

| Kubernetes 배포 위치: | 설명 | 링크 |
|---|---|---|
| **AKS (Azure Kubernetes Services)** | Azure에서 관리 되는 Kubernetes container service. | [지침](deploy-on-aks.md) |
| **여러 컴퓨터 (kubeadm)** | **Kubeadm** 를 사용 하 여 실제 또는 가상 머신에 배포 된 Kubernetes 클러스터 | [지침](deploy-with-kubeadm.md) |
| **Minikube** | VM의 단일 노드 Kubernetes 클러스터. | [지침](deploy-on-minikube.md) |

> [!TIP]
> 한 번에 AKS 및 SQL Server 빅 데이터 클러스터를 모두 배포 하는 샘플 python 스크립트를 보려면 [빠른 시작: AKS (Azure Kubernetes Service)](quickstart-big-data-cluster-deploy.md)에 빅 데이터 클러스터 SQL Server 배포

### <a name="verify-kubernetes-configuration"></a>Kubernetes 구성 확인

**Kubectl** 명령을 실행 하 여 클러스터 구성을 확인 합니다. Kubectl가 올바른 클러스터 컨텍스트를 가리키고 있는지 확인 합니다.

```bash
kubectl config view
```

Kubernetes 클러스터를 구성한 후에는 새로운 SQL Server 빅 데이터 클러스터의 배포를 진행할 수 있습니다. 이전 릴리스에서 업그레이드 하는 경우 [빅 데이터 클러스터 SQL Server 업그레이드 하는 방법](deployment-upgrade.md)을 참조 하세요.

## <a id="deploy"></a>배포 개요

대부분의 빅 데이터 클러스터 설정은 JSON 배포 구성 파일에 정의 되어 있습니다. AKS, `kubeadm`또는 `minikube` 의 기본 배포 프로필을 사용 하거나, 설치 중에 사용할 고유한 배포 구성 파일을 사용자 지정할 수 있습니다. 보안상의 이유로 인증 설정은 환경 변수를 통해 전달 됩니다.

다음 섹션에서는 빅 데이터 클러스터 배포를 구성 하는 방법 및 일반적인 사용자 지정 예제에 대 한 자세한 정보를 제공 합니다. 또한 예를 들어 VS Code와 같은 편집기를 사용 하 여 사용자 지정 배포 구성 파일을 언제 든 지 편집할 수 있습니다.

## <a id="configfile"></a>기본 구성

빅 데이터 클러스터 배포 옵션은 JSON 구성 파일에 정의 되어 있습니다. 개발/테스트 환경에 대 한 기본 설정이 포함 된 세 가지 표준 배포 프로필이 있습니다.

| 배포 프로필 | Kubernetes 환경 |
|---|---|
| **aks-dev-test** | Azure Kubernetes 서비스 (AKS) |
| **kubeadm-dev-test** | 여러 컴퓨터 (kubeadm) |
| **minikube-dev-test** | Minikube |

**Azdata bdc create**를 실행 하 여 빅 데이터 클러스터를 배포할 수 있습니다. 기본 구성 중 하나를 선택 하 라는 메시지를 표시 한 다음 배포를 안내 합니다.

를 처음 실행할 `azdata` 때 EULA (최종 사용자 `--accept-eula` 사용권 계약)에 동의 하려면를 포함 해야 합니다.

```bash
azdata bdc create --accept-eula
```

이 시나리오에서는 기본 구성의 일부가 아닌 설정 (예: 암호)을 묻는 메시지가 표시 됩니다. 

> [!NOTE]
> 2019 CTP 3.2 SQL Server부터 빅 데이터 클러스터의 미리 보기 릴리스를 경험 하는 SQL Server 2019 [초기 채택 프로그램](https://aka.ms/eapsignup) 에 더 이상 소속 된 멤버가 없습니다.

> [!IMPORTANT]
> 빅 데이터 클러스터의 기본 이름은 **mssql-cluster**입니다. 이는 `-n` 매개 변수를 사용 하 여 Kubernetes 네임 스페이스를 지정 하는 **kubectl** 명령 중 하나를 실행 하기 위해 알고 있어야 합니다.

## <a id="customconfig"></a>사용자 지정 구성

또한 사용자 고유의 배포 구성 프로필을 사용자 지정할 수 있습니다. 다음 단계를 수행 하 여이 작업을 수행할 수 있습니다.

1. Kubernetes 환경과 일치 하는 표준 배포 프로필 중 하나를 사용 하 여 시작 합니다. **Azdata bdc config list** 명령을 사용 하 여이를 나열할 수 있습니다.

   ```bash
   azdata bdc config list
   ```

1. 배포를 사용자 지정 하려면 **azdata bdc config init** 명령을 사용 하 여 배포 프로필의 복사본을 만듭니다. 예를 들어 다음 명령은 라는 `custom`대상 디렉터리에 **aks** 배포 구성 파일의 복사본을 만듭니다.

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   azdata
   > 는 `--target` `--source` 매개 변수를 기반으로 하는 구성 파일, **cluster.exe 및** **컨트롤**을 포함 하는 디렉터리를 지정 합니다.

1. 배포 구성 프로필에서 설정을 사용자 지정 하려면 VS Code와 같이 JSON 파일을 편집 하는 데 적합 한 도구에서 배포 구성 파일을 편집할 수 있습니다. 스크립팅된 자동화의 경우 **azdata bdc config** 명령을 사용 하 여 사용자 지정 배포 프로필을 편집할 수도 있습니다. 예를 들어 다음 명령은 사용자 지정 배포 프로필을 변경 하 여 배포 된 클러스터의 이름을 기본값 (**mssql-cluster**)에서 **테스트-클러스터**로 변경 합니다.  

   ```bash
   azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
   ```

   > JSON 경로를 찾는 데 유용한 도구는 [JSONPath Online 계산기](https://jsonpath.com/)입니다.

   키-값 쌍을 전달 하는 것 외에도 인라인 JSON 값을 제공 하거나 JSON 패치 파일을 전달할 수 있습니다. 자세한 내용은 [빅 데이터 클러스터에 대 한 배포 설정 구성](deployment-custom-configuration.md)을 참조 하세요.

1. 그런 다음 사용자 지정 구성 파일을 **azdata bdc create**에 전달 합니다. 필요한 [환경 변수](#env)를 설정 해야 합니다. 그렇지 않으면 값을 입력 하 라는 메시지가 표시 됩니다.

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> 배포 구성 파일의 구조에 대 한 자세한 내용은 [배포 구성 파일 참조](reference-deployment-config.md)를 참조 하세요. 추가 구성 예제는 [빅 데이터 클러스터에 대 한 배포 설정 구성](deployment-custom-configuration.md)을 참조 하세요.

## <a id="env"></a>환경 변수

다음 환경 변수는 배포 구성 파일에 저장 되지 않은 보안 설정에 사용 됩니다. 자격 증명을 제외한 Docker 설정은 구성 파일에서 설정할 수 있습니다.

| 환경 변수 | 요구 사항 |설명 |
|---|---|---|
| **CONTROLLER_USERNAME** | 필수 |클러스터 관리자의 사용자 이름입니다. |
| **CONTROLLER_PASSWORD** | 필수 |클러스터 관리자의 암호입니다. |
| **MSSQL_SA_PASSWORD** | 필수 |SQL 마스터 인스턴스의 SA 사용자 암호입니다. |
| **KNOX_PASSWORD** | 필수 |Knox 사용자에 대 한 암호입니다. |
| **ACCEPT_EULA**| 처음 사용 하는 데 필요 합니다.`azdata`| 값이 필요 하지 않습니다. 환경 변수로 설정 되 면 EULA를 SQL Server 및 `azdata`에 모두 적용 합니다. 환경 변수로 설정 하지 않으면 첫 번째 `--accept-eula` `azdata` 명령 사용에를 포함할 수 있습니다.|
| **DOCKER_USERNAME** | Optional | 개인 리포지토리에 저장 된 경우 컨테이너 이미지에 액세스 하기 위한 사용자 이름입니다. 빅 데이터 클러스터 배포에 개인 Docker 리포지토리를 사용 하는 방법에 대 한 자세한 내용은 [오프 라인 배포](deploy-offline.md) 항목을 참조 하세요.|
| **DOCKER_PASSWORD** | Optional |위의 개인 리포지토리에 액세스 하는 데 사용할 암호입니다. |

**Azdata bdc create**를 호출 하기 전에 이러한 환경 변수를 설정 해야 합니다. 변수를 설정 하지 않으면 해당 변수를 입력 하 라는 메시지가 표시 됩니다.

다음 예제에서는 Linux (bash) 및 Windows (PowerShell)의 환경 변수를 설정 하는 방법을 보여 줍니다.

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
```

환경 변수를 설정한 후에는를 실행 `azdata bdc create` 하 여 배포를 트리거해야 합니다. 이 예제에서는 위에서 만든 클러스터 구성 프로필을 사용 합니다.

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

다음 지침에 유의 하세요.

- 특수 문자를 포함 하는 경우 암호를 큰따옴표로 묶어야 합니다. **MSSQL_SA_PASSWORD** 를 원하는 대로 설정할 수 있지만 `!`, 암호가 충분히 복잡 하 고, `&` 또는 `'` 문자를 사용 하지 않는지 확인 합니다. 큰따옴표 구분 기호는 bash 명령 에서만 작동 합니다.
- **SA** 로그인은 설치 중에 생성 되는 SQL Server 마스터 인스턴스의 시스템 관리자입니다. SQL Server 컨테이너를 만든 후에는  컨테이너에서를 실행 `echo $MSSQL_SA_PASSWORD` 하 여 지정한 MSSQL_SA_PASSWORD 환경 변수를 검색할 수 있습니다. 보안을 위해 [여기](../linux/quickstart-install-connect-docker.md#sapassword)에 설명 된 모범 사례에 따라 SA 암호를 변경 합니다.

## <a id="unattended"></a>무인 설치

무인 배포의 경우 모든 필수 환경 변수를 설정 하 고 구성 파일을 사용 하 고 `azdata bdc create` `--accept-eula yes` 매개 변수를 사용 하 여 명령을 호출 해야 합니다. 이전 섹션의 예제에서는 무인 설치를 위한 구문을 보여 줍니다.

## <a id="monitor"></a>배포 모니터링

클러스터 부트스트랩 중에 클라이언트 명령 창이 배포 상태를 출력 합니다. 배포 프로세스 중에 컨트롤러 pod를 대기 하는 일련의 메시지가 표시 됩니다.

```output
Waiting for cluster controller to start.
```

15 ~ 30 분 내에 컨트롤러 pod가 실행 중임을 알립니다.

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> 전체 배포는 빅 데이터 클러스터의 구성 요소에 대 한 컨테이너 이미지를 다운로드 하는 데 필요한 시간 때문에 시간이 오래 걸릴 수 있습니다. 그러나 몇 시간이 소요 되어서는 안 됩니다. 배포에 문제가 발생 하는 경우 [빅 데이터 클러스터 SQL Server 모니터링 및 문제 해결](cluster-troubleshooting-commands.md)을 참조 하세요.

배포가 완료 되 면 출력은 성공 여부를 알려 줍니다.

```output
Cluster deployed successfully.
```

> [!TIP]
> 배포 된 빅 데이터 클러스터의 기본 이름은 사용자 지정 `mssql-cluster` 구성에 의해 수정 되지 않은 경우입니다.

## <a id="endpoints"></a>끝점 검색

배포 스크립트가 성공적으로 완료 된 후에는 다음 단계를 사용 하 여 빅 데이터 클러스터에 대 한 외부 끝점의 IP 주소를 가져올 수 있습니다.

1. 배포 후 배포 표준 출력에서 또는 다음 **kubectl** 명령의 외부 ip 출력을 보면 컨트롤러 끝점의 IP 주소를 찾습니다.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 배포 하는 동안 기본 이름을 변경 하지 않은 경우에는 `-n mssql-cluster` 이전 명령을 사용 합니다. **mssql-cluster** 는 빅 데이터 클러스터의 기본 이름입니다.

1. [Azdata 로그인](reference-azdata.md)을 사용 하 여 빅 데이터 클러스터에 로그인 합니다. **--Controller-endpoint** 매개 변수를 컨트롤러 끝점의 외부 IP 주소로 설정 합니다.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   배포 하는 동안 컨트롤러에 대해 구성한 사용자 이름 및 암호 (CONTROLLER_USERNAME 및 CONTROLLER_PASSWORD)를 지정 합니다.

1. [Azdata bdc 끝점 목록을](reference-azdata-bdc-endpoint.md) 실행 하 여 각 끝점에 대 한 설명과 해당 IP 주소 및 포트 값이 포함 된 목록을 가져옵니다. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   다음 목록에서는이 명령의 샘플 출력을 보여 줍니다.

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

다음 **kubectl** 명령을 실행 하 여 클러스터에 대해 배포 된 모든 서비스 끝점을 가져올 수도 있습니다.

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

Minikube를 사용 하는 경우 다음 명령을 실행 하 여 연결 해야 하는 IP 주소를 가져와야 합니다. IP 외에도 연결 해야 하는 끝점에 대 한 포트를 지정 합니다.

```bash
minikube ip
```

## <a id="status"></a>클러스터 상태 확인

배포 후 [azdata bdc status show](reference-azdata-bdc-status.md) 명령을 사용 하 여 클러스터의 상태를 확인할 수 있습니다.

```bash
azdata bdc status show -o table
```

> [!TIP]
> 상태 명령을 실행 하려면 먼저 이전 끝점 섹션에 표시 된 **azdata login** 명령을 사용 하 여 로그인 해야 합니다.

다음은이 명령의 샘플 출력을 보여 줍니다.

```output
Kind     Name           State
-------  -------------  -------
BDC      mssql-cluster  Ready
Control  default        Ready
Master   default        Ready
Compute  default        Ready
Data     default        Ready
Storage  default        Ready
```

이 요약 상태에서 다음 명령을 사용 하 여 보다 자세한 상태를 가져올 수도 있습니다.

- [azdata bdc 컨트롤 상태](reference-azdata-bdc-control-status.md)
- [azdata bdc 풀 상태](reference-azdata-bdc-pool-status.md)

이러한 명령의 출력에는 자세한 분석을 위해 Kibana 및 Grafana 대시보드에 대 한 Url이 포함 되어 있습니다.

**Azdata**를 사용 하는 것 외에도 Azure Data Studio를 사용 하 여 끝점과 상태 정보를 모두 찾을 수 있습니다. **Azdata** 및 Azure Data Studio를 사용 하 여 클러스터 상태를 보는 방법에 대 한 자세한 내용은 [빅 데이터 클러스터의 상태를 보는 방법](view-cluster-status.md)을 참조 하세요.

## <a id="connect"></a>클러스터에 연결

빅 데이터 클러스터에 연결 하는 방법에 대 한 자세한 내용은 [Azure Data Studio를 사용 하 여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조 하세요.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에 대해 자세히 알아보려면 다음 리소스를 참조 하세요.

- [빅 데이터 클러스터에 대 한 배포 설정 구성](deployment-custom-configuration.md)
- [SQL Server 빅 데이터 클러스터의 오프 라인 배포 수행](deploy-offline.md)
- [걸친 빅 데이터 클러스터 아키텍처 Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
