---
title: SQL Server 빅 데이터 클러스터 저장소 풀 란? | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 100ce09f7066a6df33d7b1daaf50db50bda4ed03
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48796316"
---
# <a name="what-is-the-sql-server-big-data-clusters-storage-pool"></a>SQL Server 빅 데이터 클러스터 저장소 풀 란?

이 문서에서는의 역할을 설명 합니다 *SQL Server 저장소 풀* SQL Server 2019에서 빅 데이터 클러스터 미리 보기. 다음 섹션에서는 아키텍처 및 SQL 저장소 풀의 기능을 설명합니다.

## <a name="storage-pool-architecture"></a>저장소 풀 아키텍처

Linux, Spark 및 HDFS에서 SQL Server 노드 구성 저장소의 저장소 풀 구성 됩니다. SQL 빅 데이터 클러스터의 모든 저장소 노드에 HDFS 클러스터의 멤버입니다.

![저장소 풀 아키텍처](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>책임

저장소 노드는 담당 합니다.

- Spark 통해 데이터 수집 합니다.
- HDFS (Parquet 형식)에서 데이터를 저장 합니다. 또한 HDFS로 HDFS 데이터에 SQL 빅 데이터 클러스터의 모든 저장소 노드에 걸쳐 데이터 지 속성을 제공 합니다.
- HDFS와 SQL Server 끝점을 통한 데이터 액세스 합니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 다음 개요를 참조 하세요.

- [SQL Server 2019 빅 데이터 클러스터 란?](big-data-cluster-overview.md)
