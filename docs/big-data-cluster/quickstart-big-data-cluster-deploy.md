---
title: python 스크립트를 사용하여 배포
titleSuffix: SQL Server Big Data Clusters
description: 배포 스크립트를 사용하여 AKS(Azure Kubernetes Service)에 SQL Server 빅 데이터 클러스터를 배포하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 052e3794fa058ec988160855123c5b0993f3fbd4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85699830"
---
# <a name="use-a-python-script-to-deploy-a-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>python 스크립트를 사용하여 AKS(Azure Kubernetes Service)에 SQL Server 빅 데이터 클러스터 배포

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 자습서에서는 샘플 python 배포 스크립트를 사용하여 AKS(Azure Kubernetes Service)에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)](미리 보기)를 배포합니다.

> [!TIP]
> AKS는 빅 데이터 클러스터를 위해 Kubernetes를 호스트하는 옵션 중 하나일 뿐입니다. 다른 배포 옵션 및 배포 옵션을 사용자 지정하는 방법에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)을 참조하세요.

여기서 사용하는 기본 빅 데이터 클러스터 배포는 SQL 마스터 인스턴스 1개, 컴퓨팅 풀 인스턴스 1개, 데이터 풀 인스턴스 2개, 스토리지 풀 인스턴스 2개로 구성되어 있습니다. 데이터는 AKS 기본 스토리지 클래스를 사용하는 Kubernetes 영구적 볼륨을 사용하여 유지됩니다. 이 자습서에서 사용하는 기본 구성은 개발/테스트 환경에 적합합니다.

## <a name="prerequisites"></a>사전 요구 사항

- Azure 구독
- [빅 데이터 도구](deploy-big-data-tools.md):
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **Azure CLI**

## <a name="log-in-to-your-azure-account"></a>Azure 계정에 로그인

스크립트는 Azure CLI을 사용하여 AKS 클러스터 생성을 자동화합니다. 스크립트를 실행하기 전에 Azure CLI를 사용하여 Azure 계정에 한 번 이상 로그인해야 합니다. 명령 프롬프트에서 다음 명령을 실행합니다.

```
az login
```

## <a name="download-the-deployment-script"></a>배포 스크립트 다운로드

이 자습서에서는 python 스크립트 **deploy-sql-big-data-aks.py**를 사용하여 AKS에서 빅 데이터 클러스터 생성을 자동화합니다. **azdata**용 python을 이미 설치한 경우, 이 자습서의 스크립트를 성공적으로 실행할 수 있습니다. 

Windows PowerShell 또는 Linux bash 프롬프트에서 다음 명령을 실행하여 GitHub에서 배포 스크립트를 다운로드합니다.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>배포 스크립트 실행

