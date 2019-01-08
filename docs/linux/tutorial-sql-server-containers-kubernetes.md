---
title: Azure Kubernetes 서비스 (AKS)를 사용 하 여 Kubernetes에서 SQL Server 컨테이너 배포 | Microsoft Docs
description: 이 자습서에서는 Azure Kubernetes Service에서 Kubernetes 사용 하 여 SQL Server 고가용성 솔루션을 배포 하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: sql-linux,mvc
ms.technology: linux
ms.openlocfilehash: 669d02d32642ba4723892a98a1f4d0f3bc6e51f6
ms.sourcegitcommit: c51f7f2f5d622a1e7c6a8e2270bd25faba0165e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53626323"
---
# <a name="deploy-a-sql-server-container-in-kubernetes-with-azure-kubernetes-services-aks"></a>Azure Kubernetes 서비스 (AKS)를 사용 하 여 Kubernetes에서 SQL Server 컨테이너를 배포 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

고가용성 (HA)에 대 한 영구 저장소를 사용 하 여 Azure Kubernetes Service (AKS)에서 Kubernetes에 SQL Server 인스턴스를 구성 하는 방법에 알아봅니다. 솔루션 복원 력을 제공 합니다. SQL Server 인스턴스가 실패 하면 Kubernetes 자동으로 다시 만듭니다 새 pod에서입니다. Kubernetes 노드 실패에 대 한 복원 력을 제공합니다.

이 자습서에는 AKS 컨테이너에 항상 사용 가능한 SQL Server 인스턴스를 구성 하는 방법을 보여 줍니다. 만들 수도 있습니다 [SQL Server 컨테이너에 대 한 Always On 가용성 그룹](sql-server-ag-kubernetes.md)합니다. 두 가지 다른 Kubernetes 솔루션 비교를 참조 하세요 [SQL Server 컨테이너에 대 한 고가용성](sql-server-linux-container-ha-overview.md)합니다.

> [!div class="checklist"]
> * SA 암호를 만들려면
> * 저장소 만들기
> * 배포 만들기
> * SQL Server Management Studio (SSMS)를 사용 하 여 연결
> * 오류 및 복구를 확인 합니다.

## <a name="ha-solution-on-kubernetes-running-in-azure-kubernetes-service"></a>Azure Kubernetes Service에서 실행 중인 Kubernetes에서 HA 솔루션

