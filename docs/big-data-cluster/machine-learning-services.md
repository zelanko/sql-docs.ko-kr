---
title: Machine Learning Services(Python, R)
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 빅 데이터 클러스터의 마스터 인스턴스에서 Machine Learning Services를 사용하여 Python 및 R 스크립트를 실행하는 방법을 알아봅니다.
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
ms.openlocfilehash: e16304765e5f4a51feed4d3d59e790505baa740d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75252029"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터에서 Machine Learning Services를 사용하여 Python 및 R 스크립트 실행

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[SQL Server 빅 데이터 클러스터](big-data-cluster-overview.md)에서 [Machine Learning Services](../advanced-analytics/index.yml)를 사용하여 Python 및 R 스크립트를 실행할 수 있습니다.

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

## <a name="enable-always-on-availability-groups"></a>Always On 가용성 그룹 사용

[Always On 가용성 그룹](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)에서 SQL Server 빅 데이터 클러스터를 사용하는 경우 Machine Learning Services를 사용하려면 몇 가지 단계를 추가로 수행해야 합니다.

1. 마스터 인스턴스에 연결하고 다음 문을 실행합니다.

    ```sql
    SELECT @@SERVERNAME
    ```

    서버 이름을 기록해 둡니다. 이 예제에서 마스터 인스턴스의 서버 이름은 **master-2**입니다.

1. 빅 데이터 클러스터의 Always On 가용성 그룹에 있는 각 복제본에서 다음 `kubectl` 명령을 실행합니다.

    ```
    kubectl -n bdc expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer

    kubectl -n bdc expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer

    kubectl -n bdc expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer
    ```

    다음과 비슷한 내용이 출력됩니다.
    
    ```
    service/mymaster-0 exposed

    service/mymaster-1 exposed

    service/mymaster-2 exposed
    ```

1. 각 마스터 복제본 엔드포인트에 연결하고 스크립트 실행을 사용하도록 설정합니다.

    다음 문을 실행합니다.

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

이제 빅 데이터 클러스터의 마스터 인스턴스에서 Python 및 R 스크립트를 실행할 준비가 되었습니다. 아래의 빠른 시작을 참고하여 첫 번째 스크립트를 실행하세요.

## <a name="next-steps"></a>다음 단계

+ [빠른 시작: SQL Server Machine Learning Services를 사용하여 간단한 Python 스크립트 만들기 및 실행](../advanced-analytics/tutorials/quickstart-python-create-script.md)
+ [빠른 시작: SQL Server Machine Learning Services를 사용하여 Python에서 예측 모델 만들기 및 점수 매기기](../advanced-analytics/tutorials/quickstart-python-train-score-model.md)
+ [빠른 시작: SQL Server Machine Learning Services를 사용하여 간단한 R 스크립트 만들기 및 실행](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [빠른 시작: SQL Server Machine Learning Services를 사용하여 R에서 예측 모델 만들기 및 점수 매기기](../advanced-analytics/tutorials/quickstart-r-train-score-model.md)
