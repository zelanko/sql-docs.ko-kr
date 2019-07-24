---
title: 빅 데이터 클러스터 란?
titleSuffix: SQL Server big data clusters
description: Kubernetes에서 실행 되는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대해 알아보고 관계형 및 HDFS 데이터 모두에 대 한 확장 옵션을 제공 합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0beb4ea57ba6c2591e5b2c06a7775fc2d7e8b26c
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419500"
---
# <a name="what-are-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터란 무엇인가요?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

부터 빅 데이터 클러스터 SQL Server 를사용하여Kubernetes에서실행되는SQLServer,Spark및HDFS컨테이너의확장가능한클러스터를배포할수있습니다.[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 이러한 구성 요소는 side-by-side로 실행 되므로 Transact-sql 또는 Spark에서 빅 데이터를 읽고 쓰고 처리할 수 있으므로 대용량의 빅 데이터를 사용 하 여 상위 값의 관계형 데이터를 쉽게 결합 하 고 분석할 수 있습니다.

최신 릴리스에 대 한 새로운 기능 및 알려진 문제에 대 한 자세한 내용은 [릴리스 정보](release-notes-big-data-cluster.md)를 참조 하세요.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>시나리오

빅 데이터 클러스터 SQL Server 빅 데이터와 상호 작용 하는 방법에 유연성을 제공 합니다. 외부 데이터 원본을 쿼리하거나, SQL Server에서 관리 하는 HDFS에 빅 데이터를 저장 하거나, 클러스터를 통해 여러 외부 데이터 원본의 데이터를 쿼리할 수 있습니다. 그런 다음 AI, machine learning 및 기타 분석 작업에 대 한 데이터를 사용할 수 있습니다. 다음 섹션에서는 이러한 시나리오에 대 한 자세한 정보를 제공 합니다.

### <a name="data-virtualization"></a>데이터 가상화

[SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md)를 활용 하 여 빅 데이터 클러스터 SQL Server 데이터를 이동 하거나 복사 하지 않고도 외부 데이터 원본을 쿼리할 수 있습니다. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]데이터 원본에 대 한 새 커넥터를 소개 합니다.