다음 단계를 사용하여 Windows PowerShell 또는 Linux bash 프롬프트에서 배포 스크립트를 실행합니다. 이 스크립트는 Azure에서 AKS 서비스를 만든 다음, AKS에 SQL Server 2019 빅 데이터 클러스터를 배포합니다. 다른 [환경 변수](deployment-guidance.md#configfile)로 스크립트를 수정하여 사용자 지정 배포를 만들 수도 있습니다.

1. 다음 명령을 사용하여 스크립트를 실행합니다.

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > 클라이언트 머신 및 경로에 python3과 python2가 모두 있는 경우 python3을 사용해서 명령을 실행해야 합니다. `python3 deploy-sql-big-data-aks.py`

1. 메시지가 표시되면 다음 정보를 입력합니다.

   | 값 | Description |
   |---|---|
   | **Azure 구독 ID** | AKS에 사용할 Azure 구독 ID입니다. 다른 명령줄에서 `az account list`를 실행하여 모든 구독과 해당 ID를 나열할 수 있습니다. |
   | **Azure 리소스 그룹** | AKS 클러스터에 대해 만들 Azure 리소스 그룹 이름입니다. |
   | **Azure 지역** | 새 AKS 클러스터의 Azure 지역입니다(기본값 **westus**). |
   | **머신 크기** | AKS 클러스터의 노드에 사용할 [머신 크기](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)입니다(기본값 **Standard_L8s**). |
   | **작업자 노드** | AKS 클러스터의 작업자 노드 수입니다(기본값 **1**). |
   | **클러스터 이름** | AKS 클러스터와 빅 데이터 클러스터 둘 다의 이름입니다. 빅 데이터 클러스터 이름은 소문자 영숫자여야 하고 공백을 포함하지 않아야 합니다. (기본값 **sqlbigdata**). |
   | **암호** | 컨트롤러, HDFS/Spark 게이트웨이 및 마스터 인스턴스의 암호입니다(기본값 **MySQLBigData2019**). |
   | **사용자 이름** | 컨트롤러 사용자의 사용자 이름입니다(기본값 **admin**). |

   > [!IMPORTANT]
   > 일부 Azure 지역에서는 기본 머신 크기인 **Standard_L8s**를 사용하지 못할 수도 있습니다. 다른 머신 크기를 선택하는 경우 클러스터의 노드에서 연결할 수 있는 총 디스크 수가 24개 이상인지 확인합니다. 클러스터의 영구적 볼륨 클레임마다 연결된 디스크 1개가 필요합니다. 현재, 빅 데이터 클러스터에는 24개의 영구적 볼륨 클레임이 필요합니다. 예를 들어 [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/lsv2-series) 머신 크기는 32개의 연결된 디스크를 지원하기 때문에 이 머신 크기의 단일 노드에서 빅 데이터 클러스터를 평가할 수 있습니다.

   > [!NOTE]
   > 빅 데이터 클러스터 배포 중에는 SQL Server `sa` 계정을 사용할 수 없습니다. 새 sysadmin 로그인은 **사용자 이름** 입력에 지정된 것과 동일한 이름과 **암호** 입력에 해당하는 암호로 SQL Server 마스터 인스턴스에 프로비저닝됩니다. 컨트롤러 관리 사용자를 프로비저닝하는 데 동일한 **사용자 이름** 및 **암호** 값이 사용됩니다. SQL Server 2019 CU5 이전에 배포된 클러스터에서 게이트웨이(Knox)에 지원되는 유일한 사용자는 **루트**이며 암호는 위와 동일합니다.
   >[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

1. 스크립트는 먼저 지정된 매개 변수를 사용하여 AKS 클러스터를 만듭니다. 이 단계는 몇 분 정도 걸립니다.

## <a name="monitor-the-status"></a>상태 모니터링

AKS 클러스터를 만든 후에 스크립트는 앞서 지정된 설정을 사용하여 필요한 환경 변수를 설정합니다. 그런 다음, **azdata**를 호출하여 AKS에 빅 데이터 클러스터를 배포합니다.

클라이언트 명령 창에 배포 상태가 출력됩니다. 배포 프로세스 중에 컨트롤러 Pod를 대기 중이라는 일련의 메시지가 표시됩니다.

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

10~20분 후에 컨트롤러 Pod가 실행되고 있다는 알림이 표시됩니다.

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> 빅 데이터 클러스터 구성 요소의 컨테이너 이미지를 다운로드하는 데 필요한 시간 때문에 전체 배포는 시간이 오래 걸릴 수 있습니다. 그러나 몇 시간이 걸리면 안 됩니다. 배포에 문제가 있는 경우 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 모니터링 및 문제 해결](cluster-troubleshooting-commands.md)을 참조하세요.

## <a name="inspect-the-cluster"></a>클러스터 검사

배포 중에 언제든지 **kubectl** 또는 **azdata**를 사용하여 실행 중인 빅 데이터 클러스터의 상태 및 세부 정보를 검사할 수 있습니다.

### <a name="use-kubectl"></a>kubectl 사용

배포 프로세스 중에 **kubectl**을 사용하기 위해 새 명령 창을 엽니다.

1. 다음 명령을 실행하여 전체 클러스터의 상태 요약을 가져옵니다.

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 빅 데이터 클러스터 이름을 변경하지 않은 경우 스크립트는 기본적으로 **sqlbigdata**로 설정됩니다.

1. 다음 **kubectl** 명령을 사용하여 Kubernetes 서비스와 내부 및 외부 엔드포인트를 검사합니다.

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. 다음 명령을 사용하여 Kubernetes Pod의 상태를 검사할 수도 있습니다.

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. 다음 명령을 사용하여 특정 Pod에 대한 자세한 정보를 확인합니다.

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> 배포를 모니터링하고 문제를 해결하는 방법에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 모니터링 및 문제 해결](cluster-troubleshooting-commands.md)을 참조하세요.

## <a name="connect-to-the-cluster"></a>클러스터에 연결

배포 스크립트가 완료되면 출력에 성공 알림이 표시됩니다.

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

SQL Server 빅 데이터 클러스터가 AKS에 배포되었습니다. 이제 Azure Data Studio를 사용하여 클러스터에 연결할 수 있습니다. 자세한 내용은 [Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조하세요.

## <a name="clean-up"></a>정리

Azure에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 테스트하는 경우 예기치 않은 요금이 청구되지 않도록, 작업이 완료되면 AKS 클러스터를 삭제해야 합니다. 계속 사용하려는 경우에는 클러스터를 제거하지 않습니다.

> [!WARNING]
> 다음 단계에서는 AKS 클러스터를 삭제하며, 따라서 SQL Server 빅 데이터 클러스터도 제거됩니다. 유지하려는 데이터베이스 또는 HDFS 데이터가 있는 경우 클러스터를 삭제하기 전에 해당 데이터를 백업합니다.

다음 Azure CLI 명령을 실행하여 Azure에서 빅 데이터 클러스터 및 AKS 서비스를 제거합니다(`<resource group name>`을 배포 스크립트에서 지정한 **Azure 리소스 그룹**으로 바꿈).

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>다음 단계

배포 스크립트는 Azure Kubernetes Service를 구성하고 SQL Server 2019 빅 데이터 클러스터도 배포했습니다. 수동 설치를 통해 이후 배포를 사용자 지정할 수도 있습니다. 빅 데이터 클러스터를 배포하는 방법 및 배포를 사용자 지정하는 방법에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)을 참조하세요.

이제 SQL Server 빅 데이터 클러스터가 배포되었으므로 샘플 데이터를 로드하고 자습서를 살펴볼 수 있습니다.

> [!div class="nextstepaction"]
> [자습서: SQL Server 2019 빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)
