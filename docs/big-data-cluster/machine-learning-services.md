---
title: Machine Learning Services(Python, R)
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 빅 데이터 클러스터의 마스터 인스턴스에서 Machine Learning Services를 사용하여 Python 및 R 스크립트를 실행하는 방법을 알아봅니다.
author: dphansen
ms.author: davidph
ms.date: 04/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: a14258c15ac1af1445b201f7b999dbec1682555d
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196931"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터에서 Machine Learning Services를 사용하여 Python 및 R 스크립트 실행

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

[SQL Server 빅 데이터 클러스터](big-data-cluster-overview.md)에서 [Machine Learning Services](../machine-learning/index.yml)를 사용하여 Python 및 R 스크립트를 실행할 수 있습니다.

> [!NOTE]
> [SQL Server 언어 확장](../language-extensions/language-extensions-overview.md)을 사용하면 마스터 인스턴스에서 Java 코드를 실행할 수도 있습니다. 다음 단계를 수행하면 언어 확장도 사용하도록 설정됩니다.

## <a name="enable-machine-learning-services"></a>Machine Learning Services 사용 설정

Machine Learning Services는 빅 데이터 클러스터에 기본적으로 설치되며 별도의 설치가 필요하지 않습니다.

Machine Learning Services를 사용하려면 마스터 인스턴스에서 다음 문을 실행합니다.

```sql
EXEC sp_configure 'external scripts enabled', 1
RECONFIGURE WITH OVERRIDE
GO
```

이제 빅 데이터 클러스터의 마스터 인스턴스에서 Python 및 R 스크립트를 실행할 준비가 되었습니다. [다음 단계](#next-steps)의 빠른 시작을 참고하여 첫 번째 스크립트를 실행하세요.

>[!NOTE]
>가용성 그룹 수신기 연결에는 구성 설정을 설정할 수 없습니다. 빅 데이터 클러스터가 고가용성으로 배포된 경우, 각 복제본에서 `external scripts enabled`를 설정합니다. [고가용성 클러스터에서 사용하도록 설정](#enable-on-cluster-with-high-availability)을 참조하세요.

## <a name="enable-on-cluster-with-high-availability"></a>고가용성 클러스터에서 사용하도록 설정

[SQL Server 빅 데이터 클러스터를 고가용성으로 배포](deployment-high-availability.md)하면 배포가 마스터 인스턴스에 대해 가용성 그룹을 만듭니다. Machine Learning Services를 사용하도록 설정하려면 가용성 그룹의 각 인스턴스에서 `external scripts enabled`를 설정합니다. 빅 데이터 클러스터의 경우 SQL Server 마스터 인스턴스의 각 복제본에서 `sp_configure`를 실행해야 합니다.

다음 섹션에서는 각 인스턴스에서 외부 스크립트를 사용하도록 설정하는 방법을 설명합니다.

### <a name="create-an-external-load-balancer-for-each-instance"></a>각 인스턴스에 대해 외부 부하 분산 장치 만들기

가용성 그룹에 있는 각 복제본에 대해, 인스턴스에 연결할 수 있도록 부하 분산 장치를 만듭니다. 

`kubectl expose pod <pod-name> --port=<connection port number> --name=<load-balancer-name> --type=LoadBalancer -n <kubernetes namespace>`

이 문서의 예제에서는 다음 값을 사용합니다.

- `<pod-name>`: `master-#`
- `<connection port number>`: `1533`
- `<load-balancer-name>`: `mymaster-#`
- `<kubernetes namespace>`: `mssql-cluster`

환경에 맞게 다음 스크립트를 업데이트하고, 명령을 실행합니다.

```bash
kubectl expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer -n mssql-cluster 
kubectl expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer -n mssql-cluster
kubectl expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer -n mssql-cluster 
```

`kubectl`은 다음 출력을 반환합니다.

```bash
service/mymaster-0 exposed
service/mymaster-1 exposed
service/mymaster-2 exposed
```

각 부하 분산 장치는 마스터 복제본 엔드포인트입니다.

### <a name="enable-script-execution-on-each-replica"></a>각 복제본에서 스크립트 실행을 사용하도록 설정

1. 마스터 복제본 엔드포인트의 IP 주소를 가져옵니다.

   다음 명령은 복제본 엔드포인트의 외부 IP 주소를 반환합니다. 

   `kubectl get services <load-balancer-name> -n <kubernetes namespace>`

   이 시나리오에서 각 복제본의 외부 IP 주소를 가져오려면 다음 명령을 실행합니다.

   ```bash
   kubectl get services mymaster-0 -n mssql-cluster
   kubectl get services mymaster-1 -n mssql-cluster
   kubectl get services mymaster-2 -n mssql-cluster
   ```

   >[!NOTE]
   > 외부 IP 주소를 확인할 수 있을 때까지 시간이 걸릴 수 있습니다. 각 엔드포인트가 모두 외부 IP 주소를 반환할 때까지 잎에 나온 스크립트를 주기적으로 실행합니다.

1. 마스터 복제본 엔드포인트에 연결하고 스크립트 실행을 사용하도록 설정합니다.

    다음 문을 실행합니다.

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

   예를 들어, 앞에 나온 명령을 `sqlcmd`로 실행할 수 있습니다. 다음 예제에서는 마스터 복제본 엔드포인트에 연결하고 스크립트 실행을 사용하도록 설정합니다. 환경에 맞게 스크립트의 값을 업데이트합니다.

   ```bash
   sqlcmd -S <IP address>,1533 -U <user name> -P <password> -Q "EXEC sp_configure 'external scripts enabled', 1; RECONFIGURE WITH OVERRIDE;"
   ```

   각 복제본에 대해 이 단계를 반복합니다.

### <a name="demonstration"></a>데모

다음 이미지에서는 이 프로세스를 보여 줍니다.

[![데모](media/machine-learning-services/example-kube-enable-scripts.png "Demonstrate enable feature on Kubernetes(Kubernetes에서 기능 설정 시연)")](media/machine-learning-services/example-kube-enable-scripts.png#lightbox)

이제 빅 데이터 클러스터의 마스터 인스턴스에서 Python 및 R 스크립트를 실행할 준비가 되었습니다. [다음 단계](#next-steps)의 빠른 시작을 참고하여 첫 번째 스크립트를 실행하세요.

### <a name="delete-the-master-replica-endpoints"></a>마스터 복제본 엔드포인트 삭제

Kubernetes 클러스터에서 각 복제본에 대해 엔드포인트를 삭제합니다. 엔드포인트는 Kubernetes에서 부하 분산 서비스로 노출됩니다.

다음 명령은 부하 분산 서비스를 삭제합니다.

`kubectl delete svc <load-balancer-name> -n mssql-cluster`

이 문서의 예제에서는 다음 명령을 실행합니다.

```bash
kubectl delete svc mymaster-0 -n mssql-cluster
kubectl delete svc mymaster-1 -n mssql-cluster
kubectl delete svc mymaster-2 -n mssql-cluster
```

## <a name="next-steps"></a>다음 단계

+ [간단한 Python 스크립트 실행](../machine-learning/tutorials/quickstart-python-create-script.md?toc=/sql/toc.json)
+ [Python에서 예측 모델 학습 및 점수 매기기](../machine-learning/tutorials/quickstart-python-train-score-model.md?toc=/sql/toc.json)
+ [간단한 R 스크립트 실행](../machine-learning/tutorials/quickstart-r-create-script.md?toc=/sql/toc.json)
+ [R에서 예측 모델 학습 및 점수 매기기](../machine-learning/tutorials/quickstart-r-train-score-model.md?toc=/sql/toc.json)
