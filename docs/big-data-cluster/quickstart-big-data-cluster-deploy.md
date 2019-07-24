---
title: 배포 스크립트
titleSuffix: SQL Server big data clusters
description: AKS (Azure Kubernetes Service)에서 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 배포를 연습 합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ff1ec3672fbcf101d98ad30913742186dea574d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419396"
---
# <a name="deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>AKS (Azure Kubernetes Service)에서 빅 데이터 클러스터 SQL Server 배포

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 샘플 배포 스크립트를 사용 하 여 Azure Kubernetes Service (AKS)에 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 배포 합니다. 

> [!TIP]
> AKS는 빅 데이터 클러스터에 대해 Kubernetes를 호스트 하는 옵션 중 하나입니다. 다른 배포 옵션 및 배포 옵션을 사용자 지정 하는 방법에 대 한 자세한 내용은 [Kubernetes에서 빅 데이터 클러스터 SQL Server 배포 하는 방법](deployment-guidance.md)을 참조 하세요.

여기에 사용 되는 기본 빅 데이터 클러스터 배포는 SQL 마스터 인스턴스, 하나의 계산 풀 인스턴스, 두 개의 데이터 풀 인스턴스 및 두 개의 저장소 풀 인스턴스로 구성 됩니다. 데이터는 AKS 기본 저장소 클래스를 사용 하는 Kubernetes 영구 볼륨을 사용 하 여 유지 됩니다. 이 자습서에서 사용 되는 기본 구성은 개발/테스트 환경에 적합 합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>사전 요구 사항

- Azure 구독.
- [빅 데이터 도구](deploy-big-data-tools.md):
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **Azure CLI**

## <a name="log-in-to-your-azure-account"></a>Azure 계정에 로그인 합니다.

이 스크립트는 Azure CLI을 사용 하 여 AKS 클러스터의 생성을 자동화 합니다. 스크립트를 실행 하기 전에 Azure CLI 한 번 이상 사용 하 여 Azure 계정에 로그인 해야 합니다. 명령 프롬프트에서 다음 명령을 실행 합니다.

```
az login
```

## <a name="download-the-deployment-script"></a>배포 스크립트 다운로드

이 자습서에서는 python 스크립트 **deploy-sql-big-data-aks.py**을 사용 하 여 AKS에서 빅 데이터 클러스터 만들기를 자동화 합니다. **Azdata**용 python을 이미 설치한 경우이 자습서에서 스크립트를 성공적으로 실행할 수 있어야 합니다. 

Windows PowerShell 또는 Linux bash 프롬프트에서 다음 명령을 실행 하 여 GitHub에서 배포 스크립트를 다운로드 합니다.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>배포 스크립트 실행

다음 단계를 사용 하 여 배포 스크립트를 실행 합니다. 이 스크립트는 Azure에서 AKS 서비스를 만든 다음 AKS에 SQL Server 2019 빅 데이터 클러스터를 배포 합니다. 다른 [환경 변수](deployment-guidance.md#configfile) 를 사용 하 여 스크립트를 수정 하 여 사용자 지정 배포를 만들 수도 있습니다.

1. 다음 명령을 사용 하 여 스크립트를 실행 합니다.

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > 클라이언트 컴퓨터와 경로에 python3 및 python2가 둘 다 있는 경우 python3: `python3 deploy-sql-big-data-aks.py`를 사용 하 여 명령을 실행 해야 합니다.

1. 메시지가 표시 되 면 다음 정보를 입력 합니다.

   | 값 | 설명 |
   |---|---|
   | **Azure 구독 ID** | AKS에 사용할 Azure 구독 ID입니다. 다른 명령줄에서를 실행 `az account list` 하 여 모든 구독과 해당 id를 나열할 수 있습니다. |
   | **Azure 리소스 그룹** | AKS 클러스터에 대해 만들 Azure 리소스 그룹 이름입니다. |
   | **Azure 지역** | 새 AKS 클러스터에 대 한 Azure 지역 (기본 **westus**)입니다. |
   | **컴퓨터 크기** | AKS 클러스터의 노드에 사용할 [컴퓨터 크기](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) (기본 **Standard_L8s**)입니다. |
   | **작업자 노드** | AKS 클러스터의 작업자 노드 수 (기본값 **1**)입니다. |
   | **클러스터 이름** | AKS 클러스터와 빅 데이터 클러스터의 이름입니다. 빅 데이터 클러스터의 이름은 소문자 여야 하 고 공백을 포함 해서는 안 됩니다. (기본 **sql이상 데이터**). |
   | **암호** | 컨트롤러, HDFS/Spark 게이트웨이 및 마스터 인스턴스 (기본 **MySQLBigData2019**)의 암호입니다. |
   | **컨트롤러 사용자** | 컨트롤러 사용자의 사용자 이름입니다 (기본값: **admin**). |

다음 매개 변수는 SQL Server 2019 빅 데이터 클러스터 초기 도입자 프로그램의 참가자에 게 필요 합니다. **Docker 사용자 이름**및 **docker 암호**. CTP 3.2은 더 이상 필요 하지 않습니다.

   > [!IMPORTANT]
   > 기본 **Standard_L8s** 컴퓨터 크기는 모든 Azure 지역에서 사용 하지 못할 수 있습니다. 다른 컴퓨터 크기를 선택 하는 경우 클러스터의 노드에 연결할 수 있는 총 디스크 수가 24 이상 인지 확인 합니다. 클러스터의 각 영구적 볼륨 클레임에는 연결 된 디스크가 필요 합니다. 현재 빅 데이터 클러스터에는 24 개의 영구적 볼륨 클레임이 필요 합니다. 예를 들어 [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series) 컴퓨터 크기는 32 연결 된 디스크를 지원 하기 때문에이 컴퓨터 크기의 단일 노드를 사용 하 여 빅 데이터 클러스터를 평가할 수 있습니다.

   > [!NOTE]
   > `sa` 계정은 설치 중에 생성 되는 SQL Server 마스터 인스턴스의 시스템 관리자입니다. 배포를 `MSSQL_SA_PASSWORD` 만든 후에는 마스터 인스턴스 컨테이너에서를 `echo $MSSQL_SA_PASSWORD` 실행 하 여 환경 변수를 검색할 수 있습니다. 보안을 위해 배포 후 마스터 `sa` 인스턴스에서 암호를 변경 합니다. 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)을 참조 하세요.

