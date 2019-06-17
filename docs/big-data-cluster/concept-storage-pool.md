---
title: 저장소 풀이란?
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터에 저장소 풀을 설명 합니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 7ff8b16ec5f1ea0d1df401cee9657eb8d564863a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782989"
---
# <a name="what-is-the-storage-pool-sql-server-big-data-clusters"></a>저장소 풀 (SQL Server 빅 데이터 클러스터) 란?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는의 역할을 설명 합니다 *SQL Server 저장소 풀* SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서. 다음 섹션에서는 아키텍처 및 SQL 저장소 풀의 기능을 설명합니다.

## <a name="storage-pool-architecture"></a>저장소 풀 아키텍처

Linux, Spark 및 HDFS에서 SQL Server 노드 구성 저장소의 저장소 풀 구성 됩니다. SQL 빅 데이터 클러스터에서 모든 저장소 노드에 HDFS 클러스터의 멤버입니다.

![저장소 풀 아키텍처](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>책임

저장소 노드는 담당 합니다.

- Spark 통해 데이터 수집 합니다.
- HDFS (Parquet 형식)에서 데이터를 저장 합니다. 또한 HDFS로 HDFS 데이터에 SQL 빅 데이터 클러스터의 모든 저장소 노드에 걸쳐 데이터 지 속성을 제공 합니다.
- HDFS와 SQL Server 끝점을 통한 데이터 액세스 합니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [SQL Server 2019 빅 데이터 클러스터는 무엇 인가요?](big-data-cluster-overview.md)
- [워크숍: Microsoft SQL Server 빅 데이터 클러스터 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
