---
title: 스토리지 풀이란?
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터에서 SQL Server 스토리지 풀의 역할과 SQL 스토리지 풀의 아키텍처 및 기능에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4d810220e0bd1148d4f572638c3ac67d4c3b44c0
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257245"
---
# <a name="what-is-the-storage-pool-big-data-clusters-2019"></a>스토리지 풀이란([!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)])?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)](BDC)에서 *SQL Server 스토리지 풀*의 역할을 설명합니다. 다음 섹션에서는 SQL 스토리지 풀의 아키텍처 및 기능을 설명합니다.

## <a name="storage-pool-architecture"></a>스토리지 풀 아키텍처

스토리지 풀은 SQL Server BDC 에코시스템의 로컬 HDFS(Hadoop) 클러스터입니다. 구조화되지 않은 데이터 및 반구조화된 데이터의 영구 스토리지를 제공합니다. Parquet 또는 구분된 텍스트와 같은 데이터 파일은 스토리지 풀에 저장할 수 있습니다. 스토리지를 유지하기 위해 풀의 각 Pod에 영구 볼륨이 연결되어 있습니다. 스토리지 풀 파일은 SQL Server에서 [PolyBase](../relational-databases/polybase/polybase-guide.md)를 통해 액세스하거나 Apache Knox Gateway를 사용하여 직접 액세스할 수 있습니다.

기존의 HDFS 설정은 스토리지가 연결된 상용 하드웨어 컴퓨터의 집합으로 구성됩니다. 내결함성 및 병렬 처리 활용을 위해 노드 전체에 걸쳐 데이터가 블록으로 분산됩니다. 클러스터의 노드 중 하나는 이름 노드로 작동하며 데이터 노드에 있는 파일에 대한 메타데이터 정보를 포함합니다.

![기존의 HDFS 설정](media/concept-storage-pool/classic-hdfs-setup.png)

스토리지 풀은 HDFS 클러스터의 구성원인 스토리지 노드로 구성됩니다. 스토리지 풀은 다음 컨테이너를 호스트하는 각 Pod에서 하나 이상의 Kubernetes Pod를 실행합니다.

- 영구 볼륨(스토리지)에 연결된 Hadoop 컨테이너. 이 형식의 모든 컨테이너는 함께 Hadoop 클러스터를 형성합니다. Hadoop 컨테이너 내에는 주문형 Apache Spark 작업자 프로세스를 만들 수 있는 YARN 노드 관리자 프로세스가 있습니다. Spark 헤드 노드는 Hive metastore, Spark 기록 및 YARN 작업 기록 컨테이너를 호스트합니다.
- OpenRowSet 기술을 사용하여 HDFS에서 데이터를 읽는 SQL Server 인스턴스.
- 메트릭 데이터를 수집하기 위한 `collectd`.
- 로그 데이터를 수집하기 위한 `fluentbit`.

![스토리지 풀 아키텍처](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>담당 작업

스토리지 노드에서 담당하는 작업은 다음과 같습니다.

- Apache Spark를 통한 데이터 수집
- HDFS의 데이터 스토리지(Parquet 및 구분 기호로 분리된 텍스트 형식) HDFS 데이터가 SQL BDC의 모든 스토리지 노드에 분산되므로 HDFS는 데이터 지속성도 제공합니다.
- HDFS 및 SQL Server 엔드포인트를 통한 데이터 액세스

## <a name="accessing-data"></a>데이터 액세스

스토리지 풀의 데이터에 액세스하는 주요 방법은 다음과 같습니다.

- Spark 작업.
- PolyBase 컴퓨팅 노드를 사용하고 HDFS 노드에서 실행되는 SQL Server 인스턴스를 사용하여 데이터를 쿼리하도록 허용하기 위해 SQL Server 외부 테이블 사용.

다음을 사용하여 HDFS와 상호 작용할 수도 있습니다.

- Azure Data Studio.
- [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)].
- Hadoop 컨테이너에 대한 명령을 실행하기 위한 kubectl.
- HDFS http 게이트웨이.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)
- [워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