![데이터 가상화](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data lake

SQL Server 빅 데이터 클러스터에는 확장 가능한 HDFS *저장소 풀이*포함 되어 있습니다. 이를 사용 하 여 큰 데이터를 저장 하 고, 잠재적으로 여러 외부 원본에서 수집 수 있습니다. 빅 데이터를 빅 데이터 클러스터의 HDFS에 저장 한 후에는 데이터를 분석 하 고 쿼리하고 관계형 데이터와 결합할 수 있습니다.

![Data lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>데이터 마트 확장

빅 데이터 클러스터 SQL Server 확장 계산 및 저장소를 제공 하 여 데이터 분석 성능을 향상 시킵니다. 추가 분석을 위해 다양 한 원본에서 데이터를 수집 하 고 *데이터 풀* 노드에 캐시로 배포할 수 있습니다.

![데이터 마트](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>통합 AI 및 Machine Learning

빅 데이터 클러스터 SQL Server는 HDFS 저장소 풀 및 데이터 풀에 저장 된 데이터에 대 한 AI 및 기계 학습 작업을 가능 하 게 합니다. R, Python, Scala 또는 Java를 사용 하 여 SQL Server의 기본 제공 AI 도구 뿐만 아니라 Spark도 사용할 수 있습니다.

![AI 및 ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>관리 및 모니터링

관리 및 모니터링은 명령줄 도구, Api, 포털 및 동적 관리 뷰를 조합 하 여 제공 됩니다.

Azure Data Studio를 사용 하 여 빅 데이터 클러스터에서 다양 한 작업을 수행할 수 있습니다. 새 **SQL Server 2019 확장 (미리 보기)** 에서 사용할 수 있습니다. 이 확장은 다음을 제공 합니다.

- 일반적인 관리 작업을 위한 기본 제공 코드 조각입니다.
- HDFS를 찾아보고, 파일을 업로드 하 고, 파일을 미리 보고, 디렉터리를 만들 수 있습니다.
- Jupyter 호환 노트북을 만들고 열고 실행 하는 기능.
- 데이터 가상화 마법사를 통해 외부 데이터 원본 만들기를 간소화할 수 있습니다.

## <a id="architecture"></a>마이크로아키텍처

SQL Server 빅 데이터 클러스터는 [Kubernetes](https://kubernetes.io/docs/concepts/)오케스트레이션 Linux 컨테이너의 클러스터입니다.

### <a name="kubernetes-concepts"></a>Kubernetes 개념

Kubernetes는 컨테이너 배포를 필요에 따라 확장할 수 있는 오픈 소스 컨테이너 오 케 스트레이 터입니다. 다음 표에서는 몇 가지 중요 한 Kubernetes 용어를 정의 합니다.

|||
|:--|:--|
| **Cluster** | Kubernetes 클러스터는 노드 라는 컴퓨터 집합입니다. 한 노드는 클러스터를 제어 하 고 마스터 노드로 지정 됩니다. 나머지 노드는 작업자 노드입니다. Kubernetes 마스터는 작업자 간에 작업을 배포 하 고 클러스터의 상태를 모니터링 하는 일을 담당 합니다. |
| **Node** | 노드는 컨테이너 화 된 응용 프로그램을 실행 합니다. 물리적 컴퓨터 또는 가상 컴퓨터 일 수 있습니다. Kubernetes 클러스터는 물리적 컴퓨터와 가상 컴퓨터 노드를 혼합 하 여 포함할 수 있습니다. |
| **Pod** | Pod는 Kubernetes의 원자성 배포 단위입니다. Pod는 응용 프로그램을 실행 하는 데 필요한 하나 이상의 컨테이너 및 연결 된 리소스의 논리적 그룹입니다. 각 pod는 노드에서 실행 됩니다. 노드는 하나 이상의 pod을 실행할 수 있습니다. Kubernetes 마스터는 클러스터의 노드에 pod을 자동으로 할당 합니다. |
| &nbsp; ||

빅 데이터 클러스터 SQL Server Kubernetes는 빅 데이터 클러스터 SQL Server의 상태를 담당 합니다. Kubernetes는 클러스터 노드를 작성 및 구성 하 고, pod를 노드에 할당 하 고, 클러스터의 상태를 모니터링 합니다.

### <a name="big-data-clusters-architecture"></a>빅 데이터 클러스터 아키텍처

다음 다이어그램에서는 SQL Server에 대 한 빅 데이터 클러스터의 구성 요소를 보여 줍니다.

![아키텍처 개요](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a>Controller

컨트롤러는 클러스터에 대 한 관리 및 보안을 제공 합니다. Cntrol 서비스, 구성 저장소 및 기타 클러스터 수준 서비스 (예: Kibana, Grafana, 탄력적 검색)를 포함 합니다.

### <a id="computeplane"></a>Compute 풀

Compute 풀은 클러스터에 계산 리소스를 제공 합니다. SQL Server on Linux pod를 실행 하는 노드가 포함 됩니다. Compute 풀의 pod은 특정 처리 작업을 위해 *SQL 계산 인스턴스로* 나뉩니다. 

### <a id="dataplane"></a>데이터 풀

데이터 풀은 데이터 지 속성 및 캐싱에 사용 됩니다. 데이터 풀은 SQL Server on Linux를 실행 하는 하나 이상의 pod으로 구성 됩니다. SQL 쿼리 또는 Spark 작업에서 데이터를 수집 하는 데 사용 됩니다. SQL Server 빅 데이터 클러스터 데이터 마트는 데이터 풀에 유지 됩니다. 

### <a name="storage-pool"></a>스토리지 풀

저장소 풀은 SQL Server on Linux, Spark 및 HDFS로 구성 된 저장소 풀 pod 구성 됩니다. SQL Server 빅 데이터 클러스터의 모든 저장소 노드는 HDFS 클러스터의 멤버입니다.

> [!TIP]
> 빅 데이터 클러스터 아키텍처 및 설치에 대 한 자세한 내용은 [워크숍: 빅 데이터 클러스터 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)를 Microsoft SQL Server 합니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터는 SQL Server 2019 초기 도입 프로그램을 통해 제한 된 공개 미리 보기로 제공 됩니다. 액세스를 요청 하려면 [여기](https://aka.ms/eapsignup)에 등록 하 고 빅 데이터 클러스터를 시도 하는 관심을 지정 합니다. Microsoft는 모든 요청을 심사 하 고 가능한 한 빨리 응답 합니다.
