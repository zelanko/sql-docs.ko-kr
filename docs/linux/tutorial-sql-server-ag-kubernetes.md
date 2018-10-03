---
title: Kubernetes의 Docker 컨테이너에서 SQL Server Always On 가용성 그룹 구성 | Microsoft Docs
description: 이 자습서에서는 Azure Container Service에서 Kubernetes 사용 하 여 SQL Server always on 가용성 그룹을 배포 하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: sql-linux,mvc
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 119574498dec87bc38ab1b0904c53b7f62716427
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665574"
---
# <a name="configure-a-sql-server-always-on-availability-group-on-docker-containers-in-kubernetes-with-azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS)를 사용 하 여 Kubernetes에서 Docker 컨테이너에서 SQL Server Always On 가용성 그룹 구성

이 자습서에는 AKS 컨테이너에 항상 사용 가능한 SQL Server 인스턴스를 구성 하는 방법을 보여 줍니다. 할 수도 있습니다 [Kubernetes에서 SQL Server 컨테이너를 배포](tutorial-sql-server-containers-kubernetes.md)합니다. 두 가지 다른 Kubernetes 솔루션 비교를 참조 하세요 [SQL Server 컨테이너에 대 한 고가용성](sql-server-linux-container-ha-overview.md)합니다.

이 자습서에 알아봅니다 방법:  

> [!div class="checklist"]
> * 저장소 만들기
> * SQL Server 운영자는 Kubernetes 클러스터에 배포 
> * Kubernetes 비밀 만들기
> * SQL Server 인스턴스 및 상태 에이전트를 배포 합니다.
> * 주 복제본에 연결
> * 가용성 그룹에 데이터베이스 추가

