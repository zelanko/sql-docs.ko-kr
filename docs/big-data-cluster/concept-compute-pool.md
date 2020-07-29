---
title: 컴퓨팅 풀이란?
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터의 컴퓨팅 풀을 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c7afce300e40f6703cbe4c2d734751aa27256959
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730672"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터의 컴퓨팅 풀이란?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 SQL Server 빅 데이터 클러스터에서 *SQL Server 컴퓨팅 풀*의 역할을 설명합니다. 컴퓨팅 풀은 빅 데이터 클러스터에 스케일 아웃 계산 리소스를 제공합니다. 다음 섹션에서는 컴퓨팅 풀의 아키텍처 및 기능을 설명합니다.

컴퓨팅 풀을 소개하는 5분 분량의 다음 동영상을 시청할 수도 있습니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Compute-Pool/player?WT.mc_id=dataexposed-c9-niner]


## <a name="compute-pool-architecture"></a>컴퓨팅 풀 아키텍처

컴퓨팅 풀은 Kubernetes에서 실행되는 하나 이상의 컴퓨팅 Pod로 구성됩니다. 이러한 Pod의 자동화된 생성 및 관리는 [SQL Server 마스터 인스턴스](concept-master-instance.md)에서 조정됩니다. 각 Pod에는 기본 서비스 집합과 SQL Server 데이터베이스 엔진 인스턴스가 포함되어 있습니다.

## <a name="scale-out-groups"></a>확장 그룹

컴퓨팅 풀은 HDFS, Oracle, MongoDB, Teradata 등의 다양한 데이터 원본에 대한 분산 쿼리를 위한 PolyBase 스케일 아웃 그룹 역할을 할 수 있습니다. Kubernetes의 컴퓨팅 Pod를 사용하여 빅 데이터 클러스터는 PolyBase 스케일 아웃 그룹의 컴퓨팅 Pod 생성 및 구성을 자동화할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)
- [워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
