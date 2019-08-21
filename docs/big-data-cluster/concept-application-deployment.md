---
title: 애플리케이션 배포란?
titleSuffix: Big Data Clusters for SQL Server 2019
description: 이 문서에서는 SQL Server 2019에 대 한 빅 데이터 클러스터의 응용 프로그램 배포에 대해 설명 합니다.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: da497f8d7c435a807ba530ae619ff91a6f2dff71
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653005"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>SQL Server 2019 빅 데이터 클러스터의 애플리케이션 배포란?

애플리케이션 배포는 애플리케이션을 만들고 관리 및 실행하기 위한 인터페이스를 제공하여 빅 데이터 클러스터에 애플리케이션을 배포할 수 있게 합니다. 빅 데이터 클러스터에 배포된 애플리케이션은 클러스터의 계산 능력을 활용하며, 클러스터에서 사용할 수 있는 데이터에 액세스할 수 있습니다. 이로 인해 데이터가 있는 애플리케이션을 관리하는 동시에 애플리케이션의 확장성과 성능이 향상됩니다.
다음 섹션에서는 애플리케이션 배포의 아키텍처 및 기능을 설명합니다.

## <a name="application-deployment-architecture"></a>애플리케이션 배포 아키텍처

애플리케이션 배포는 컨트롤러 및 앱 런타임 처리기로 구성됩니다. 애플리케이션을 만들면 사양 파일(`spec.yaml`)이 제공됩니다. `spec.yaml` 파일에는 애플리케이션을 성공적으로 배포하기 위해 컨트롤러에서 알아야 하는 모든 사항이 포함되어 있습니다. 다음은 `spec.yaml`의 내용 샘플입니다.

```yaml
#spec.yaml
name: add-app #name of your python script
version: v1  #version of the app
runtime: Python #the language this app uses (R or Python)
src: ./add.py #full path to the location of the app
entrypoint: add #the function that will be called upon execution
replicas: 1  #number of replicas needed
poolsize: 1  #the pool size that you need your app to scale
inputs:  #input parameters that the app expects and the type
  x: int
  y: int
output: #output parameter the app expects and the type
  result: int
```

컨트롤러가 `spec.yaml` 파일에 지정된 `runtime`을 검사하고 해당 런타임 처리기를 호출합니다. 런타임 처리기가 애플리케이션을 만듭니다. 먼저, 각각 배포할 애플리케이션을 포함하는 Pod가 하나 이상 포함된 Kubernetes ReplicaSet가 생성됩니다. Pod 수는 애플리케이션의 `spec.yaml` 파일에 설정된 `replicas` 매개 변수를 통해 정의됩니다. 각 Pod는 하나 이상의 풀을 포함할 수 있습니다. 풀 수는 `spec.yaml` 파일에 설정된 `poolsize` 매개 변수를 통해 정의됩니다.

이러한 설정은 배포에서 병렬로 처리할 수 있는 요청량에 영향을 줍니다. 지정된 한 시점의 최대 요청 수는 `replicas`에 `poolsize`를 곱한 값과 같습니다. 복제본 5개와 복제본당 풀 2개가 있다면 배포에서 요청 10개를 병렬로 처리할 수 있습니다. `replicas` 및 `poolsize`의 그래픽 표현은 아래 그림을 참조하세요.

![poolsize 및 replicas](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

ReplicaSet가 생성되고 Pod가 시작된 후에는 `spec.yaml` 파일에 `schedule`이 설정된 경우 cron 작업이 생성됩니다. 마지막으로, 애플리케이션을 관리하고 실행하는 데 사용할 수 있는 Kubernetes 서비스가 생성됩니다(아래 참조).

애플리케이션을 실행하면 애플리케이션의 Kubernetes 서비스가 요청을 복제본으로 프록시하고 결과를 반환합니다.

## <a name="how-to-work-with-application-deployment"></a>애플리케이션 배포를 사용하는 방법

애플리케이션 배포의 두 가지 주요 인터페이스는 다음과 같습니다. 
- [명령줄 인터페이스 `azdata`](big-data-cluster-create-apps.md)
- [Visual Studio Code 및 Azure Data Studio 확장](app-deployment-extension.md)

RESTful 웹 서비스를 사용하여 애플리케이션을 실행할 수도 있습니다. 자세한 내용은 [빅 데이터 클러스터에서 애플리케이션 사용](big-data-cluster-consume-apps.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]응용 프로그램을 만들고 실행 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

- [azdata를 사용하여 애플리케이션 배포](big-data-cluster-create-apps.md)
- [앱 배포 확장을 사용하여 애플리케이션 배포](app-deployment-extension.md)
- [빅 데이터 클러스터에서 애플리케이션 사용](big-data-cluster-consume-apps.md)

에 대해 자세히 알아보려면 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]다음 개요를 참조 하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]무엇 인가요?](big-data-cluster-overview.md)
