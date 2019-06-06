---
title: Kubernetes 클러스터에 SQL Server Always On 가용성 그룹 배포
description: 이 문서는 SQL Server Kubernetes Always On 가용성 그룹 연산자 글로벌 요구 사항에 대 한 매개 변수를 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 07d0929dbdf60c31f1518a19a2999f0845d7d2e2
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713121"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-a-kubernetes-cluster"></a>Kubernetes 클러스터에 SQL Server Always On 가용성 그룹 배포

이 문서의 예제에서는 세 개의 복제본을 사용 하 여 Kubernetes 클러스터에서 SQL Server Always On 가용성 그룹을 배포합니다. 보조 복제본이 동기 커밋 모드입니다.

Kubernetes에 배포 포함 연산자를 SQL Server, SQL Server 컨테이너 및 부하 분산 장치 서비스입니다. 연산자는 가용성 그룹을 자동으로 조정합니다. 이 문서에서는 설명 하는 방법.

- 연산자, SQL Server 컨테이너 및 부하 분산 서비스를 배포 합니다.
- 서비스를 사용 하 여 가용성 그룹에 연결 합니다.
- 가용성 그룹에 데이터베이스를 추가 합니다.

## <a name="requirements"></a>요구 사항

- 최신 버전을 사용 하 여 AKS Kubernetes 클러스터를
- 노드가 3 개 이상
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- 에 대 한 액세스는 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) GitHub 리포지토리

