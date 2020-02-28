---
title: 빅 데이터 클러스터란?
titleSuffix: SQL Server Big Data Clusters
description: Kubernetes에서 실행되고 관계형 및 HDFS 데이터 둘 다에 대해 스케일 아웃 옵션을 제공하는 SQL Server 2019 빅 데이터 클러스터에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c751992e666151752783e9813efa2f696fcdcb6e
ms.sourcegitcommit: 9bdecafd1aefd388137ff27dfef532a8cb0980be
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2020
ms.locfileid: "77173643"
---
# <a name="what-are-big-data-clusters-2019"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]란 무엇인가요?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]부터 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 사용하면 Kubernetes에서 실행되는 SQL Server, Spark 및 HDFS 컨테이너의 확장 가능한 클러스터를 배포할 수 있습니다. 이러한 구성 요소는 동시에 실행되므로 Transact-SQL 또는 Spark에서 빅 데이터 읽기, 쓰기 및 처리할 수 있으며, 대용량의 빅 데이터를 사용하여 가치 높은 관계형 데이터를 쉽게 조합하고 분석할 수 있습니다.

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]부터 SQL Server 빅 데이터 클러스터가 도입되었습니다.

SQL Server 빅 데이터 클러스터는 다음과 같은 용도로 사용할 수 있습니다.

- Kubernetes에서 실행되는 SQL Server, Spark 및 HDFS 컨테이너의 [확장성 있는 클러스터 배포](../big-data-cluster/deploy-get-started.md) 
- Transact-SQL 또는 Spark에서 빅 데이터 읽기, 쓰기 및 처리
- 대용량 빅 데이터를 사용하여 가치 높은 관계형 데이터를 쉽게 조합 및 분석
- 외부 데이터 원본 쿼리
- SQL Server에서 관리하는 HDFS에 빅 데이터 저장
- 클러스터를 통해 여러 외부 데이터 원본에서 데이터 쿼리
- AI, 기계 학습 및 기타 분석 작업에 데이터 사용
- [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]에서 [애플리케이션 배포 및 실행](../big-data-cluster/concept-application-deployment.md)
- [PolyBase](../relational-databases/polybase/polybase-guide.md)를 사용하여 데이터 가상화 외부 테이블을 사용하여 외부 SQL Server, Oracle, Teradata, MongoDB 및 ODBC 데이터 원본의 데이터 쿼리
- Always On 가용성 그룹 기술을 사용하여 SQL Server 마스터 인스턴스 및 모든 데이터베이스에 관해 고가용성 제공

최신 릴리스의 새로운 기능 및 알려진 문제에 대한 자세한 내용은 [릴리스 정보](release-notes-big-data-cluster.md)를 참조하세요.

## <a name="scenarios"></a>시나리오

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]는 빅 데이터와 상호 작용하는 유연한 방법을 제공합니다. 외부 데이터 원본을 쿼리하거나, SQL Server에서 관리하는 HDFS에 빅 데이터를 저장하거나, 클러스터를 통해 여러 외부 데이터 원본에서 데이터를 쿼리할 수 있습니다. 그런 후 AI, Machine Learning 및 기타 분석 작업에 데이터를 사용할 수 있습니다. 다음 섹션에서는 이러한 시나리오에 대해 자세히 설명합니다.

### <a name="data-virtualization"></a>데이터 가상화

[SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md)를 활용하므로 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]는 데이터를 이동하거나 복사하지 않고도 외부 데이터 원본을 쿼리할 수 있습니다. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]에서는 데이터 원본에 대한 새 커넥터를 도입했습니다.

