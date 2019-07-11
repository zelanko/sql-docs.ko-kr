---
title: 배포 스크립트
titleSuffix: SQL Server big data clusters
description: Azure Kubernetes Service (AKS)에서 SQL Server 2019 빅 데이터 클러스터 (미리 보기)의 배포를 연습 합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0254b76b0845ff5f913d2d0ab69324ddd0072923
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728777"
---
# <a name="deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS)에서 SQL Server 빅 데이터 클러스터를 배포 합니다.

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 Azure Kubernetes Service (AKS)를 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 배포 하는 샘플 배포 스크립트를 사용 합니다. 

> [!TIP]
> AKS는 Kubernetes 빅 데이터 클러스터에 대 한 호스팅에 대 한 하나의 옵션입니다. 다른 배포 옵션 하는 옵션 배포를 사용자 지정 하는 방법을 알아보려면 [빅 데이터를 SQL Server를 배포 하는 방법에서 kubernetes 클러스터](deployment-guidance.md)합니다.

여기에 기본 빅 데이터 클러스터 배포를 SQL 마스터 인스턴스를, 풀 인스턴스를 하나의 계산, 두 데이터 풀 인스턴스 및 두 개의 저장소 풀 인스턴스에 구성 됩니다. 데이터는 AKS 기본 저장소 클래스를 사용 하는 Kubernetes 영구적 볼륨을 사용 하 여 유지 됩니다. 이 자습서에 사용 된 기본 구성을 개발/테스트 환경에 적합 합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>사전 요구 사항

- Azure 구독입니다.
- [빅 데이터 도구도](deploy-big-data-tools.md):
   - **mssqlctl**
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **Azure CLI**

## <a name="log-in-to-your-azure-account"></a>Azure 계정에 로그인

AKS 클러스터 만들기를 자동화 하려면 Azure CLI를 사용 하는 스크립트입니다. 스크립트를 실행 하기 전에 로그인 해야 Azure CLI를 사용 하 여 Azure 계정에 한 번 이상. 명령 프롬프트에서 다음 명령을 실행 합니다.

```
az login
```

## <a name="download-the-deployment-script"></a>배포 스크립트를 다운로드 합니다.

이 자습서는 python 스크립트를 사용 하 여 AKS에서 빅 데이터 클러스터 만들기 자동화 **배포-sql-큰-데이터-aks.py**합니다. Python을 이미 설치한 경우 **mssqlctl**,이 자습서에서 스크립트를 성공적으로 실행할 수 있도록 해야 합니다. 

Windows PowerShell 또는 Linux bash 프롬프트에서 GitHub에서 배포 스크립트를 다운로드 하려면 다음 명령을 실행 합니다.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>배포 스크립트를 실행 합니다.

