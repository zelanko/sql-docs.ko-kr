---
title: AKS(Azure Kubernetes Services)를 사용하여 SQL Server 컨테이너 배포
description: 이 자습서에서는 Azure Kubernetes Service의 Kubernetes를 사용하여 SQL Server 고가용성 솔루션을 배포하는 방법을 보여 줍니다.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 91607fd8a7bc7b3b104de6d0ba3e6ce97cab8137
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558353"
---
# <a name="deploy-a-sql-server-container-in-kubernetes-with-azure-kubernetes-services-aks"></a>AKS(Azure Kubernetes Services)를 사용하여 Kubernetes에 SQL Server 컨테이너 배포

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

HA(고가용성)를 위한 영구적 스토리지를 사용하여 AKS(Azure Kubernetes Service)의 Kubernetes에서 SQL Server 인스턴스를 구성하는 방법을 알아봅니다. 이 솔루션은 복원력을 제공합니다. SQL Server 인스턴스가 실패하면 Kubernetes가 새 Pod에서 자동으로 다시 만듭니다. Kubernetes는 노드 실패에 대한 복원력도 제공합니다.

이 자습서에서는 AKS의 컨테이너에서 고가용성 SQL Server 인스턴스를 구성하는 방법을 보여 줍니다.

> [!div class="checklist"]
> * SA 암호 만들기
> * 스토리지 만들기
> * 배포 만들기
> * SSMS(SQL Server Management Studio)를 사용하여 연결
> * 실패 및 복구 확인

## <a name="ha-solution-on-kubernetes-running-in-azure-kubernetes-service"></a>Azure Kubernetes Service에서 실행되는 Kubernetes의 HA 솔루션

