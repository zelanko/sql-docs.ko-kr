---
title: SQL Server 빅 데이터 클러스터 배포 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: quickstart
ms.prod: sql
ms.openlocfilehash: 839823f9336a09b0790ee41b74793e548742c1d5
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49384108"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>빠른 시작: Azure Kubernetes Service (AKS)에서 SQL Server 빅 데이터 클러스터 배포

AKS에서 개발/테스트 환경에 적합 한 기본 구성에서는 SQL Server 빅 데이터 클러스터를 설치 합니다. SQL Master 인스턴스 외에 클러스터 풀 인스턴스를 하나의 계산, 데이터 풀 인스턴스 하나 및 두 개의 저장소 풀 인스턴스를 포함합니다. 데이터는 AKS 기본 저장소 클래스를 사용 하는 Kubernetes 영구적 볼륨을 사용 하 여 유지 됩니다. 추가 사용자 지정 구성에서 환경 변수를 참조 하세요 [배포 가이드](deployment-guidance.md)합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>필수 구성 요소

이 빠른 시작이에서는 이미 v1.10의 최소 버전을 사용 하 여 AKS 클러스터를 구성한 필요 합니다. 자세한 내용은 참조는 [AKS에 배포](deploy-on-aks.md) 가이드입니다.

SQL Server 빅 데이터 클러스터를 설치 하는 명령을 실행 하는 데 사용할 컴퓨터에 설치할 [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)합니다. SQL Server 빅 데이터 클러스터에 kubernetes, 서버 및 클라이언트 (kubectl)에 대 한 1.10 이상이 필요합니다. Kubectl을 설치 하려면 [kubectl 설치](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl)합니다. 

