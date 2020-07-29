---
title: 스토리지 풀이란?
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터의 스토리지 풀을 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7a9d3e9e16eb923e0954154b46362cdc88c0bff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730691"
---
# <a name="what-is-the-storage-pool-big-data-clusters-2019"></a>스토리지 풀이란([!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)])?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에서 ‘SQL Server 스토리지 풀’의 역할을 설명합니다.  다음 섹션에서는 SQL 스토리지 풀의 아키텍처 및 기능을 설명합니다.

## <a name="storage-pool-architecture"></a>스토리지 풀 아키텍처

스토리지 풀은 SQL Server on Linux, Spark 및 HDFS로 구성된 스토리지 노드로 이루어져 있습니다. SQL 빅 데이터 클러스터의 모든 스토리지 노드는 HDFS 클러스터의 멤버입니다.

![스토리지 풀 아키텍처](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>담당 작업

스토리지 노드에서 담당하는 작업은 다음과 같습니다.

- Spark를 통한 데이터 수집
- HDFS의 데이터 스토리지(Parquet 및 구분 기호로 분리된 텍스트 형식) HDFS 데이터가 SQL 빅 데이터 클러스터의 모든 스토리지 노드에 분산되므로 HDFS는 데이터 지속성도 제공합니다.
- HDFS 및 SQL Server 엔드포인트를 통한 데이터 액세스

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)
- [워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
