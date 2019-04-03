---
title: 데이터 풀이란?
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터에 데이터 풀을 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 8345ae06280458e7fa479ad95ffa20383e429267
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860124"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터에 데이터 풀이란?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 설명의 역할 *SQL Server 데이터 풀* SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 있습니다. 다음 섹션에서는 아키텍처 및 SQL 데이터 풀의 기능을 설명합니다.

## <a name="data-pool-architecture"></a>데이터 풀 아키텍처

하나 이상의 SQL Server 인스턴스의 데이터 풀 데이터 풀 구성 됩니다. SQL 데이터 풀 인스턴스는 클러스터에 대 한 SQL Server의 영구 저장소를 제공합니다. 데이터 풀은 SQL 쿼리 또는 Spark 작업에서 데이터를 수집 하는 데 사용 됩니다. 큰 데이터 집합에서 더 나은 성능을 제공 하려면 데이터 풀에 데이터 멤버 SQL 데이터 풀 인스턴스를 분할 된 데이터베이스로 분산 됩니다.

## <a name="scale-out-data-marts"></a>수평 확장 데이터 마트

데이터 풀 규모 데이터 마트, 여러 원본에서 외부 데이터는 데이터 풀으로 수집 하는 위치를 만들 수 있게 합니다. 데이터가 데이터 풀 인스턴스에 분산 되어, 때문에 큐 레이트 데이터에 대 한 병렬 쿼리는 더 효율적입니다.

![수평 확장 데이터 마트](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [SQL Server 2019 빅 데이터 클러스터는 무엇 인가요?](big-data-cluster-overview.md)
- [워크숍: Microsoft SQL Server 빅 데이터 클러스터 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
