---
title: 빅 데이터 클러스터는 무엇 인가요?
titleSuffix: SQL Server big data clusters
description: Kubernetes에서 실행 하 고 관계형 둘 다에 대 한 확장 옵션 및 HDFS 데이터를 제공 하는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대해 알아봅니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/07/2018
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: fed82f9bda8f72d92157de726eb6ae3c6ed1c0c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801884"
---
# <a name="what-are-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터란 무엇인가요?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

부터 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)], SQL Server 빅 데이터 클러스터를 사용 하면 Kubernetes에서 실행 되는 SQL Server, Spark 및 HDFS 컨테이너의 확장 가능한 클러스터를 배포 합니다. 이러한 구성 요소는 읽기, 쓰기, 및 TRANSACT-SQL 또는 Spark의 빅 데이터 처리, 결합 및 대규모 빅 데이터를 사용 하 여 높은 가치의 관계형 데이터에 분석 있게 할 수 있도록 나란히 실행 됩니다.

새로운 기능 및 최신 릴리스의 알려진된 문제에 대 한 자세한 내용은 참조는 [릴리스](release-notes-big-data-cluster.md)합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>시나리오

SQL Server 빅 데이터 클러스터 빅 데이터와 상호 작용 하는 방법에 유연성을 제공 합니다. 외부 데이터 원본을 쿼리, 관리 SQL 서버 또는 클러스터를 통해 여러 외부 데이터 원본에서 데이터를 쿼리 하는 HDFS의 빅 데이터를 저장할 수 있습니다. 그런 다음 인공 지능, 기계 학습, 및 기타 분석 작업에 대 한 데이터를 사용할 수 있습니다. 다음 섹션에서는 이러한 시나리오에 대 한 자세한 정보를 제공합니다.

### <a name="data-virtualization"></a>데이터 가상화

활용 하 여 [SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md), SQL Server 빅 데이터 클러스터 이동 하거나 데이터를 복사 하지 않고 외부 데이터 원본을 쿼리할 수 있습니다. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 데이터 원본에 새 커넥터를 소개합니다.