배포 스크립트를 실행 하려면 다음 단계를 사용 합니다. 이 스크립트를 Azure에서 AKS 서비스를 만들고 AKS에 SQL Server 2019 빅 데이터 클러스터를 배포 합니다. 또한 다른 스크립트를 수정할 수 있습니다 [환경 변수](deployment-guidance.md#configfile) 사용자 지정 배포를 만듭니다.

1. 다음 명령을 사용 하 여 스크립트를 실행 합니다.

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > Python3을 사용 하 여 명령을 실행 해야 하는 경우 python3와 python2 경로 및 클라이언트 컴퓨터에서: `python3 deploy-sql-big-data-aks.py`합니다.

1. 메시지가 표시 되 면 다음 정보를 입력 합니다.

   | 값 | 설명 |
   |---|---|
   | **Azure 구독 ID** | AKS를 사용 하 여 Azure 구독 ID입니다. 실행 하 여 모든 구독 및 해당 Id를 나열할 수 있습니다 `az account list` 다른 명령줄에서. |
   | **Azure 리소스 그룹** | AKS 클러스터를 만드는 Azure 리소스 그룹 이름입니다. |
   | **Docker 사용자 이름** | 제한 된 공개 미리 보기의 일부로 제공 되는 Docker 사용자 이름입니다. |
   | **Docker 암호** | 제한 된 공개 미리 보기의 일부로 제공 된 Docker 암호입니다. |
   | **Azure 지역** | 새 AKS 클러스터에 대 한 Azure 지역 (기본 **westus**). |
   | **컴퓨터 크기** | 합니다 [컴퓨터 크기](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) AKS 클러스터의 노드에 대해 사용 하도록 (기본 **Standard_L8s**). |
   | **작업자 노드** | AKS 클러스터의 작업자 노드 수 (기본 **1**). |
   | **클러스터 이름** | AKS 클러스터와 빅 데이터 클러스터의 이름입니다. 소문자 영숫자 문자만 및 공백 없이 빅 데이터 클러스터의 이름 이어야 합니다. (기본값 **sqlbigdata**). |
   | **암호** | 컨트롤러, HDFS/Spark 게이트웨이 및 마스터 인스턴스를 실행 하는 것에 대 한 암호 (기본 **MySQLBigData2019**). |
   | **컨트롤러 사용자** | 컨트롤러 사용자의 사용자 이름 (기본값: **관리자**). |

   > [!IMPORTANT]
   > 기본값 **Standard_L8s** 모든 Azure 지역에서 인해 컴퓨터 크기를 사용할 수 있습니다. 다른 컴퓨터 크기 선택 않으면, 클러스터의 노드에서 연결할 수 있는 디스크의 총 24 보다 크거나 같은 경우 인지 확인 합니다. 클러스터의 각 영구적 볼륨 클레임에는 연결된 된 디스크에 필요합니다. 현재 빅 데이터 클러스터는 24 영구적 볼륨 클레임을 필요합니다. 예를 들어 합니다 [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series) 이 컴퓨터 크기의 단일 노드를 사용 하 여 빅 데이터 클러스터를 평가할 수 있도록 컴퓨터 크기에 32 개의 연결 된 디스크를 지원 합니다.

   > [!NOTE]
   > `sa` 계정은 설치 중에 생성 되는 SQL Server 마스터 인스턴스에서 시스템 관리자입니다. 배포를 만든 후 합니다 `MSSQL_SA_PASSWORD` 실행 하 여 환경 변수를 검색할 수 `echo $MSSQL_SA_PASSWORD` 마스터 인스턴스 컨테이너에 있습니다. 보안상의 이유로 변경에 `sa` 마스터 인스턴스 배포 후에 암호입니다. 자세한 내용은 [SA 암호 변경](../linux/quickstart-install-connect-docker.md#sapassword)합니다.

1. 지정한 매개 변수를 사용 하 여 AKS 클러스터를 만들어 스크립트를 시작 합니다. 이 단계는 몇 분 정도 걸립니다.

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>상태 모니터링

AKS 클러스터에서 스크립트를 만든 후 이전에 지정한 설정 사용 하 여 필요한 환경 변수를 설정 하려면 진행 됩니다. 그런 다음 호출 **mssqlctl** AKS에서 빅 데이터 클러스터를 배포 합니다.

클라이언트 명령 창에는 배포 상태를 출력 합니다. 배포 과정에서 컨트롤러 pod에 대 한 기다리고 있는 일련의 메시지를 표시 됩니다.

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

10 ~ 20 분 후 있습니다 알려야 컨트롤러 pod가 실행 중인지:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> 전체 배포는 빅 데이터 클러스터의 구성 요소에 대 한 컨테이너 이미지를 다운로드 하는 데 필요한 시간 때문에 시간이 걸릴 수 있습니다. 그러나 하지 몇 시간이 걸립니다. 배포 문제가 발생 하는 경우 참조 [모니터링 및 SQL Server 빅 데이터 클러스터 문제 해결](cluster-troubleshooting-commands.md)합니다.

## <a name="inspect-the-cluster"></a>클러스터를 검사 합니다.

배포 하는 동안 언제 든 사용할 수 있습니다 **kubectl** 또는 **mssqlctl** 의 상태 및 실행 빅 데이터 클러스터에 대 한 세부 정보를 검사 합니다.

### <a name="use-kubectl"></a>Kubectl 사용

사용 하는 새 명령 창을 열고 **kubectl** 배포 프로세스 중입니다.

1. 전체 클러스터의 상태 요약을 가져오려면 다음 명령을 실행 합니다.

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 빅 데이터 클러스터 이름을 변경 하지 않은 스크립트를 기본값으로 **sqlbigdata**합니다.

1. Kubernetes 서비스 및 해당 내부 및 외부 끝점은 다음을 사용 하 여 검사할 **kubectl** 명령:

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. 또한 다음 명령 사용 하 여 kubernetes pod의 상태를 검사할 수 있습니다.

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. 다음 명령 사용 하 여 특정 pod에 대 한 자세한 정보를 확인 합니다.

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> 모니터링 및 배포 문제를 해결 하는 방법에 대 한 자세한 내용은 참조 하세요. [모니터링 및 SQL Server 빅 데이터 클러스터 문제 해결](cluster-troubleshooting-commands.md)합니다.

## <a name="connect-to-the-cluster"></a>클러스터에 연결

배포 스크립트가 완료 되 면 출력 성공 알리는 메시지를 표시 합니다.

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

SQL Server 빅 데이터 클러스터를 AKS에 배포 됩니다. 이제 클러스터에 연결할 Azure Data Studio를 사용할 수 있습니다. 자세한 내용은 [Azure Data Studio를 사용 하 여 빅 데이터 클러스터를 SQL Server에 연결](connect-to-big-data-cluster.md)합니다.

## <a name="clean-up"></a>정리

Azure에서 SQL Server 빅 데이터 클러스터를 테스트 하는 경우 예기치 않은 요금을 방지 하려면 완료 되 면 AKS 클러스터를 삭제 해야 합니다. 계속 사용 하려는 경우에 클러스터를 제거 하지 마십시오.

> [!WARNING]
> AKS 클러스터 뿐만 아니라 SQL Server 빅 데이터 클러스터를 제거 하는 다음 단계를 삭제 합니다. 모든 데이터베이스 또는 HDFS 데이터를 유지 하려는 경우 클러스터를 삭제 하기 전에 해당 데이터를 백업 합니다.

Azure에서 빅 데이터 클러스터 및 AKS 서비스를 제거 하려면 다음 Azure CLI 명령을 실행 (바꿉니다 `<resource group name>` 사용 하 여 합니다 **Azure 리소스 그룹** 배포 스크립트에 지정):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>다음 단계

배포 스크립트는 Azure Kubernetes Service를 구성 하 고도 SQL Server 2019 빅 데이터 클러스터를 배포 합니다. 또한 수동 설치를 통해 향후 배포를 사용자 지정할 수 있습니다. 더 어떻게 빅 데이터에 대 한 클러스터 배포 된 배포를 사용자 지정 하는 방법에 대해 알아보려면 [빅 데이터를 SQL Server를 배포 하는 방법에서 kubernetes 클러스터](deployment-guidance.md)합니다.

이제 SQL Server 빅 데이터 클러스터를 배포한 샘플 데이터를 로드 하 고 수 있는 자습서를 탐색 합니다.

> [!div class="nextstepaction"]
> [자습서: SQL Server 2019 빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)