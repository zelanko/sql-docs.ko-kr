---
title: Kubernetes 클러스터에 SQL Server Always On 가용성 그룹 배포
description: 이 문서에서는 SQL Server Kubernetes Always On 가용성 그룹 연산자 전역 요구 사항에 대한 매개 변수를 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1e8825336edd4e55812f6037bbb4479a3b225e3f
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028735"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-a-kubernetes-cluster"></a>Kubernetes 클러스터에 SQL Server Always On 가용성 그룹 배포

이 문서의 예제에서는 세 개의 복제본이 있는 Kubernetes 클러스터에 SQL Server Always On 가용성 그룹을 배포합니다. 보조 복제본은 동기 커밋 모드에 있습니다.

Kubernetes에 대한 배포에는 SQL Server 연산자, SQL Server 컨테이너 및 부하 분산 장치 서비스가 포함됩니다. 연산자는 가용성 그룹을 자동으로 오케스트레이션합니다. 이 문서에서는 다음 방법을 설명합니다.

- 연산자, SQL Server 컨테이너 및 부하 분산 서비스를 배포합니다.
- 서비스를 사용하여 가용성 그룹에 연결합니다.
- 가용성 그룹에 데이터베이스를 추가합니다.

## <a name="requirements"></a>요구 사항

- 최신 버전을 사용하는 AKS Kubernetes 클러스터
- 노드 3개 이상
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) GitHub 리포지토리에 액세스

