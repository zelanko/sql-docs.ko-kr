---
title: 애플리케이션 배포란?
titleSuffix: SQL Server Big Data Clusters
description: 애플리케이션 배포가 SQL Server 2019 빅 데이터 클러스터에서 애플리케이션을 만들고, 관리하고, 실행하는 인터페이스를 제공하는 방법을 알아봅니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 65a7c0afc57cc29d8ec5df7beb4c3107470e2d31
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257263"
---
# <a name="what-is-application-deployment-on-a-big-data-cluster"></a>빅 데이터 클러스터의 애플리케이션 배포란?

애플리케이션 배포는 애플리케이션을 만들고 관리 및 실행하기 위한 인터페이스를 제공하여 빅 데이터 클러스터에 애플리케이션을 배포할 수 있게 합니다. 빅 데이터 클러스터에 배포된 애플리케이션은 클러스터의 계산 능력을 활용하며, 클러스터에서 사용할 수 있는 데이터에 액세스할 수 있습니다. 이로 인해 데이터가 있는 애플리케이션을 관리하는 동시에 애플리케이션의 확장성과 성능이 향상됩니다. SQL Server 빅 데이터 클러스터에서 지원되는 애플리케이션 런타임은 R, Python, SSIS, MLeap입니다.

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

## <a name="security-considerations-for-applications-deployments-on-openshift"></a><a id="app-deploy-security"></a> OpenShift의 애플리케이션 배포에 대한 보안 고려 사항

SQL Server 2019 CU5는 Red Hat OpenShift의 빅 데이터 클러스터 배포뿐만 아니라 BDC의 업데이트된 보안 모델도 지원하므로, 권한 있는 컨테이너가 더 이상 필요하지 않습니다. 권한 없는 컨테이너 외에도, 컨테이너는 SQL Server 2019 CU5를 사용하는 모든 신규 배포에 대해 기본적으로 루트가 아닌 사용자로 실행됩니다.

CU5 릴리스 시점에 [앱 배포]() 인터페이스를 사용하여 배포되는 애플리케이션의 설치 단계는 여전히 ‘루트’ 사용자로 실행됩니다. 이 동작은 설치 도중에 애플리케이션에서 사용할 추가 패키지가 설치되기 때문에 필요합니다. 애플리케이션의 일부로 배포된 다른 사용자 코드는 권한이 낮은 사용자로 실행됩니다. 

또한 **CAP_AUDIT_WRITE** 기능은 cron 작업을 사용하여 SSIS 애플리케이션 예약을 허용하는 데 필요한 선택적 기능입니다. 애플리케이션의 yaml 사양 파일에서 일정을 지정하는 경우 애플리케이션은 추가 기능을 필요로 하는 cron 작업을 통해 트리거됩니다.  또는 *azdata app run*을 사용하여 웹 서비스 호출을 통해 요청 시 애플리케이션을 트리거할 수 있으며, 여기에는 CAP_AUDIT_WRITE 기능이 필요하지 않습니다. 

> [!NOTE]
> [OpenShift 배포 문서](deploy-openshift.md)의 사용자 지정 SCC는 빅 데이터 클러스터의 기본 배포에 필요하지 않기 때문에 이 기능을 포함하지 않습니다. 이 기능을 사용하도록 설정하려면 먼저 사용자 지정 SCC yaml 파일을 업데이트하여 다음 위치에 CAP_AUDIT_WRITE를 포함해야 합니다. 

```yml
...
allowedCapabilities:
- SETUID
- SETGID
- CHOWN
- SYS_PTRACE
- AUDIT_WRITE
...
```

## <a name="how-to-work-with-application-deployment"></a>애플리케이션 배포를 사용하는 방법

애플리케이션 배포의 두 가지 주요 인터페이스는 다음과 같습니다. 
- [명령줄 인터페이스 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](app-create.md)
- [Visual Studio Code 및 Azure Data Studio 확장](app-deployment-extension.md)

RESTful 웹 서비스를 사용하여 애플리케이션을 실행할 수도 있습니다. 자세한 내용은 [빅 데이터 클러스터에서 애플리케이션 사용](app-consume.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에서 애플리케이션을 만들고 실행하는 방법에 대한 자세한 내용은 다음을 참조하세요.

- [azdata를 사용하여 애플리케이션 배포](app-create.md)
- [앱 배포 확장을 사용하여 애플리케이션 배포](app-deployment-extension.md)
- [빅 데이터 클러스터에서 애플리케이션 사용](app-consume.md)

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 개요를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)