![데이터 가상화](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data Lake

SQL Server 빅 데이터 클러스터에는 확장 가능한 HDFS *스토리지 풀*이 포함되어 있습니다. 이를 사용하여 여러 외부 원본에서 수집될 수 있는 빅 데이터를 저장할 수 있습니다. 빅 데이터를 빅 데이터 클러스터의 HDFS에 저장한 후에는 데이터를 분석 및 쿼리하고 관계형 데이터와 결합할 수 있습니다.

![Data Lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>스케일 아웃 데이터 마트

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]는 스케일 아웃 컴퓨팅 및 스토리지를 제공하여 데이터 분석 성능을 향상시킵니다. 추가 분석을 위해 다양한 원본의 데이터를 수집하고 *데이터 풀* 노드 간에 캐시로 분산할 수 있습니다.

![데이터 마트](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>통합 AI 및 Machine Learning

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]는 HDFS 스토리지 풀 및 데이터 풀에 저장된 데이터에 대해 AI 및 Machine Learning 작업을 사용하도록 설정합니다. R, Python, Scala 또는 Java를 사용하여 SQL Server의 기본 제공 AI 도구 뿐만 아니라 Spark도 사용할 수 있습니다.

![AI 및 ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>관리 및 모니터링

관리 및 모니터링은 명령줄 도구, API, 포털 및 동적 관리 뷰를 조합하여 제공됩니다.

[Azure Data Studio](../azure-data-studio/what-is.md)를 사용하여 빅 데이터 클러스터에서 다양한 작업을 수행할 수 있습니다.
- 일반적인 관리 작업을 위한 기본 제공 코드 조각
- HDFS를 찾아보고, 파일을 업로드하고, 파일을 미리 보고, 디렉터리를 만드는 기능
- Jupyter 호환 Notebook을 만들고 열고 실행하는 기능
- 외부 데이터 원본 만들기를 간소화하기 위한 데이터 가상화 마법사(**데이터 가상화 확장**에 의해 사용하도록 설정됨).

## <a id="architecture"></a> 아키텍처

SQL Server 빅 데이터 클러스터는 [Kubernetes](https://kubernetes.io/docs/concepts/)에서 오케스트레이션되는 Linux 컨테이너의 클러스터입니다.

### <a name="kubernetes-concepts"></a>Kubernetes 개념

Kubernetes는 컨테이너 배포를 필요에 따라 확장할 수 있는 오픈 소스 컨테이너 오케스트레이터입니다. 다음 표에서는 몇 가지 중요한 Kubernetes 용어를 정의합니다.

|||
|:--|:--|
| **Cluster** | Kubernetes 클러스터는 노드라는 컴퓨터 세트입니다. 한 노드는 클러스터를 제어하고 마스터 노드로 지정됩니다. 나머지 노드는 작업자 노드입니다. Kubernetes 마스터는 작업자 간에 작업을 배포하고 클러스터의 상태를 모니터링하는 일을 담당합니다. |
| **Node** | 노드는 컨테이너화된 애플리케이션을 실행합니다. 물리적 컴퓨터 또는 가상 머신일 수 있습니다. Kubernetes 클러스터는 물리적 컴퓨터 및 가상 머신 노드를 혼합해서 포함할 수 있습니다. |
| **Pod** | Pod는 Kubernetes의 원자성 배포 단위입니다. Pod는 애플리케이션을 실행하는 데 필요한 하나 이상의 컨테이너 및 연결된 리소스의 논리적 그룹입니다. 각 pod는 하나의 노드에서 실행되고 하나의 노드는 하나 이상의 pod를 실행할 수 있습니다. Kubernetes 마스터는 클러스터의 노드에 pod을 자동으로 할당합니다. |
| &nbsp; ||

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에서 Kubernetes는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]의 상태를 담당합니다. Kubernetes는 클러스터 노드를 작성 및 구성하고, pod를 노드에 할당하고, 클러스터의 상태를 모니터링합니다.

### <a name="big-data-clusters-architecture"></a>빅 데이터 클러스터 아키텍처

다음 다이어그램에서는 SQL Server의 빅 데이터 클러스터 구성 요소를 보여 줍니다.

![아키텍처 개요](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a> 컨트롤러

컨트롤러는 클러스터에 대한 관리 및 보안을 제공합니다. 여기에는 컨트롤 서비스, 구성 저장소 및 기타 클러스터 수준 서비스(예: Kibana, Grafana, 탄력적 검색)가 포함됩니다.

### <a id="computeplane"></a> 컴퓨팅 풀

컴퓨팅 풀은 클러스터에 컴퓨팅 리소스를 제공합니다. 여기에는 SQL Server on Linux pod를 실행하는 노드가 포함됩니다. 컴퓨팅 풀의 pod는 특정 처리 작업을 위한 *SQL 컴퓨팅 인스턴스*로 나뉩니다. 

### <a id="dataplane"></a> 데이터 풀

데이터 풀은 데이터 지속성 및 캐싱에 사용됩니다. 데이터 풀은 Linux에서 SQL Server를 실행하는 하나 이상의 pod로 구성됩니다. SQL 쿼리 또는 Spark 작업에서 데이터를 수집하는 데 사용됩니다. SQL Server 빅 데이터 클러스터 데이터 마트는 데이터 풀에 유지됩니다. 

### <a name="storage-pool"></a>스토리지 풀

스토리지 풀은 Linux의 SQL Server, Spark 및 HDFS로 이루어진 스토리지 풀 pod로 구성됩니다. SQL Server 빅 데이터 클러스터의 모든 스토리지 노드는 HDFS 클러스터의 멤버입니다.

> [!TIP]
> 빅 데이터 클러스터 아키텍처 및 설치를 자세히 알아보려면 [워크숍: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters).

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터 배포에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터 시작](deploy-get-started.md)을 참조하세요.