설치 합니다 `mssqlctl` CLI 도구는 SQL Server 빅 데이터를 관리 하려면 클라이언트 컴퓨터에서 클러스터를 먼저 설치 해야 합니다 [Python](https://www.python.org/downloads/) 최소 버전 v3.0 및 [pip3](https://pip.pypa.io/en/stable/installing/)합니다. `pip` 다운로드 하는 3.4 이상의 Python 버전을 사용 하는 경우 이미 설치 되어 [python.org](https://www.python.org/)합니다.

Python 설치를 사용할 수 없는 경우는 `requests` 패키지를 설치한 `requests` 사용 하 여 `python -m pip install requests`입니다. 이미 있는 경우는 `requests` 패키지를 사용 하 여 최신 버전으로 업그레이드 `python -m pip install requests --upgrade`합니다.

## <a name="verify-aks-configuration"></a>AKS 구성 확인

배포 된 AKS 클러스터를 만든 후 실행할 수는 아래 클러스터 구성을 보려면 kubectl 명령을 합니다. 해당 kubectl 가리키는 올바른 클러스터 컨텍스트를 확인 합니다.

```bash
kubectl config view
```

## <a name="install-mssqlctl-cli-management-tool"></a>Mssqlctl CLI 관리 도구 설치

설치를 알아보려면 아래 명령의 실행 `mssqlctl` 클라이언트 컴퓨터에 도구입니다. Windows 및 Linux 클라이언트에서 명령이 작동 하지만 Windows에서 관리자 권한으로 실행 되는 cmd 창에서 실행 되는지 또는 앞에 접두사를 사용 하 여 `sudo` on Linux:

```
pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl  
```

## <a name="define-environment-variables"></a>환경 변수를 정의 합니다.

Windows 또는 Linux/macOS 클라이언트 사용 하는지에 따라 달라 집니다 약간 빅 데이터 클러스터를 배포 하는 데 필요한 환경 변수를 설정 합니다.  사용 중인 운영 체제에 따라 아래 단계를 선택 합니다.

계속 하기 전에 다음 중요 한 지침을 note:

- 에 [명령 창](http://docs.microsoft.com/visualstudio/ide/reference/command-window), 따옴표 환경 변수에 포함 됩니다. 따옴표를 사용 하 여 암호를 래핑할 경우 큰따옴표는 암호에 포함 됩니다.
- Bash에서 따옴표 변수에 포함 되지 않습니다. 큰따옴표를 사용 하는 예제 `"`합니다.
- 원하는에 환경 변수는 암호를 설정할 수는 있지만 해야 속도가 충분히 복잡 한 사용 하지 않는 합니다 `!`, `&`, 또는 `'` 문자입니다.
- CTP 2.0 릴리스에 대 한 기본 포트를 변경 하지 마세요.
- `sa` 계정은 설치 중에 생성 되는 SQL Server Master 인스턴스의 시스템 관리자입니다. SQL Server 컨테이너를 만든 후 컨테이너에서 `echo $MSSQL_SA_PASSWORD`를 실행하여 지정한 `MSSQL_SA_PASSWORD` 환경 변수를 검색할 수 있습니다. 보안상의 이유로 변경 프로그램 `sa` 설명 된 모범 사례에 따라 암호 [여기](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password)합니다.

다음 환경 변수를 초기화 합니다.  빅 데이터 클러스터를 배포 하는 데 필요 합니다.

### <a name="windows"></a>Windows

명령 창 (PowerShell)를 사용 하면 다음 환경 변수를 구성할:

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=aks

SET CONTROLLER_USERNAME=<controller_admin_name – can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username, credentials provided by Microsoft>
SET DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
SET DOCKER_EMAIL=<your Docker email, use the username provided by Microsoft>
SET DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="linuxmacos"></a>Linux/macOS

다음 환경 변수를 초기화 합니다.

```bash
export ACCEPT_EULA="Y"
export CLUSTER_PLATFORM="aks"

export CONTROLLER_USERNAME="<controller_admin_name – can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password – can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password – can be anything, password complexity compliant>"
export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="<your username, credentials provided by Microsoft>"
export DOCKER_PASSWORD="<your password, credentials provided by Microsoft>"
export DOCKER_EMAIL="<your Docker email, use the username provided by Microsoft>"
export DOCKER_PRIVATE_REGISTRY="1"
```

> [!NOTE]
> 제한 된 공개 미리 보기 동안 SQL Server에 대 한 빅 데이터 클러스터 이미지 다운로드를 위해 Docker 자격 증명은 Microsoft에서 각 고객에 게 제공 됩니다. 액세스를 요청 하려면 등록 [여기](https://aka.ms/eapsignup), SQL Server 빅 데이터 클러스터를 시도 하려면 관심을 가져를 지정 합니다.

## <a name="deploy-a-big-data-cluster"></a>빅 데이터 클러스터를 배포 합니다.

Kubernetes 클러스터에서 SQL Server 2019 CTP 2.0 빅 데이터 클러스터를 배포 하려면 다음 명령을 실행 합니다.

```bash
mssqlctl create cluster <name of your cluster>
```

> [!NOTE]
> 클러스터의 이름을 소문자 영숫자 문자, 공백 없이 해야 합니다. 클러스터와 동일한 이름 가진 네임 스페이스의 빅 데이터 클러스터에 대 한 모든 Kubernetes 아티팩트를 만들 수는 지정 된 이름입니다.


명령 창 또는 셸에서 배포 상태를 반환합니다. 또한 다른 cmd 창에서 다음이 명령을 실행 하 여 배포 상태를 확인할 수 있습니다.

```bash
kubectl get all -n <name of your cluster>
kubectl get pods -n <name of your cluster>
kubectl get svc -n <name of your cluster>
```

보다 세부적인 상태 및 각 pod에 대 한 구성을 실행 하 여 확인할 수 있습니다.
```bash
kubectl describe pod <pod name> -n <name of your cluster>
```

컨트롤러 pod가 실행 되 면 배포를 모니터링 하려면 클러스터 관리 포털을 사용할 수 있습니다. 외부 IP 주소 및 포트 번호를 사용 하 여 포털에 액세스할 수 있습니다 합니다 `service-proxy-lb` (예: **https://\<ip 주소\>: 30777**). 값은 관리 포털 액세스에 대 한 자격 증명 `CONTROLLER_USERNAME` 고 `CONTROLLER_PASSWORD` 위에 제공 된 환경 변수입니다.

Bash 또는 cmd 창에서이 명령을 실행 하 여 lb-프록시 서비스-서비스의 IP 주소를 가져올 수 있습니다.

```bash
kubectl get svc service-proxy-lb -n <name of your cluster>
```

> [!NOTE]
> 자동으로 생성 된 SSL 인증서 사용 하므로 웹 페이지에 액세스할 때 보안 경고가 나타납니다. 향후 릴리스에서 자체 서명 된 인증서를 제공 하는 기능을 제공 합니다 했습니다.
 

## <a name="connect-to-the-big-data-cluster"></a>빅 데이터 클러스터에 연결

배포 스크립트를 성공적으로 완료 된 후에 SQL Server 마스터 인스턴스와 아래 설명 된 단계를 사용 하 여 Spark/HDFS 끝점의 IP 주소를 얻을 수 있습니다. 모든 클러스터 끝점도 쉽게 참조할 수 있도록에 대 한 클러스터 관리 포털에서 서비스 끝점 섹션에 표시 됩니다.

Azure는 AKS에 Azure 부하 분산 장치 서비스를 제공합니다. 다음 명령을 cmd에서 실행할지 bash 창:

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
```

검색할 합니다 **EXTERNAL-IP** 서비스에 할당 되는 값입니다. 에 대 한 IP 주소를 사용 하 여 SQL Server 마스터 인스턴스에 연결할 합니다 `service-master-pool-lb` 31433 포트 (예:  **\<ip 주소\>31433,**) 및에 대 한 외부 IP를 사용 하 여 SQL Server 빅 데이터 클러스터 끝점에는 `service-security-lb` 서비스입니다.   빅 데이터 클러스터 끝점은 HDFS와 상호 작용 하 고 Knox 통해 Spark 작업을 제출할 수 있는 됩니다.

## <a name="sample-deployment-script"></a>샘플 배포 스크립트

AKS와 SQL Server 빅 데이터 클러스터를 배포 하는 샘플 python 스크립트를 참조 하세요 [빅 데이터 클러스터 Azure Kubernetes Service (AKS)에서 SQL Server 배포](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks)합니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터를 배포 했으므로 새 기능 중 일부를 사용해 보세요.

> [!div class="nextstepaction"]
> [SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법](notebooks-guidance.md)