> [!NOTE]
> 모든 유형의 Kubernetes 클러스터를 사용할 수 있습니다. AKS(Azure Kubernetes Service)에서 Kubernetes 클러스터를 만들려면 [Create an AKS cluster](https://docs.microsoft.com/azure/aks/create-cluster)(AKS 클러스터 만들기)를 참조하세요.
>
> 최신 버전의 Kubernetes를 사용합니다. 특정 버전은 구독 및 지역에 따라 달라집니다. [Supported Kubernetes versions in AKS](https://docs.microsoft.com/azure/aks/supported-kubernetes-versions)(AKS에서 지원되는 Kubernetes 버전)를 참조하세요.  
>
> 다음 스크립트는 Azure에서 4노드 Kubernetes 클러스터를 만듭니다. 스크립트를 실행하기 전에 `<latest version>`을 사용 가능한 최신 버전으로 바꿉니다. 예를 들면 `1.12.5`입니다.
>
> ```azure-cli
> az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version <latest version> --generate-ssh-keys
> ```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>연산자, SQL Server 컨테이너 및 부하 분산 서비스 배포

1. [네임스페이스](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)를 만듭니다.

      이 예제에서는 `ag1`이라는 네임스페이스를 사용합니다. 다음 명령을 실행하여 네임스페이스를 만듭니다.
    
      ```azurecli
      kubectl create namespace ag1
      ```
    
      이 솔루션에 속하는 모든 개체는 `ag1` 네임스페이스에 있습니다.

1. SQL Server 연산자 매니페스트를 구성하고 배포합니다.

      [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)에서 SQL Server [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml) 파일을 복사합니다.
    
      `operator.yaml` 파일은 Kubernetes 연산자의 배포 매니페스트입니다.
    
      Kubernetes 클러스터에 매니페스트를 적용합니다.
    
      ```azurecli
      kubectl apply -f operator.yaml --namespace ag1
      ```
    
1. `sa` 계정 및 SQL Server 인스턴스 마스터 키의 암호를 사용하여 Kubernetes의 비밀을 만듭니다.

      `kubectl`을 사용하여 비밀을 만듭니다.
      
      다음 예제에서는 `ag1` 네임스페이스에 `sql-secrets`라는 비밀을 만듭니다. 비밀은 두 개의 암호를 저장합니다.
      
      - `sapassword`는 SQL Server `sa` 계정의 암호를 저장합니다.
      - `masterkeypassword`는 SQL Server 마스터 키를 만드는 데 사용된 암호를 저장합니다. 
    
   스크립트를 터미널에 복사합니다. 각 `<>`를 복잡한 암호로 바꾸고 스크립트를 실행하여 비밀을 만듭니다.
    
   >[!NOTE]
   >암호에는 `` ` `` 또는 `&` 문자를 사용할 수 없습니다.
    
   ```azurecli
   kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
   ```

1. SQL Server 사용자 지정 리소스를 배포합니다.

      [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)에서 SQL Server 매니페스트 [`sqlserver.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml)을 복사합니다.
    
      >[!NOTE]
      >`sqlserver.yaml` 파일은 각 SQL Server 인스턴스에 필요한 SQL Server 컨테이너, 영구적 볼륨 클레임, 영구적 볼륨 및 부하 분산 서비스를 설명합니다.
    
      Kubernetes 클러스터에 매니페스트를 적용합니다.
    
      ```azurecli
      kubectl apply -f sqlserver.yaml --namespace ag1
      ```
      
다음 이미지는 이 예제에서 성공적인 `kubectl apply` 적용을 보여 줍니다.

![sqlservers 만들기](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

SQL Server 매니페스트를 적용한 후 연산자는 SQL Server 컨테이너를 배포합니다.

Kubernetes는 컨테이너를 Pod에 배치합니다. `kubectl get pods --namespace ag1`을 사용하여 Pod 상태를 확인합니다. 다음 이미지는 SQL Server Pod가 배포된 후 배포 예제를 보여 줍니다. 

![빌드된 Pod](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>배포 모니터링

[Azure Kubernetes Service와 함께 Kubernetes 대시보드](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)를 사용하여 배포를 모니터링합니다.

`az aks browse`를 사용하여 대시보드를 시작합니다. 

## <a name="connect-to-the-availability-group-with-the-services"></a>서비스를 사용하여 가용성 그룹에 연결

[sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 예제의 [`ag-services.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml)은 가용성 그룹 복제본에 연결할 수 있는 부하 분산 서비스를 설명합니다. 

- `ag1-primary`는 주 복제본에 연결할 엔드포인트를 제공합니다.
- `ag1-secondary`는 보조 복제본에 연결할 엔드포인트를 제공합니다.

매니페스트 파일을 적용하면 Kubernetes는 각 유형의 복제본에 대한 부하 분산 서비스를 만듭니다. 부하 분산 서비스에는 IP 주소가 포함됩니다. 이 IP 주소를 사용하여 필요한 복제본 유형에 연결합니다.

서비스를 배포하려면 다음 명령을 실행합니다.

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

서비스를 배포한 후 `kubectl get services --namespace ag1`을 사용하여 서비스의 IP 주소를 식별합니다.

IP 주소를 사용하여 각 유형의 복제본을 호스트하는 SQL Server 인스턴스에 연결할 수 있습니다.

아래 이미지는 다음 항목을 보여 줍니다.

- 네임스페이스 `ag1`에 대한 `kubectl get services`의 출력.

- 각 SQL Server 컨테이너에 대해 만들어진 부하 분산 서비스. 이이 IP 주소를 엔드포인트로 사용하여 클러스터의 SQL Server 인스턴스에 직접 연결합니다.

- 부하 분산 장치 엔드포인트를 통해 `sa` 계정으로 주 복제본에 대한 `sqlcmd` 연결.

![연결](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>가용성 그룹에 데이터베이스 추가

>[!NOTE]
>현재 SQL Server Management Studios는 가용성 그룹에 데이터베이스를 추가할 수 없습니다. Transact-SQL을 사용합니다.

Kubernetes가 SQL Server 컨테이너를 만든 후 다음 단계를 완료하여 가용성 그룹에 데이터베이스를 추가합니다.

1. 클러스터의 SQL Server 인스턴스에 [연결](sql-server-linux-kubernetes-connect.md)합니다.

1. 데이터베이스를 만듭니다.

      ```sql
      CREATE DATABASE [demodb]
      ```

1. 데이터베이스의 전체 백업을 수행하여 로그 체인을 시작합니다.

      ```sql
      USE MASTER
      GO
      BACKUP DATABASE [demodb] 
      TO DISK = N'/var/opt/mssql/data/demodb.bak'
      ```

1. 가용성 그룹에 데이터베이스를 추가합니다.

      ```sql
      ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [demodb]
      ```
    
SQL Server가 자동으로 보조 복제본을 만들도록 자동 시드를 사용하여 가용성 그룹을 만듭니다.

SQL Server Management Studio 가용성 그룹 대시보드에서 가용성 그룹의 상태를 볼 수 있습니다.

![대시보드](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>다음 단계

- [Kubernetes 클러스터의 SQL Server 가용성 그룹에 연결](sql-server-linux-kubernetes-connect.md)

- [Kubernetes 클러스터에서 SQL Server 가용성 그룹 관리](sql-server-linux-kubernetes-manage.md)

- [SQL Server는 Kubernetes 클러스터의 컨테이너에 대한 가용성 그룹을 지원함](sql-server-ag-kubernetes.md)