![데이터 가상화](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>데이터 레이크

SQL Server 빅 데이터 클러스터를 확장 가능한 HDFS 포함 *저장소 풀*합니다. 이 잠재적으로 여러 외부 소스에서 수집 하는 빅 데이터를 저장할 수 있습니다. 빅 데이터는 빅 데이터 클러스터의 HDFS에 저장 되 면 분석 하 고 및 데이터를 쿼리 하 고, 관계형 데이터와 결합할 수 있습니다.

![데이터 레이크](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>수평 확장 데이터 마트

SQL Server 빅 데이터 클러스터 스케일 아웃 계산 및 데이터 분석의 성능 향상을 위해 저장소를 제공 합니다. 다양 한 원본에서에서 데이터를 수집 하 고 분산 될 수 있습니다 *데이터 풀* 추가 분석을 위해 캐시 노드.

![데이터 마트](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>통합된 AI 및 기계 학습

SQL Server 빅 데이터 클러스터에 AI 및 기계 학습 작업에 HDFS 저장소 풀 및 데이터 풀에 저장 된 데이터를 사용 합니다. SQL server에서 R, Python, Scala 또는 Java를 사용 하 여 Spark 뿐만 아니라 기본 제공 AI 도구를 사용할 수 있습니다.

![AI 및 기계 학습](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>관리 및 모니터링

관리 및 모니터링은 명령줄 도구, Api, 관리자 포털을 및 동적 관리 보기의 조합을 통해 제공 됩니다.

합니다 [클러스터 관리자 포털](cluster-admin-portal.md) 클러스터의 pod의 상태를 표시 하는 웹 인터페이스입니다. 또한 log analytics 및 대시보드 모니터링을 다른 대시보드에 대 한 링크를 제공 합니다.

Azure 데이터 Studio를 사용 하 여 빅 데이터 클러스터에서 다양 한 작업을 수행할 수 있습니다. 새 활성화 됩니다 **SQL Server 2019 확장 (미리 보기)** 합니다. 이 확장을 제공합니다.

- 일반적인 관리 작업에 대 한 기본 제공 조각입니다.
- HDFS 찾아보기, 파일 업로드, 파일, 미리 보기 및 디렉터리를 만들 수 있습니다.
- 열기 및 실행-호환 되는 Jupyter notebook을 만들 수 있습니다.
- 데이터 가상화 마법사 외부 데이터 원본 만들기를 간소화할 수 있습니다.

## <a id="architecture"></a> 아키텍처

SQL Server 빅 데이터 클러스터는 클러스터의 Linux 컨테이너에 의해 오케스트레이션 됨 [Kubernetes](https://kubernetes.io/docs/concepts/)합니다.

### <a name="kubernetes-concepts"></a>Kubernetes 개념

Kubernetes는 오픈 소스 컨테이너 오 케 스트레이 터를 필요에 따라 컨테이너 배포를 확장할 수 있는 경우 다음 표에서 몇 가지 중요 한 Kubernetes 용어를 정의합니다.

|||
|:--|:--|
| **Cluster** | Kubernetes 클러스터는 노드 라는 컴퓨터 집합입니다. 하나의 노드 클러스터를 제어 하 고 지정 된 마스터 노드 나머지 노드는 작업자 노드입니다. Kubernetes 마스터는 작업자 간 작업 분산 및 클러스터의 상태를 모니터링 합니다. |
| **Node** | 노드는 컨테이너 화 된 응용 프로그램을 실행 합니다. 물리적 컴퓨터 또는 가상 컴퓨터 수 있습니다. Kubernetes 클러스터는 혼합 물리적 컴퓨터와 가상 컴퓨터 노드를 포함할 수 있습니다. |
| **Pod** | Pod는 Kubernetes의 원자성 배포 단위입니다. Pod는 하나 이상의 컨테이너의 논리적 그룹-및 관련 응용 프로그램을 실행 하려면 리소스가 필요 합니다. 각 pod; 노드에서 실행 됩니다. 노드는 하나 이상의 pod를 실행할 수 있습니다. Kubernetes 마스터를 클러스터의 노드에 pod를 자동으로 할당합니다. |
| &nbsp; ||

SQL Server 빅 데이터 클러스터에 Kubernetes는 SQL Server 빅 데이터 클러스터;의 상태 Kubernetes 빌드 및 클러스터 노드를 구성 노드에 pod를 할당 하 고 클러스터의 상태를 모니터링 합니다.

### <a name="big-data-clusters-architecture"></a>빅 데이터 클러스터 아키텍처

클러스터의 노드는 세 개의 논리 평면으로 정렬 됩니다: 제어 평면, 계산 평면 및 데이터 평면입니다. 각 평면은 클러스터의 다른 책임이 있습니다. SQL Server 빅 데이터 클러스터의 모든 Kubernetes 노드는 구성 요소에 대 한 하나 이상의 평면의 pod 호스팅입니다.

![아키텍처 개요](media/big-data-cluster-overview/architecture-diagram-planes.png)

### <a id="controlplane"></a> 제어 평면

제어 평면 관리 및 클러스터에 대 한 보안을 제공합니다. Kubernetes 마스터를 포함 하는 *SQL Server 마스터 인스턴스*, 및 Hive Metastore와 Spark 드라이버와 같은 다른 클러스터 수준 서비스입니다.

### <a id="computeplane"></a> 평면 계산

계산 평면 클러스터에 계산 리소스를 제공합니다. SQL Server Linux pod를 실행 하는 노드를 포함 합니다. 계산 영역에서 pod 나뉩니다 *풀 계산* 특정 태스크를 처리 합니다. 계산 풀 역할을 할 수는 [PolyBase](../relational-databases/polybase/polybase-guide.md) HDFS, Oracle, MongoDB, 또는 Teradata 원본 등 다양 한 데이터에 대해 분산된 쿼리를 위한 스케일 아웃 그룹입니다.

### <a id="dataplane"></a> 데이터 평면

데이터 평면 데이터 지 속성 및 캐싱에 사용 됩니다. SQL 데이터 풀 및 저장소 풀을 포함합니다.  SQL 데이터 풀에서 Linux SQL Server를 실행 하는 하나 이상의 pod 이루어져 있습니다. SQL 쿼리 또는 Spark 작업에서 데이터를 수집 하는 것이 됩니다. SQL Server 빅 데이터 클러스터 데이터 마트의 데이터 풀에 유지 됩니다. 저장소 풀의 SQL Server Linux, Spark 및 HDFS로 구성 된 저장소 풀 pod 이루어져 있습니다. SQL Server 빅 데이터 클러스터의 모든 저장소 노드에 HDFS 클러스터의 멤버입니다.

> [!TIP]
> 빅 데이터 클러스터 아키텍처 및 설치에는 대 한 심층적인 기사를 참조 하세요. [워크숍: Microsoft SQL Server 빅 데이터 클러스터 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)합니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터는 먼저 SQL Server 2019 Early Adoption Program을 통해 제한 된 공개 미리 보기로 제공 됩니다. 액세스를 요청 하려면 등록 [여기](https://aka.ms/eapsignup), 빅 데이터 클러스터를 시도 하려면 관심을 가져를 지정 합니다. Microsoft는 모든 요청을 심사 하 고 가능한 한 빨리 응답 합니다.
