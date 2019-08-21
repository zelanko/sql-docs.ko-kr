---
title: 데이터 풀이란?
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터의 데이터 풀을 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bfd4d9d6ca24599a2297799555f53a83c6601420
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652260"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터의 데이터 풀이란?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] *SQL Server 데이터 풀* 의 역할을 설명 합니다. 다음 섹션에서는 SQL 데이터 풀의 아키텍처 및 기능을 설명합니다.

## <a name="data-pool-architecture"></a>데이터 풀 아키텍처

데이터 풀은 하나 이상의 SQL Server 데이터 풀 인스턴스로 구성됩니다. SQL 데이터 풀 인스턴스는 클러스터의 영구적 SQL Server 스토리지를 제공합니다. 데이터 풀은 SQL 쿼리 또는 Spark 작업에서 데이터를 수집하는 데 사용됩니다. 큰 데이터 세트에서 성능을 향상하기 위해 데이터 풀의 데이터가 멤버 SQL 데이터 풀 인스턴스에 분할 배포됩니다.

## <a name="scale-out-data-marts"></a>스케일 아웃 데이터 마트

데이터 풀을 사용하면 여러 원본의 외부 데이터가 데이터 풀로 수집되는 스케일 아웃 데이터 마트를 만들 수 있습니다. 데이터가 데이터 풀 인스턴스에 분산되기 때문에 큐레이팅된 데이터에 대한 병렬 쿼리가 더 효율적입니다.

![스케일 아웃 데이터 마트](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>다음 단계

에 대해 자세히 알아보려면 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]다음 리소스를 참조 하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]무엇 인가요?](big-data-cluster-overview.md)
- [워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
