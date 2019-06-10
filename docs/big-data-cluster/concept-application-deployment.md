---
title: 응용 프로그램 배포는 무엇입니까?
titleSuffix: SQL Server 2019 big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 응용 프로그램 배포를 설명 합니다.
author: jterh
ms.author: jroth
manager: jroth
ms.date: 03/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1a6ba9caed2b01abc50e16e34d1a13413af2d0ba
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801860"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>SQL Server 2019 빅 데이터 클러스터에 응용 프로그램 배포 란?

만들기, 관리 및 응용 프로그램을 실행 하는 인터페이스를 제공 하 여 빅 데이터 클러스터에 응용 프로그램 배포를 사용 하는 응용 프로그램 배포. 빅 데이터 클러스터에 배포 된 응용 프로그램 클러스터의 계산 능력의 혜택 및 클러스터에서 사용할 수 있는 데이터에 액세스할 수 있습니다. 확장성 및 데이터를 거주 응용 프로그램을 관리 하는 동안 응용 프로그램의 성능을 향상 됩니다.
다음 섹션의 아키텍처 및 응용 프로그램 배포 기능을 설명 합니다.

## <a name="application-deployment-architecture"></a>응용 프로그램 배포 아키텍처

응용 프로그램 배포는 컨트롤러 및 앱 런타임 처리기 구성 됩니다. 사양 파일을 응용 프로그램을 만들 때 (`spec.yaml`) 제공 됩니다. 이 `spec.yaml` 컨트롤러를 성공적으로 응용 프로그램을 배포 하려면 알아야 할 모든 파일 포함 합니다. 다음은 샘플에 대 한 내용의 `spec.yaml`:

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

컨트롤러 검사는 `runtime` 에 지정 된 된 `spec.yaml` 파일 및 해당 런타임 처리기를 호출 합니다. 런타임 처리기는 응용 프로그램을 만듭니다. 먼저 Kubernetes ReplicaSet 하나 이상의 pod를 배포할 응용 프로그램을 포함 하는 각 포함 된 만들어집니다. Pod의 수를 정의한를 `replicas` 매개 변수에서 설정 된 `spec.yaml` 응용 프로그램에 대 한 파일입니다. 각 pod 하나 이상의 풀이 있습니다. 풀의 개수는 정의한 합니다 `poolsize` 매개 변수에서 설정는 `spec.yaml` 파일.

이러한 설정을 배포 병렬로 처리할 수 있는 요청 양을 영향을 줍니다. 특정된 한 번에 요청의 최대 수는과 동일한 `replicas` 번 `poolsize`합니다. 5 개의 복제본 및 복제본 당 2 개의 풀에 있는 경우 배포에 10 개의 요청을 병렬로 처리할 수 있습니다. 그래픽 표현 아래 이미지를 참조 하세요 `replicas` 고 `poolsize`:

![Poolsize 및 복제본](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

ReplicaSet 만들어진 후 pod 시작한는 cron 작업이 생성 됩니다는 `schedule` 에서 설정한는 `spec.yaml` 파일입니다. Kubernetes 서비스를 마지막으로 만들 관리 하 고 (아래 참조) 응용 프로그램을 실행할 수 있습니다.

응용 프로그램을 실행 하는 경우, Kubernetes 서비스 응용 프로그램 프록시의 요청을 복제 하 고 결과 반환 합니다.

## <a name="how-to-work-with-application-deployment"></a>응용 프로그램 배포를 사용 하는 방법

응용 프로그램 배포에 대 한 두 가지 주요 인터페이스는 다음과 같습니다. 
- [명령줄 인터페이스 `mssqlctl`](big-data-cluster-create-apps.md)
- [Visual Studio Code 및 Azure Data Studio 확장](app-deployment-extension.md)

RESTful 웹 서비스를 사용 하 여 실행 될 응용 프로그램에 대 한 가능한 이기도 합니다. 자세한 내용은 [빅 데이터 클러스터에 응용 프로그램을 사용](big-data-cluster-consume-apps.md)합니다.

## <a name="next-steps"></a>다음 단계

만들기 및 SQL Server 빅 데이터 클러스터에 응용 프로그램을 실행 하는 방법에 대 한 자세한 내용은 다음을 참조 합니다.

- [mssqlctl를 사용하여 애플리케이션 배포](big-data-cluster-create-apps.md)
- [앱 배포 확장을 사용 하 여 응용 프로그램 배포](app-deployment-extension.md)
- [빅 데이터 클러스터에 응용 프로그램 사용](big-data-cluster-consume-apps.md)

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 다음 개요를 참조 하세요.

- [SQL Server 2019 빅 데이터 클러스터는 무엇 인가요?](big-data-cluster-overview.md)
