---
title: azdata 및 Grafana 대시보드를 사용하여 애플리케이션 모니터링
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 빅 데이터 클러스터에서 azdata 및 Grafana를 사용하여 애플리케이션을 모니터링합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 08/16/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1391b88f2762293aa4eebf255682605bf5b6b1e0
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257283"
---
# <a name="monitor-applications-with-azdata-and-grafana-dashboard"></a>azdata 및 Grafana 대시보드를 사용하여 애플리케이션 모니터링

Grafana는 Kubernetes에서 실행되는 애플리케이션의 다양한 모니터링 메트릭을 제공하는 데 사용할 수 있는 최고의 클라우드 네이티브 가상화 도구 중 하나입니다.  

이 문서에서는 SQL Server 빅 데이터 클러스터 내에서 애플리케이션을 모니터링하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>기능

SQL Server 2019에서 애플리케이션을 만들고, 삭제, 설명, 초기화, 나열, 실행 및 업데이트할 수 있습니다. 다음 표에서는 **azdata**와 함께 사용할 수 있는 애플리케이션 배포 명령을 설명합니다.

|명령 |설명 |
|:---|:---|
|`azdata bdc endpoint list` | 빅 데이터 클러스터의 엔드포인트를 나열합니다. |


다음 예제를 사용하여 **Grafana 대시보드**의 엔드포인트를 나열할 수 있습니다.

```bash
azdata bdc endpoint list --endpoint-name metricsui 
```

출력에서는 클러스터 사용자 이름 및 암호를 사용하여 로그인할 수 있는 엔드포인트를 제공합니다. 

![Grafana 대시보드](media/big-data-cluster-monitor-apps/grafana-dashboard-endpoint.png)


이 대시보드를 열면 애플리케이션에 대한 더 많은 정보를 얻고 추적을 유지할 수 있는  **호스트 앱 메트릭**으로 이동합니다.  

![호스트 앱 메트릭](media/big-data-cluster-monitor-apps/host-apps-metrics.png)


애플리케이션의 단일 Pod에 대한 자세한 정보를 보려면(경우에 따라 애플리케이션 복사본이 여러 개 있는 경우)  **호스트 Pod 메트릭**으로 이동하고 Pod를 선택하면 다음과 같은 메트릭 보기가 제공됩니다.  

![호스트 Pod 메트릭](media/big-data-cluster-monitor-apps/host-pods-metrics.png) 


## <a name="next-steps"></a>다음 단계

[앱 배포 샘플](https://aka.ms/sql-app-deploy)에서 추가 샘플을 확인할 수 있습니다.

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.