> [!NOTE]
> 모든 유형의 Kubernetes 클러스터를 사용할 수 있습니다. Azure Kubernetes Service (AKS)에서 Kubernetes 클러스터를 만들려면, 참조 [AKS 클러스터 만들기](https://docs.microsoft.com/azure/aks/create-cluster)합니다.
>
> Kubernetes의 최신 버전을 사용 합니다. 특정 버전 구독 및 지역에 따라 달라 집니다. 참조 [AKS의 Kubernetes 지원 버전](https://docs.microsoft.com/en-us/azure/aks/supported-kubernetes-versions)합니다.  
>
> 다음 스크립트는 Azure에서 4 개 노드 Kubernetes 클러스터를 만듭니다. Replace 하는 스크립트를 실행 하기 전에 `<latest version>` 사용 가능한 최신 버전으로 합니다. 예를 들면 `1.12.5`입니다.
>
> ```azure-cli
> az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version <latest version> --generate-ssh-keys
> ```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>연산자, SQL Server 컨테이너 및 부하 분산 서비스를 배포 합니다.

1. 만들기는 [네임 스페이스](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)합니다.

      이 예제에서는 라는 네임 스페이스 `ag1`합니다. 네임 스페이스를 만들려면 다음 명령을 실행 합니다.
    
      ```azurecli
      kubectl create namespace ag1
      ```
    
      이 솔루션에 속하는 모든 개체에는 `ag1` 네임 스페이스입니다.

1. 구성 하 고 SQL Server 연산자 매니페스트를 배포 합니다.

      SQL Server 복사 [ `operator.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml) 에서 파일 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)합니다.
    
      `operator.yaml` Kubernetes 연산자에 대 한 배포 매니페스트 파일이 있습니다.
    
      매니페스트는 Kubernetes 클러스터에 적용 됩니다.
    
      ```azurecli
      kubectl apply -f operator.yaml --namespace ag1
      ```
    
1. 에 대 한 암호를 사용 하 여 kubernetes 비밀 만들기는 `sa` 계정 및 SQL Server 인스턴스의 마스터 키입니다.

      사용 하 여 비밀을 만들 `kubectl`합니다.
      
      다음 예제에서는 라는 비밀 `sql-secrets` 에 `ag1` 네임 스페이스입니다. 암호는 두 개의 암호를 저장합니다.
      
      - `sapassword` SQL Server에 대 한 암호를 저장 `sa` 계정.
      - `masterkeypassword` SQL Server 마스터 키를 만드는 데 사용한 암호를 저장 합니다. 
    
   터미널에 스크립트를 복사 합니다. 각 대체 `<>` 복잡 한 암호와 암호를 만드는 스크립트를 실행 합니다.
    
   >[!NOTE]
   >암호를 사용할 수 없습니다 `&` 또는 `` ` `` 문자입니다.
    
   ```azurecli
   kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
   ```

1. SQL Server 사용자 지정 리소스를 배포 합니다.

      SQL Server 매니페스트를 복사 [ `sqlserver.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml) 에서 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)합니다.
    
      >[!NOTE]
      >`sqlserver.yaml` 파일 SQL Server 컨테이너, 영구적 볼륨 클레임, 영구적 볼륨 및 각 SQL Server 인스턴스에 대 한 필요한 부하 분산 서비스를 설명 합니다.
    
      매니페스트는 Kubernetes 클러스터에 적용 됩니다.
    
      ```azurecli
      kubectl apply -f sqlserver.yaml --namespace ag1
      ```
      
다음 이미지는 성공적인 응용 프로그램의 표시 `kubectl apply` 예입니다.

![sqlservers 만들기](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

SQL Server 매니페스트를 적용 하면 연산자는 SQL Server 컨테이너를 배포 합니다.

Kubernetes는 pod에 컨테이너를 배치합니다. 사용 하 여 `kubectl get pods --namespace ag1` pod의 상태를 확인 합니다. 다음 이미지는 SQL Server pod를 배포한 후 배포를 예제를 보여줍니다. 

![pod를 작성합니다.](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>배포 모니터링

사용할 수는 [Azure Kubernetes Service를 사용 하 여 Kubernetes 대시보드](https://docs.microsoft.com/azure/aks/kubernetes-dashboard) 배포를 모니터링 하려면.

사용 하 여 `az aks browse` 대시보드를 시작 합니다. 

## <a name="connect-to-the-availability-group-with-the-services"></a>서비스를 사용 하 여 가용성 그룹에 연결

합니다 [ `ag-services.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) 에서 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) 예제 가용성 그룹 복제본에 연결할 수 있는 부하 분산 서비스에 설명 합니다. 

- `ag1-primary` 주 복제본에 연결 하기 위한 끝점을 제공 합니다.
- `ag1-secondary` 모든 보조 복제본에 연결 하기 위한 끝점을 제공 합니다.

Kubernetes 매니페스트 파일에 적용 하면 복제본의 각 형식에 대 한 부하 분산 서비스를 만듭니다. 부하 분산 서비스 IP 주소를 포함합니다. 이 IP 주소를 사용 하 여 해야 하는 복제 유형에 연결할 수 있습니다.

서비스를 배포 하려면 다음 명령을 실행 합니다.

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

사용 하 여 서비스를 배포한 후 `kubectl get services --namespace ag1` 서비스에 대 한 IP 주소를 식별 합니다.

IP 주소를 사용 하 여 연결할 수 있습니다 SQL Server 인스턴스를 호스팅하는 복제본의 각 형식.

다음 이미지를 보여 줍니다.

- 출력 `kubectl get services` 네임 스페이스에 대 한 `ag1`합니다.

- 각 SQL Server 컨테이너에 대해 생성 된 부하 분산 서비스입니다. 끝점으로 이러한 IP 주소를 사용 하 여 클러스터에서 SQL Server의 인스턴스를 직접 연결할 수 있습니다.

- `sqlcmd` 주 복제본에 연결 된는 `sa` 부하 분산 장치 끝점을 통해 계정.

![연결](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>가용성 그룹에 데이터베이스 추가

>[!NOTE]
>지금은 SQL Server Management Studio를 가용성 그룹에 데이터베이스를 추가할 수 없습니다. TRANSACT-SQL을 사용 합니다.

Kubernetes에서 SQL Server 컨테이너를 만든 후 가용성 그룹에 데이터베이스를 추가 하려면 다음 단계를 완료 합니다.

1. [연결](sql-server-linux-kubernetes-connect.md) 클러스터의 SQL Server 인스턴스에 있습니다.

1. 데이터베이스를 만듭니다.

      ```sql
      CREATE DATABASE [demodb]
      ```

1. 전체 로그 체인을 시작 하려면 데이터베이스 백업을 수행 합니다.

      ```sql
      USE MASTER
      GO
      BACKUP DATABASE [demodb] 
      TO DISK = N'/var/opt/mssql/data/demodb.bak'
      ```

1. 가용성 그룹에 데이터베이스를 추가 합니다.

      ```sql
      ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [demodb]
      ```
    
SQL Server 보조 복제본을 자동으로 만들 수 있도록 자동 시드 가용성 그룹 생성 됩니다.

SQL Server Management Studio 가용성 그룹 대시보드를 통해 가용성 그룹의 상태를 볼 수 있습니다.

![대시보드](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>다음 단계

- [Kubernetes 클러스터에 SQL Server 가용성 그룹에 연결](sql-server-linux-kubernetes-connect.md)

- [Kubernetes 클러스터에 SQL Server 가용성 그룹 관리](sql-server-linux-kubernetes-manage.md)

- [SQL Server는 가용성 그룹을 Kubernetes 클러스터에서 컨테이너에 대 한 지원](sql-server-ag-kubernetes.md)
