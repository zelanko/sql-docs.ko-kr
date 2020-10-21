---
title: 컴퓨팅 풀이란?
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터의 컴퓨팅 풀을 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 10/15/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9c3374b0820233e20ee73b85947ed2b8a61847c0
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866821"
---
# <a name="what-are-compute-pools-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터의 컴퓨팅 풀이란?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 SQL Server 빅 데이터 클러스터에서 ‘SQL Server 컴퓨팅 풀’의 역할을 설명합니다. 컴퓨팅 풀은 빅 데이터 클러스터에 스케일 아웃 계산 리소스를 제공합니다. SQL Server 마스터 인스턴스에서 계산 작업 또는 중간 결과 집합을 오프로드하는 데 사용됩니다. 다음 섹션에서는 컴퓨팅 풀의 아키텍처, 기능, 사용 시나리오에 대해 설명합니다.

컴퓨팅 풀을 소개하는 5분 분량의 다음 동영상을 시청할 수도 있습니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Compute-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="compute-pool-architecture"></a>컴퓨팅 풀 아키텍처

컴퓨팅 풀은 Kubernetes에서 실행되는 하나 이상의 컴퓨팅 Pod로 구성됩니다. 이러한 Pod의 자동화된 생성 및 관리는 [SQL Server 마스터 인스턴스](concept-master-instance.md)에서 조정됩니다. 각 Pod에는 기본 서비스 집합과 SQL Server 데이터베이스 엔진 인스턴스가 포함되어 있습니다.

![컴퓨팅 풀 아키텍처](media/concept-compute-pool/compute-pool-architecture.png)

## <a name="scale-out-groups"></a>확장 그룹

컴퓨팅 풀은 SQL Server, Oracle, MongoDB, Teradata, HDFS 등의 다양한 외부 데이터 원본에 대한 분산 쿼리를 위한 PolyBase 스케일 아웃 그룹 역할을 할 수 있습니다. Kubernetes의 컴퓨팅 Pod를 사용함으로써 빅 데이터 클러스터는 PolyBase 스케일 아웃 그룹의 컴퓨팅 Pod 생성 및 구성을 자동화할 수 있습니다.

## <a name="compute-pool-scenarios"></a>컴퓨팅 풀 시나리오

컴퓨팅 풀이 사용되는 시나리오는 다음과 같습니다.

- 마스터 인스턴스에 제출된 쿼리가 [스토리지 풀](concept-storage-pool.md)에 있는 하나 이상의 테이블을 사용하는 경우

- 마스터 인스턴스에 제출된 쿼리가 [데이터 풀](concept-data-pool.md)에 있는 하나 이상의 테이블을 라운드 로빈 분산으로 사용하는 경우

- 마스터 인스턴스에 제출된 쿼리가 SQL Server, Oracle, MongoDB, Teradata의 외부 데이터 원본과 함께 **분할된** 테이블을 사용하는 경우. 이 시나리오에서는 OPTION (FORCE SCALEOUTEXECUTION) 쿼리 힌트를 사용하도록 설정해야 합니다.

- 마스터 인스턴스에 제출된 쿼리가 [HDFS 계층화](hdfs-tiering.md)에 있는 하나 이상의 테이블을 사용하는 경우

컴퓨팅 풀이 사용되지 **않는** 시나리오는 다음과 같습니다.

- 마스터 인스턴스에 제출된 쿼리가 외부 Hadoop HDFS 클러스터에 있는 하나 이상의 테이블을 사용하는 경우

- 마스터 인스턴스에 제출된 쿼리가 Azure Blob Storage에 있는 하나 이상의 테이블을 사용하는 경우

- 마스터 인스턴스에 제출된 쿼리가 SQL Server, Oracle, MongoDB, Teradata의 외부 데이터 원본과 함께 **분할되지 않은** 테이블을 사용하는 경우

- OPTION (DISABLE SCALEOUTEXECUTION) 쿼리 힌트를 사용하도록 설정한 경우

- 마스터 인스턴스에 제출된 쿼리가 마스터 인스턴스에 있는 데이터베이스에 적용되는 경우

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)
- [워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