이 자습서의 아키텍처를 보여 줍니다 [Azure Kubernetes Service (AKS)](http://docs.microsoft.com/azure/aks/)합니다. Azure 구독이 없으면 만듭니다는 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 시작 하기 전에 합니다.

이 다이어그램에는이 자습서에서 만든 솔루션을 나타냅니다.

![kubernetes ag 클러스터](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

### <a name="deployment-methodology-for-kubernetes"></a>Kubernetes에 대 한 배포 방법

이 문서의 단계 중 일부를 매니페스트를 만들고 클러스터 매니페스트를 배포 합니다. 매니페스트는 배포 하는 Kubernetes 개체의 설명 사용 하 여.yaml 파일.

이 예제의.yaml 파일에서 제공 됩니다 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability)합니다.

개체는 저장소, 연산자, pod, 컨테이너 및 서비스를 포함 합니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이러한 기술 사용 하 여 일반 경험

  * [Kubernetes](http://kubernetes.io) 버전 1.8
  * [AKS (azure Kubernetes Service)](http://docs.microsoft.com/azure/aks/)
  * [Docker에서 SQL Server](quickstart-install-connect-docker.md)
  * [SQL Server Always On 가용성 그룹](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

* 4 개의 노드가 있는 Kubernetes 클러스터입니다.

  자세한 내용은를 참조 [자습서: Azure Kubernetes Service (AKS) 클러스터를 배포](http://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster)합니다.

* 설치할 [ `kubectl` ](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#install-the-kubectl-cli)합니다.

## <a name="configuration-and-deployment-procedures"></a>구성 및 배포 절차

자습서에서는 Kubernetes 클러스터에.yaml 파일을 적용 하는 방법을 보여줍니다.

## <a name="create-the-secrets"></a>비밀 만들기

SQL Server SA 계정 및 SQL Server 마스터 키에 대 한 암호를 저장 하는 Kubernetes 비밀을 만들려면 다음 명령을 실행 합니다.

```azurecli
kubectl create secret generic sql-secrets --from-literal=sapassword="MyC0m9l&xP@ssw0rd" --from-literal=masterkeypassword="MyC0m9l&xP@ssw0rd2"
```

프로덕션 환경에서 다른, 복잡 한 암호를 사용 합니다.

## <a name="deploy-the-operator"></a>연산자를 배포 합니다.

SQL Server 인스턴스를 배포 하 고 Kubernetes 클러스터에서 가용성 그룹을 구성 하는 Kubernetes 연산자. 

예의 운영자를 참조 하세요. [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml)

다운로드 `operator.yaml` 에서 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/)

하나의 복제본 Kubernetes 배포로 연산자를 배포 합니다.

연산자를 배포 합니다.

연산자를 사용 하 여 배포를 `kubectl apply` 명령입니다.

```azurecli
kubectl apply -f operator.yaml
```

## <a name="create-the-sql-server-ag-deployment"></a>SQL Server AG 배포 만들기

다음 단계는 한 Kubernetes 배포를 SQL Server 인스턴스 및 가용성 그룹을 만듭니다. 클러스터에이 배포를 적용 하면 연산자는 Docker 컨테이너로 SQL Server 인스턴스를 배포 합니다. 이 배포 1 개의 pod 사용 하 여 세 가지 StatefulSets 발생 합니다. 모든 pod는 두 개의 컨테이너가 포함 됩니다.

* SQL Server 인스턴스를 기반으로 합니다 `mssql-server` 이미지
* HA 감독자

배포에서 가용성 그룹 수신기에 대 한 부하 분산 서비스를 설명 하는 또한

Mssql server를 배포 합니다.

1. 복사본 [sqlserver.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml) 컴퓨터에 있습니다.
2. 업데이트 `sqlserver.yaml` 사용자 환경에 대 한 합니다.


SQL Server 인스턴스를 배포 하는 가용성 그룹 만들기를 다음 명령을 실행 합니다.

```azurecli
kubectl apply -f sqlserver.yaml
```

## <a name="deploy-ag-services"></a>배포 AG 서비스

Kubernetes 클러스터에서 가용성 그룹의 복제본에 대 한 직접 호출으로 부하 분산 장치 서비스를 만듭니다.

[ag services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 네 가지 서비스를 만듭니다.

* ag1 기본 주 복제본에 연결합니다.
* ag1 보조 동기화 동기 보조 복제본에 연결합니다.
* ag1 보조 비동기 비동기 보조 복제본에 연결합니다.
* ag1-보조-config 구성 전용 복제본에 연결합니다. 

  >[!NOTE]
  >이러한 부하 분산 장치 서비스 예제로 제공 됩니다. 이 자습서에서는 구성 전용 복제본 하지 않습니다.


가용성 그룹에 연결할 수 있도록 부하 분산 장치 서비스를 배포 합니다.

서비스를 배포 하려면 다음 명령을 실행 합니다.

```azurecli
kubectl apply -f ag-services.yaml
```

### <a name="monitor-the-deployment"></a>배포 모니터링

사용할 수 있습니다 [Azure Kubernetes Service (AKS)를 사용 하 여 Kubernetes 대시보드](https://docs.microsoft.com/en-us/azure/aks/kubernetes-dashboard) 배포를 모니터링 하려면. 

사용 하 여 `az aks browse` 대시보드를 시작 합니다. 

배포 후만 AG 멤버 자격 목록 및 post init T-SQL 스크립트를 업데이트할 수 있습니다. 다른 속성을 업데이트할 수 없습니다-리소스를 삭제 하 고 다시 만들어야 합니다. 사용 하 여 자동으로 생성 된 사용자를 회전할 수에 대 한 자격 증명을 `mssql-server-k8s-rotate-creds` 작업 합니다.

## <a name="connect-to-the-sql-server-instance-hosting-the-primary-replica"></a>주 복제본을 호스팅하는 SQL Server 인스턴스에 연결 합니다.

합니다 `ag-services.yaml` Kubernetes 서비스 이름에 설명 `ag1-primary`합니다. `ag1-primary` 주 복제본을 호스팅하는 SQL Server 인스턴스를 가리키는 Azure load balancer를 만듭니다. 서비스의 외부 IP 주소를 사용 하 여 대상 서버로 `sa` 계정으로 및에서 만든 암호를 `mssql secret` 암호입니다.

사용 하 여 `kubectl get services` 이 IP 주소를 가져옵니다.

이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

![가져오기 서비스 예제](media\tutorial-sql-server-ag-containers-kubernetes\KubernetesGetServices.png)

위의 그림과 `ag1-primary` 서비스의 외부 IP 주소에 `104.42-50.138`입니다. 

SQL 인증을 사용 하 여 SQL Server에 연결 하려면 사용 합니다 `sa` 계정, 값 `sapassword` , 만든 비밀 및이 IP 주소에서 합니다.

이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

```cmd
sqlcmd -S 104.42.50.138 -U sa -P "MyC0m9l&xP@ssw0rd"
```

![Sqlcmd를 사용 하 여 연결](./media/tutorial-sql-server-ag-containers-kubernetes/sqlcmdConnect.png)

사용 하 여 연결할 수 있습니다 [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)합니다.

연결을 확인 하려면 주 복제본을 호스팅하는 SQL Server 인스턴스에 다음 쿼리를 실행 합니다.

```sql
SELECT @@SERVERNAME;
```

쿼리는 주 복제본을 호스팅하는 SQL Server 인스턴스의 이름을 반환 합니다.

이 시점에서 Kubernetes 클러스터에 docker 컨테이너에서 SQL Server 인스턴스의 수가 세 있습니다. 가용성 그룹이 SQL Server의 세 개를 모두 있지만 데이터베이스가 가용성 그룹에 없습니다. 가용성 그룹에 데이터베이스를 추가 하려면 다음 단계가입니다.

## <a name="add-a-database-to-the-availability-group"></a>가용성 그룹에 데이터베이스 추가

가용성 그룹에 데이터베이스를 추가 합니다.

1. 데이터베이스 만들기

  ```sql
  CREATE DATABASE [DemoDB]
  ```

1. 전체 트랜잭션 로그 체인이 시작 데이터베이스의 백업을 수행합니다

  ```sql
  BACKUP DATABASE [DemoDB] 
  TO  DISK = N'/var/opt/mssql/data/DemoDB.bak' 
    WITH NOFORMAT, 
    NOINIT,  
    NAME = N'DemoDB-Full Database Backup', 
    SKIP, 
    NOREWIND, 
    NOUNLOAD,  
    STATS = 10;
  GO
  ```

1. 가용성 그룹에 데이터베이스 추가

  ```sql
  ALTER AVAILABILITY GROUP ag1 ADD DATABASE [DemoDB]; 
  ```

복제본은 가용성 그룹 보조 복제본에 데이터베이스를 시드합니다 있으므로 자동 시드 모드를 사용 하 여 자동으로 구성 됩니다.

SQL Server Management Studio에서 주 복제본에 연결 하 고 대시보드에서 가용성 그룹을 확인할 수 있습니다.

다음 샘플 대시보드의 구성 하는 세 개의 노드에서 가용성 그룹을 복제본을 사용 하 여 보여 줍니다.

![AG1 대시보드](./media/tutorial-sql-server-ag-containers-kubernetes/ssms_AG1.png)

## <a name="verify-failure-and-recovery"></a>오류 및 복구를 확인 합니다.

오류 감지 및 장애 조치를 확인 하려면 주 복제본을 호스트 하는 pod를 삭제할 수 있습니다. Kubernetes는 새로운 주 복제본을 선택 하 고 수신기를 리디렉션합니다. 이 다시 pod를 삭제 합니다. 

이 프로세스를 보여 주기 위해 다음 단계를 수행 합니다.

1. SQL Server를 실행 하는 pod를 나열 합니다.

   ```azurecli
   kubectl get pods
   ```

2. 주 복제본을 실행 하는 pod를 식별 합니다.

   외부 IP 및 쿼리를 사용 하 여 주 복제본에 연결 하거나 `@@servername` 사용할지 `kubectl` 적절 한 pod를 가져오려고 합니다. 이 명령에는 AG의 주 복제본을 실행 중인 컨테이너를 포함 하는 pod의 이름을 반환 합니다.

   ```azurecli
   kubectl get pods --selector="role.ag.mssql.microsoft.com/ag1"="primary" --output=jsonpath={.items..metadata.name}
   ```

3. Pod를 삭제 합니다.

   ```azurecli
   kubectl delete pod <podName>
   ```

대체 `<podName>` pod 이름에 대 한 이전 단계에서 반환 된 값입니다. 

Kubernetes 자동으로 동기화를 사용할 수 있는 보조 복제본 중 하나에 장애 조치 뿐만 아니라 삭제 된 pod를 다시 만듭니다.

## <a name="clean-up-resources"></a>리소스 정리

더 이상 필요한 경우 리소스 그룹 및 모든 관련된 리소스를 삭제 합니다. 다음 명령을 실행합니다.
>[!WARNING]
>이 명령은 리소스 그룹의 모든 항목에 완전히 삭제합니다. Kubernetes 클러스터의 구성 요소가 리소스 그룹을 삭제 한 후 사용할 수 있습니다.

```azurecli
az group delete --name <MyResourceGroup>
```

위의 명령을 실행 하려면 대체 `<MyResourceGroup>` 리소스 그룹의 이름입니다. 

Azure는 리소스 그룹을 삭제합니다.

## <a name="summary"></a>요약

이 자습서에서는 학습 하는 방법.  

> [!div class="checklist"]
> * 저장소 만들기
> * SQL Server 운영자는 Kubernetes 클러스터에 배포 
> * Kubernetes 비밀 만들기
> * SQL Server 인스턴스 및 상태 에이전트를 배포 합니다.
> * 주 복제본에 연결
> * 가용성 그룹에 데이터베이스 추가

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
>[Kubernetes 소개](http://docs.microsoft.com/azure/aks/intro-kubernetes)
>[Kubernetes의 SQL Server 관리](sql-server-linux-kubernetes-manage.md)