Kubernetes 버전 1.6 이상에 대 한 지원 [저장소 클래스](https://kubernetes.io/docs/concepts/storage/storage-classes/), [영구적 볼륨 클레임](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims), 및 [Azure 디스크 볼륨 형식](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)합니다. 만들기 및 Kubernetes에 기본적으로 SQL Server 인스턴스를 관리할 수 있습니다. 이 문서의 예제에서에서 만드는 방법을 보여 줍니다.는 [배포](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) 공유 디스크 장애 조치 클러스터 인스턴스에 유사한 고가용성 구성을 위해. 이 구성에서는 Kubernetes 클러스터 오 케 스트레이 터의 역할을 재생합니다. 컨테이너에서 SQL Server 인스턴스를 실패 한 경우는 오 케 스트레이 터 같은 영구 저장소에 연결 하는 컨테이너의 다른 인스턴스를 부트스트랩 합니다.

![Kubernetes SQL Server 클러스터의 다이어그램](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

위의 다이어그램에서 `mssql-server` 은 컨테이너에는 [pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/)합니다. Kubernetes는 클러스터의 리소스를 조정합니다. A [복제본 세트](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) pod가 노드 실패 후 자동으로 복구 하 고 있는지 확인 합니다. 응용 프로그램 서비스에 연결 합니다. 이 경우 서비스를 나타내는 실패 후에 동일 하 게 유지 하는 IP 주소를 호스트 하는 부하 분산 장치는 `mssql-server`합니다.

다음 다이어그램에는 `mssql-server` 컨테이너에 실패 했습니다. 오 케 스트레이 터로 Kubernetes 복제본에 정상 인스턴스의 정확한 수를 설정 및 구성에 따라 새 컨테이너를 시작을 보장 합니다. 오 케 스트레이 터 같은 노드에서 새 pod를 시작 하 고 `mssql-server` 같은 영구 저장소에 다시 연결 합니다. 서비스에 다시 만들어진 연결 `mssql-server`합니다.

![Kubernetes SQL Server 클러스터의 다이어그램](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

다음 다이어그램에서 호스트 하는 노드는 `mssql-server` 컨테이너에 실패 했습니다. Orchestrator 다른 노드에서 새 pod를 시작 하 고 `mssql-server` 같은 영구 저장소에 다시 연결 합니다. 서비스에 다시 만들어진 연결 `mssql-server`합니다.

![Kubernetes SQL Server 클러스터의 다이어그램](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>사전 요구 사항

* **Kubernetes 클러스터**
   - 이 자습서에는 Kubernetes 클러스터에 필요합니다. 단계를 사용 하 여 [kubectl](https://kubernetes.io/docs/user-guide/kubectl/) 클러스터를 관리 합니다. 

   - 참조 [Azure Container Service (AKS) 클러스터 배포](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster) 를 만들고 사용 하 여 AKS에서 단일 노드 Kubernetes 클러스터에 연결 `kubectl`합니다. 

   >[!NOTE]
   >노드 오류를 방지 하려면 Kubernetes 클러스터에는 둘 이상의 노드가 필요 합니다.

* **Azure CLI 2.0.23**
   - 이 자습서의 지침은 Azure CLI 2.0.23에 대해 유효성이 확인 된 합니다.

## <a name="create-an-sa-password"></a>SA 암호를 만들려면

Kubernetes 클러스터에서 SA 암호를 만듭니다. Kubernetes로 암호와 같은 중요 한 구성 정보를 관리할 수 있습니다 [비밀](https://kubernetes.io/docs/concepts/configuration/secret/)합니다.

다음 명령은 SA 계정의 암호를 만듭니다.

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   대체 `MyC0m9l&xP@ssw0rd` 복잡 한 암호를 사용 하 여 합니다.

   이라는 kubernetes 비밀을 만들려면 `mssql` 값을 보유 하는 `MyC0m9l&xP@ssw0rd` 에 대 한는 `SA_PASSWORD`, 명령을 실행 합니다.


## <a name="create-storage"></a>저장소 만들기

구성 된 [영구적 볼륨](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) 및 [영구적 볼륨 클레임](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection) Kubernetes 클러스터에서. 다음 단계를 수행 합니다. 

1. 영구적 볼륨 및 저장소 클래스를 정의 하는 매니페스트를 만듭니다 클레임입니다.  매니페스트는 저장소 프로 비 저 너를, 매개 변수를 지정 하 고 [회수 정책](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming)합니다. Kubernetes 클러스터는이 매니페스트를 사용 하 여 영구 저장소를 만듭니다. 

   다음 yaml 예제에서는 저장소 클래스와 영구적 볼륨 클레임을 정의합니다. 저장소 클래스 너는 `azure-disk`이므로 Azure에서 Kubernetes 클러스터가이 있습니다. 저장소 계정 유형이 `Standard_LRS`합니다. 영구적 볼륨 클레임이 이름은 `mssql-data`합니다. 영구적 볼륨 클레임 메타 데이터 주석 연결 저장소 클래스를 포함 합니다. 

   ```yaml
   kind: StorageClass
   apiVersion: storage.k8s.io/v1beta1
   metadata:
        name: azure-disk
   provisioner: kubernetes.io/azure-disk
   parameters:
     storageaccounttype: Standard_LRS
     kind: Managed
   ---
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: mssql-data
     annotations:
       volume.beta.kubernetes.io/storage-class: azure-disk
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi
   ```

   파일을 저장 합니다 (예를 들어 **pvc.yaml**).

1. Kubernetes에서 영구적 볼륨 클레임을 만듭니다.

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` 파일 저장 위치가입니다.

   영구적 볼륨이 자동으로 Azure storage 계정으로 만들어지고 영구적 볼륨 클레임에 바인딩됩니다. 

    ![영구적 볼륨 클레임 명령 스크린샷](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. 영구적 볼륨 클레임을 확인 합니다.

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` 영구적 볼륨 클레임의 이름이입니다.

   이전 단계에서 영구적 볼륨 클레임이 이름은 `mssql-data`합니다. 영구적 볼륨 클레임에 대 한 메타 데이터를 보려면 다음 명령을 실행 합니다.

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   호출 된 값을 포함 하는 반환된 된 메타 데이터 `Volume`입니다. 이 값은 blob의 이름에 매핑됩니다.

   ![볼륨을 포함 하 여 반환 된 메타 데이터의 스크린샷](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   Azure portal에서 다음 이미지에서 blob의 이름 부분 일치 하는 볼륨에 대 한 값: 

   ![Azure의 스크린 샷 포털 blob 이름](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. 영구적 볼륨을 확인 합니다.

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` 자동으로 만들어지고 영구적 볼륨 클레임 바인딩되는 영구적 볼륨에 대 한 메타 데이터를 반환 합니다. 

## <a name="create-the-deployment"></a>배포 만들기

이 예제에서는 SQL Server 인스턴스를 호스팅하는 컨테이너는 Kubernetes 배포 개체로 설명 되어 있습니다. 배포 된 복제본 집합을 만듭니다. 복제본 세트 pod를 만듭니다. 

이 단계에서는 SQL Server를 기반으로 컨테이너를 설명 하는 매니페스트를 만듭니다 [mssql server linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) Docker 이미지입니다. 매니페스트 참조를 `mssql-server` 영구적 볼륨 클레임 및 `mssql` Kubernetes 클러스터에 이미 적용 하는 암호입니다. 매니페스트도 설명 합니다.는 [서비스](https://kubernetes.io/docs/concepts/services-networking/service/)합니다. 이 서비스는 부하 분산 장치. 부하 분산 장치 IP 주소를 SQL Server 인스턴스를 복구한 후에 유지 되도록 보장 합니다. 

1. 배포를 설명 하는 매니페스트 (YAML 파일)를 만듭니다. 다음 예제에서는 SQL Server 컨테이너 이미지를 기반으로 컨테이너를 포함 하 여 배포를 설명 합니다.

   ```yaml
   apiVersion: apps/v1beta1
   kind: Deployment
   metadata:
     name: mssql-deployment
   spec:
     replicas: 1
     template:
       metadata:
         labels:
           app: mssql
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: mssql
           image: mcr.microsoft.com/mssql/server:2017-latest
           ports:
           - containerPort: 1433
           env:
           - name: MSSQL_PID
             value: "Developer"
           - name: ACCEPT_EULA
             value: "Y"
           - name: MSSQL_SA_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: mssql
                 key: SA_PASSWORD 
           volumeMounts:
           - name: mssqldb
             mountPath: /var/opt/mssql
         volumes:
         - name: mssqldb
           persistentVolumeClaim:
             claimName: mssql-data
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: mssql-deployment
   spec:
     selector:
       app: mssql
     ports:
       - protocol: TCP
         port: 1433
         targetPort: 1433
     type: LoadBalancer
   ```

   라는 새 파일에 앞의 코드를 복사 `sqldeployment.yaml`합니다. 다음 값을 업데이트 합니다. 

   * MSSQL_PID `value: "Developer"`: SQL Server Developer edition을 실행 하도록 컨테이너를 설정 합니다. Developer edition은 프로덕션 데이터에 대 한 허가 받지 않았습니다. 프로덕션 사용에 대 한 배포가 되 면 적절 한 버전을 설정 (`Enterprise`, `Standard`, 또는 `Express`). 

      >[!NOTE]
      >자세한 내용은 [SQL Server 라이선스 방법](https://www.microsoft.com/sql-server/sql-server-2017-pricing)합니다.

   * `persistentVolumeClaim`: 이 값에 대 한 항목이 필요한 `claimName:` 영구적 볼륨 클레임에 대 한 사용 되는 이름에 매핑되는 합니다. 이 자습서에서는 `mssql-data`합니다. 

   * `name: SA_PASSWORD`: 이 섹션에 정의 된 대로 SA 암호를 설정 하려면 컨테이너 이미지를 구성 합니다.

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     라는 비밀을 참조 하는 Kubernetes 컨테이너에 배포할 때 `mssql` 암호에 대 한 값을 가져오려고 합니다. 

   >[!NOTE]
   >사용 하 여는 `LoadBalancer` 서비스 유형, SQL Server 인스턴스가 원격 (인터넷을 통해 액세스할)을 포트 1433에서.

   파일을 저장 합니다 (예를 들어 **sqldeployment.yaml**).

1. 배포를 만듭니다.

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` 파일 저장 위치가입니다.

   ![배포 명령 스크린샷](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   배포 및 서비스 생성 됩니다. SQL Server 인스턴스가 영구 저장소에 연결 된 컨테이너 에서입니다.

   Pod의 상태를 확인 하려면 다음을 입력 `kubectl get pod`합니다.

   ![Get pod 명령 스크린샷](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   위의 이미지에서 pod의 상태는 `Running`합니다. 이 상태는 컨테이너 준비 되었음을 나타냅니다. 몇 분 정도 걸릴 수 있습니다.

   >[!NOTE]
   >배포를 만든 후 pod 표시 되기 전에 몇 분 정도 걸릴 수 있습니다. 클러스터에서 가져오는 지연 되므로 합니다 [mssql server linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) Docker 허브에서 이미지입니다. 이미지를 처음으로 가져오면 후에 캐시 된 이미지에 이미 있는 노드에 배포할 경우에 후속 배포 가속화할 수 있습니다. 

1. 서비스가 실행 중인지 확인 합니다. 다음 명령을 실행합니다.

   ```azurecli
   kubectl get services 
   ```

   이 명령은 실행 중인 서비스 뿐만 아니라 서비스에 대 한 내부 및 외부 IP 주소를 반환 합니다. 에 대 한 외부 IP 주소를 메모 합니다 `mssql-deployment` 서비스입니다. 이 IP 주소를 사용 하 여 SQL Server에 연결 합니다. 

   ![Get service 명령 스크린샷](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Kubernetes 클러스터에 있는 개체의 상태에 대 한 자세한 내용은 다음을 실행 합니다.

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>SQL Server 인스턴스에 연결

설명 된 대로 컨테이너를 구성한 경우에 Azure virtual network 외부에서 응용 프로그램을 사용 하 여 연결할 수 있습니다. 사용 된 `sa` 서비스에 대 한 계정 및 외부 IP 주소입니다. Kubernetes 비밀을 구성한 암호를 사용 합니다. 

SQL Server 인스턴스에 연결 하려면 다음 응용 프로그램을 사용할 수 있습니다. 

* [SSMS](https://docs.microsoft.com/sql/linux/sql-server-linux-manage-ssms)

* [SSDT](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   연결할 `sqlcmd`, 다음 명령을 실행 합니다.

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   다음 값을 바꿉니다.
      
    - `<External IP Address>` 에 대 한 IP 주소를 사용 하 여는 `mssql-deployment` 서비스 
    - `MyC0m9l&xP@ssw0rd` 암호를 사용 하 여

## <a name="verify-failure-and-recovery"></a>오류 및 복구를 확인 합니다.

오류 및 복구를 확인 하려면 pod를 삭제할 수 있습니다. 다음 단계를 수행 합니다.

1. SQL Server를 실행 하는 pod를 나열 합니다.

   ```azurecli
   kubectl get pods
   ```

   SQL Server를 실행 하는 pod의 이름을 note 합니다.

1. Pod를 삭제 합니다.

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0` pod 이름 이전 단계에서 값 반환 됩니다. 

Kubernetes 자동으로 다시는 pod를 만듭니다 SQL Server 인스턴스를 복구 하 여 영구 저장소에 연결 합니다. 사용 하 여 `kubectl get pods` 새 pod가 배포 되었는지 확인 합니다. 사용 하 여 `kubectl get services` 새 컨테이너에 대 한 ip가 동일한 지 확인 합니다. 

## <a name="summary"></a>요약

이 자습서에서는 고가용성을 위해 Kubernetes 클러스터에 SQL Server 컨테이너를 배포 하는 방법을 알아보았습니다. 

> [!div class="checklist"]
> * SA 암호를 만들려면
> * 저장소 만들기
> * 배포 만들기
> * SQL Server Management Studio (SSMS)를 사용 하 여 연결
> * 오류 및 복구를 확인 합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
>[Kubernetes 소개](https://docs.microsoft.com/azure/aks/intro-kubernetes)