1. 지정한 매개 변수를 사용 하 여 AKS 클러스터를 만들어 스크립트를 시작 합니다. 이 단계는 몇 분 정도 걸립니다.

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>상태 모니터링

스크립트는 AKS 클러스터를 만든 후 앞에서 지정한 설정을 사용 하 여 필요한 환경 변수를 설정 하는 것으로 진행 합니다. 그런 다음 **azdata** 를 호출 하 여 AKS에 빅 데이터 클러스터를 배포 합니다.

클라이언트 명령 창이 배포 상태를 출력 합니다. 배포 프로세스 중에 컨트롤러 pod를 대기 하는 일련의 메시지가 표시 됩니다.

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

10 분에서 20 분 후에 컨트롤러 pod가 실행 중임을 알리는 알림이 표시 됩니다.

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> 전체 배포는 빅 데이터 클러스터의 구성 요소에 대 한 컨테이너 이미지를 다운로드 하는 데 필요한 시간 때문에 시간이 오래 걸릴 수 있습니다. 그러나 몇 시간이 소요 되어서는 안 됩니다. 배포에 문제가 발생 하는 경우 [빅 데이터 클러스터 SQL Server 모니터링 및 문제 해결](cluster-troubleshooting-commands.md)을 참조 하세요.

## <a name="inspect-the-cluster"></a>클러스터 검사

배포 하는 동안 언제 든 지 **kubectl** 또는 **azdata** 를 사용 하 여 실행 중인 빅 데이터 클러스터에 대 한 상태 및 세부 정보를 검사할 수 있습니다.

### <a name="use-kubectl"></a>Kubectl 사용

배포 프로세스 중에 **kubectl** 를 사용 하는 새 명령 창을 엽니다.

1. 다음 명령을 실행 하 여 전체 클러스터의 상태에 대 한 요약을 가져옵니다.

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 빅 데이터 클러스터 이름을 변경 하지 않은 경우 스크립트는 기본적으로 **sql를 data**로 설정 합니다.

1. 다음 **kubectl** 명령을 사용 하 여 kubernetes services 및 내부 및 외부 끝점을 검사 합니다.

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. 다음 명령을 사용 하 여 kubernetes pod의 상태를 검사할 수도 있습니다.

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. 다음 명령을 사용 하 여 특정 pod에 대 한 자세한 정보를 확인 합니다.

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> 배포를 모니터링 하 고 문제를 해결 하는 방법에 대 한 자세한 내용은 [빅 데이터 클러스터 SQL Server 모니터링 및 문제 해결](cluster-troubleshooting-commands.md)을 참조 하세요.

## <a name="connect-to-the-cluster"></a>클러스터에 연결

배포 스크립트가 완료 되 면 출력은 성공 여부를 알려 줍니다.

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

이제 SQL Server 빅 데이터 클러스터가 AKS에 배포 됩니다. 이제 Azure Data Studio를 사용 하 여 클러스터에 연결할 수 있습니다. 자세한 내용은 [Azure Data Studio를 사용 하 여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조 하세요.

## <a name="clean-up"></a>정리

Azure에서 빅 데이터 클러스터 SQL Server 테스트 하는 경우 예기치 않은 요금을 방지 하기 위해 완료 되 면 AKS 클러스터를 삭제 해야 합니다. 클러스터를 계속 사용 하려는 경우 클러스터를 제거 하지 마세요.

> [!WARNING]
> 다음 단계는 SQL Server 빅 데이터 클러스터도 제거 하는 AKS 클러스터를 종료 합니다. 유지 하려는 데이터베이스 또는 HDFS 데이터가 있는 경우 클러스터를 삭제 하기 전에 해당 데이터를 백업 합니다.

다음 Azure CLI 명령을 실행 하 여 Azure에서 빅 데이터 클러스터 및 AKS 서비스 (배포 스크립트에서 지정한 `<resource group name>` **azure 리소스 그룹** 으로 대체)를 제거 합니다.

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>다음 단계

배포 스크립트는 Azure Kubernetes Service를 구성 하 고 SQL Server 2019 빅 데이터 클러스터도 배포 했습니다. 수동 설치를 통해 향후 배포를 사용자 지정 하도록 선택할 수도 있습니다. 빅 데이터 클러스터를 배포 하는 방법 및 배포를 사용자 지정 하는 방법에 대 한 자세한 내용은 [Kubernetes에서 빅 데이터 클러스터 SQL Server 배포 하는 방법](deployment-guidance.md)을 참조 하세요.

SQL Server 빅 데이터 클러스터가 배포 되었으므로 샘플 데이터를 로드 하 고 자습서를 탐색할 수 있습니다.

> [!div class="nextstepaction"]
> [자습서: SQL Server 2019 빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)