Kubernetes 1.6 이상에서는 [스토리지 클래스](https://kubernetes.io/docs/concepts/storage/storage-classes/), [영구적 볼륨 클레임](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims) 및 [Azure 디스크 볼륨 유형](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)을 지원합니다. Kubernetes에서 기본적으로 SQL Server 인스턴스를 만들고 관리할 수 있습니다. 이 문서의 예제에서는 [배포](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)를 만들어 공유 디스크 장애 조치(failover) 클러스터 인스턴스와 비슷한 고가용성 구성을 얻는 방법을 보여 줍니다. 이 구성에서 Kubernetes는 클러스터 오케스트레이터의 역할을 수행합니다. 컨테이너의 SQL Server 인스턴스가 실패하면 오케스트레이터는 동일한 영구적 스토리지에 연결된 또 다른 컨테이너 인스턴스를 부트스트랩합니다.

![Kubernetes SQL Server 클러스터의 다이어그램](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

위 다이어그램에서 `mssql-server`는 [Pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/)의 컨테이너입니다. Kubernetes는 클러스터의 리소스를 오케스트레이션합니다. [복제본 세트](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)는 노드 실패 후에 Pod가 자동으로 복구되도록 합니다. 애플리케이션이 서비스에 연결됩니다. 이 경우 서비스는 `mssql-server` 실패 후에도 동일하게 유지되는 IP 주소를 호스트하는 부하 분산 장치를 나타냅니다.

다음 다이어그램에서는 `mssql-server` 컨테이너에서 오류가 발생했습니다. 오케스트레이터인 Kubernetes는 복제본 세트에 올바른 개수의 정상적인 인스턴스가 있도록 보장하고 구성에 따라 새 컨테이너를 시작합니다. 오케스트레이터가 동일한 노드에서 새 Pod를 시작하고, `mssql-server`가 동일한 영구적 스토리지에 다시 연결됩니다. 서비스가 다시 생성된 `mssql-server`에 연결됩니다.

![Kubernetes SQL Server 클러스터의 다이어그램](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

다음 다이어그램에서는 `mssql-server` 컨테이너를 호스트하는 노드에서 오류가 발생했습니다. 오케스트레이터가 다른 노드에서 새 Pod를 시작하고, `mssql-server`가 동일한 영구적 스토리지에 다시 연결됩니다. 서비스가 다시 생성된 `mssql-server`에 연결됩니다.

![Kubernetes SQL Server 클러스터의 다이어그램](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>사전 요구 사항

* **Kubernetes 클러스터**
   - 이 자습서를 완료하려면 Kubernetes 클러스터가 필요합니다. 이 단계에서는 [kubectl](https://kubernetes.io/docs/user-guide/kubectl/)을 사용하여 클러스터를 관리합니다. 

   - `kubectl`을 사용하여 AKS에서 단일 노드 Kubernetes 클러스터를 만들고 연결하려면 [AKS(Azure Container Service) 클러스터 배포](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster)를 참조하세요. 

   >[!NOTE]
   >노드 오류로부터 보호하려면 Kubernetes 클러스터에 두 개 이상의 노드가 필요합니다.

* **Azure CLI 2.0.23**
   - 이 자습서의 지침은 Azure CLI 2.0.23에서 유효성이 검사되었습니다.

## <a name="create-an-sa-password"></a>SA 암호 만들기

Kubernetes 클러스터에서 SA 암호를 만듭니다. Kubernetes는 [비밀](https://kubernetes.io/docs/concepts/configuration/secret/) 등의 암호와 같은 중요한 구성 정보를 관리할 수 있습니다.

다음 명령은 SA 계정의 암호를 만듭니다.

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   `MyC0m9l&xP@ssw0rd`를 복잡한 암호로 바꿉니다.

   `SA_PASSWORD`의 값 `MyC0m9l&xP@ssw0rd`를 포함하는 `mssql`이라는 비밀을 Kubernetes에서 만들려면 다음 명령을 실행합니다.


## <a name="create-storage"></a>스토리지 만들기

Kubernetes 클러스터에서 [영구적 볼륨](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) 및 [영구적 볼륨 클레임](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection)을 구성합니다. 다음 단계를 완료합니다. 

1. 스토리지 클래스 및 영구적 볼륨 클레임을 정의하는 매니페스트를 만듭니다.  매니페스트는 스토리지 프로비저닝 프로그램, 매개 변수 및 [회수 정책](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming)을 지정합니다. Kubernetes 클러스터는 이 매니페스트를 사용하여 영구적 스토리지를 만듭니다. 

   다음 yaml 예제에서는 스토리지 클래스 및 영구적 볼륨 클레임을 정의합니다. 이 Kubernetes 클러스터가 Azure에 있기 때문에 스토리지 클래스 프로비저닝 프로그램은 `azure-disk`입니다. 스토리지 계정 유형은 `Standard_LRS`입니다. 영구적 볼륨 클레임의 이름은 `mssql-data`입니다. 영구적 볼륨 클레임 메타데이터에는 스토리지 클래스에 다시 연결하는 주석이 포함되어 있습니다. 

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

   파일(예: **pvc.yaml**)을 저장합니다.

1. Kubernetes에서 영구적 볼륨 클레임을 만듭니다.

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>`은 파일을 저장한 위치입니다.

   영구적 볼륨은 Azure Storage 계정으로 자동으로 생성되고 영구적 볼륨 클레임에 바인딩됩니다. 

    ![영구적 볼륨 클레임 명령 스크린샷](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. 영구적 볼륨 클레임을 확인합니다.

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>`은 영구적 볼륨 클레임의 이름입니다.

   이전 단계에서 영구적 볼륨 클레임의 이름은 `mssql-data`입니다. 영구적 볼륨 클레임에 대한 메타데이터를 확인하려면 다음 명령을 실행합니다.

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   반환된 메타데이터에는 `Volume`이라는 값이 있습니다. 이 값은 Blob의 이름에 매핑됩니다.

   ![Volume을 포함하여 반환된 메타데이터 스크린샷](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   볼륨의 값은 Azure Portal에서 캡처된 다음 그림에 있는 Blob 이름의 일부와 일치합니다. 

   ![Azure Portal Blob 이름 스크린샷](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. 영구적 볼륨을 확인합니다.

   ```azurecli
   kubectl describe pv
   ```

   `kubectl`이 자동으로 생성되어 영구적 볼륨 클레임에 바인딩된 영구적 볼륨에 대한 메타데이터를 반환합니다. 

## <a name="create-the-deployment"></a>배포 만들기

이 예제에서는 SQL Server 인스턴스를 호스트하는 컨테이너를 Kubernetes 배포 개체로 설명합니다. 배포는 복제본 세트를 만듭니다. 복제본 세트는 Pod를 만듭니다. 

이 단계에서는 SQL Server [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) Docker 이미지를 기반으로 하는 컨테이너를 설명하는 매니페스트를 만듭니다. 매니페스트는 `mssql-server` 영구적 볼륨 클레임 및 Kubernetes 클러스터에 이미 적용된 `mssql` 비밀을 참조합니다. 또한 매니페스트는 [서비스](https://kubernetes.io/docs/concepts/services-networking/service/)를 설명합니다. 이 서비스는 부하 분산 장치입니다. 부하 분산 장치는 SQL Server 인스턴스가 복구된 후에도 IP 주소가 유지되도록 보장합니다. 

1. 배포를 설명하는 매니페스트(YAML 파일)를 만듭니다. 다음 예제에서는 SQL Server 컨테이너 이미지를 기반으로 하는 컨테이너를 포함하여 배포를 설명합니다.

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

   앞의 코드를 `sqldeployment.yaml`이라는 새 파일에 복사합니다. 다음 값을 업데이트합니다. 

   * MSSQL_PID `value: "Developer"`: SQL Server Developer Edition을 실행할 컨테이너를 설정합니다. Developer Edition은 프로덕션 데이터에 사용할 수 없습니다. 프로덕션용으로 배포하는 경우 적절한 버전(`Enterprise`, `Standard` 또는 `Express`)을 설정합니다. 

      >[!NOTE]
      >자세한 내용은 [SQL Server 라이선스 획득 방법](https://www.microsoft.com/sql-server/sql-server-2017-pricing)을 참조하세요.

   * `persistentVolumeClaim`: 이 값에는 영구적 볼륨 클레임의 이름에 매핑되는 `claimName:` 항목이 필요합니다. 이 자습서에서는 `mssql-data`를 사용합니다. 

   * `name: SA_PASSWORD`: 이 섹션에 정의된 대로 SA 암호를 설정하도록 컨테이너 이미지를 구성합니다.

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     Kubernetes는 컨테이너를 배포할 때 암호의 값을 얻기 위해 `mssql`이라는 비밀을 참조합니다. 

   >[!NOTE]
   >`LoadBalancer` 서비스 유형을 사용하면 포트 1433에서 인터넷을 통해 원격으로 SQL Server 인스턴스에 액세스할 수 있습니다.

   파일(예: **sqldeployment.yaml**)을 저장합니다.

1. 배포를 만듭니다.

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>`은 파일을 저장한 위치입니다.

   ![배포 명령 스크린샷](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   배포 및 서비스가 만들어집니다. SQL Server 인스턴스는 영구적 스토리지에 연결된 컨테이너에 있습니다.

   Pod의 상태를 보려면 `kubectl get pod`를 입력합니다.

   ![Pod 가져오기 명령 스크린샷](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   앞의 그림에서는 Pod가 `Running` 상태입니다. 이 상태는 컨테이너가 준비되었음을 나타냅니다. 이 작업은 몇 분 정도 걸릴 수 있습니다.

   >[!NOTE]
   >배포를 만든 후에 Pod가 표시될 때까지 몇 분 정도 걸릴 수 있습니다. 이 지연은 클러스터가 Docker 허브에서 [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) 이미지를 끌어오기 때문에 발생합니다. 이미지를 처음 끌어온 후, 해당 이미지가 이미 캐시되어 있는 노드에 배포하는 경우 후속 배포는 더 빨라질 수 있습니다. 

1. 서비스가 실행되고 있는지 확인합니다. 다음 명령 실행:

   ```azurecli
   kubectl get services 
   ```

   이 명령은 서비스의 내부 및 외부 IP 주소뿐만 아니라 실행 중인 서비스도 반환합니다. `mssql-deployment` 서비스의 외부 IP 주소를 적어 둡니다. 이 IP 주소를 사용하여 SQL Server에 연결합니다. 

   ![get service 명령 스크린샷](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Kubernetes 클러스터의 개체 상태에 대한 자세한 내용을 보려면 다음 명령을 실행합니다.

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>SQL Server 인스턴스에 연결

설명에 따라 컨테이너를 구성한 경우 Azure 가상 네트워크 외부에서 애플리케이션에 연결할 수 있습니다. `sa` 계정과 서비스의 외부 IP 주소를 사용합니다. Kubernetes 비밀로 구성한 암호를 사용합니다. 

다음 애플리케이션을 사용하여 SQL Server 인스턴스에 연결할 수 있습니다. 

* [SSMS](https://docs.microsoft.com/sql/linux/sql-server-linux-manage-ssms)

* [SSDT](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   `sqlcmd`에 연결하려면 다음 명령을 실행합니다.

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   다음 값을 바꿉니다.
      
    - `<External IP Address>`를 `mssql-deployment` 서비스의 IP 주소로 바꿉니다. 
    - `MyC0m9l&xP@ssw0rd`를 해당 암호로 바꿉니다.

## <a name="verify-failure-and-recovery"></a>실패 및 복구 확인

실패 및 복구를 확인하기 위해 Pod를 삭제할 수 있습니다. 다음 단계를 수행합니다.

1. SQL Server를 실행하는 Pod를 나열합니다.

   ```azurecli
   kubectl get pods
   ```

   SQL Server를 실행하는 Pod의 이름을 적어 둡니다.

1. Pod를 삭제합니다.

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0`은 Pod 이름으로 이전 단계에서 반환된 값입니다. 

Kubernetes는 Pod를 자동으로 다시 만들어 SQL Server 인스턴스를 복구하고 영구적 스토리지에 연결합니다. `kubectl get pods`를 사용하여 새 Pod가 배포되었는지 확인합니다. `kubectl get services`를 사용하여 새 컨테이너의 IP 주소가 동일한지 확인합니다. 

## <a name="summary"></a>요약

이 자습서에서는 고가용성을 위해 Kubernetes 클러스터에 SQL Server 컨테이너를 배포하는 방법을 알아보았습니다. 

> [!div class="checklist"]
> * SA 암호 만들기
> * 스토리지 만들기
> * 배포 만들기
> * SSMS(SQL Server Management Studio)를 사용하여 연결
> * 실패 및 복구 확인

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
>[Kubernetes 소개](https://docs.microsoft.com/azure/aks/intro-kubernetes)


