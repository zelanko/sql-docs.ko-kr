---
title: 응용 프로그램 배포 란?
titleSuffix: SQL Server 2019 big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)의 응용 프로그램 배포에 대해 설명 합니다.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d8cc44862af21c54bdbd0e4adbb35db912c3f7c9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419412"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>SQL Server 2019 빅 데이터 클러스터에 응용 프로그램을 배포 하는 것은 무엇 인가요?

응용 프로그램을 배포 하면 응용 프로그램을 만들고, 관리 하 고, 실행할 수 있는 인터페이스를 제공 하 여 빅 데이터 클러스터에 응용 프로그램을 배포할 수 있습니다. 빅 데이터 클러스터에 배포 된 응용 프로그램은 클러스터의 계산 능력을 활용 하 고 클러스터에서 사용할 수 있는 데이터에 액세스할 수 있습니다. 이렇게 하면 데이터가 있는 응용 프로그램을 관리 하면서 응용 프로그램의 확장성과 성능이 향상 됩니다.
다음 섹션에서는 응용 프로그램 배포의 아키텍처 및 기능에 대해 설명 합니다.

## <a name="application-deployment-architecture"></a>응용 프로그램 배포 아키텍처

응용 프로그램 배포는 컨트롤러 및 앱 런타임 처리기로 구성 됩니다. 응용 프로그램을 만들 때 사양 파일 (`spec.yaml`)이 제공 됩니다. 이 `spec.yaml` 파일에는 응용 프로그램을 성공적으로 배포 하기 위해 컨트롤러에서 알아야 하는 모든 항목이 포함 되어 있습니다. 다음은에 대 한 `spec.yaml`콘텐츠의 샘플입니다.

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

컨트롤러는 `spec.yaml` 파일에서 `runtime` 지정 된를 검사 하 고 해당 하는 런타임 처리기를 호출 합니다. 런타임 처리기에서 응용 프로그램을 만듭니다. 먼저 배포 될 응용 프로그램을 포함 하는 하나 이상의 pod를 포함 하는 Kubernetes ReplicaSet가 만들어집니다. Pod의 수는 응용 프로그램의 `replicas` `spec.yaml` 파일에 설정 된 매개 변수를 통해 정의 됩니다. 각 pod는 풀을 하나 이상 포함할 수 있습니다. 풀 수는 `poolsize` `spec.yaml` 파일에 설정 된 매개 변수를 통해 정의 됩니다.

이러한 설정은 배포가 병렬로 처리할 수 있는 요청 양에 영향을 줍니다. 지정 된 시간에 대 한 최대 요청 수는 `replicas` 시간과 `poolsize`같습니다. 복제본 당 5 개의 복제본과 2 개의 풀이 있으면 배포에서 10 개의 요청을 병렬로 처리할 수 있습니다. `replicas` 및`poolsize`의 그래픽 표현은 아래 이미지를 참조 하세요.

![Poolsize 및 복제본](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

ReplicaSet을 만들고 pod를 시작 하면 `schedule` `spec.yaml` 파일에가 설정 된 경우 cron 작업이 생성 됩니다. 마지막으로 응용 프로그램을 관리 하 고 실행 하는 데 사용할 수 있는 Kubernetes 서비스가 생성 됩니다 (아래 참조).

응용 프로그램이 실행 되 면 응용 프로그램에 대 한 Kubernetes 서비스에서 복제본에 대 한 요청을 프록시 하 고 결과를 반환 합니다.

## <a name="how-to-work-with-application-deployment"></a>응용 프로그램 배포를 사용 하는 방법

응용 프로그램 배포에 대 한 두 가지 주요 인터페이스는 다음과 같습니다. 
- [명령줄 인터페이스`azdata`](big-data-cluster-create-apps.md)
- [Visual Studio Code 및 Azure Data Studio 확장](app-deployment-extension.md)

RESTful 웹 서비스를 사용 하 여 응용 프로그램을 실행할 수도 있습니다. 자세한 내용은 [빅 데이터 클러스터에서 응용 프로그램 사용](big-data-cluster-consume-apps.md)을 참조 하세요.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에서 응용 프로그램을 만들고 실행 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

- [Azdata를 사용 하 여 응용 프로그램 배포](big-data-cluster-create-apps.md)
- [앱 배포 확장을 사용 하 여 응용 프로그램 배포](app-deployment-extension.md)
- [빅 데이터 클러스터에서 응용 프로그램 사용](big-data-cluster-consume-apps.md)

SQL Server 빅 데이터 클러스터에 대해 자세히 알아보려면 다음 개요를 참조 하세요.

- [SQL Server 2019 빅 데이터 클러스터는 무엇 인가요?](big-data-cluster-overview.md)
