---
title: 데이터 풀이란?
titleSuffix: SQL Server big data clusters
description: SQL Server 빅 데이터 클러스터에서 SQL Server 데이터 풀의 역할과 SQL 데이터 풀의 아키텍처 및 기능에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b486d0fbb8e0f2c8595251de386bb9f133ac73cf
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379628"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터의 데이터 풀이란?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에서 ‘SQL Server 데이터 풀’의 역할을 설명합니다.  다음 섹션에서는 SQL 데이터 풀의 아키텍처, 기능 및 사용 시나리오에 대해 설명합니다.

5분 분량의 다음 동영상에서는 데이터 풀을 소개하고 데이터 풀에서 데이터를 쿼리하는 방법을 보여 줍니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Querying-Data-from-Big-Data-Cluster-Data-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="data-pool-architecture"></a>데이터 풀 아키텍처

데이터 풀은 SQL Server 영구 스토리지를 클러스터에 제공하는 하나 이상의 SQL Server 데이터 풀 인스턴스로 구성됩니다. 이를 통해 외부 데이터 원본에 대해 캐시된 데이터의 성능 쿼리 및 작업 오프로드를 수행할 수 있습니다. 데이터는 T-SQL 쿼리 또는 Spark 작업을 통해 데이터 풀로 수집됩니다. 큰 데이터 세트에서 성능을 향상시키기 위해 수집된 데이터는 분할에 배포되고 풀의 모든 SQL Server 인스턴스에 저장됩니다. 지원되는 배포 방법은 라운드 로빈 및 복제입니다. 읽기 액세스 최적화를 위해 클러스터된 columnstore 인덱스가 각 데이터 풀 인스턴스의 각 테이블에 만들어집니다. 데이터 풀은 SQL 빅 데이터 클러스터에 대한 스케일 아웃 데이터 마트 역할을 합니다.

![스케일 아웃 데이터 마트](media/concept-data-pool/data-virtualization-improvements.png)

데이터 풀의 SQL Server 인스턴스에 대한 액세스는 SQL Server 마스터 인스턴스에서 관리됩니다. 데이터 풀에 대한 외부 데이터 원본이 데이터 캐시를 저장하는 PolyBase 외부 테이블과 함께 만들어집니다. 백그라운드에서 컨트롤러는 외부 테이블과 일치하는 테이블이 있는 데이터베이스를 데이터 풀에 만듭니다. SQL Server 마스터 인스턴스에서 워크플로는 투명합니다. 컨트롤러에서 특정 외부 테이블 요청을 Compute 풀을 통해 연결될 수 있는 데이터 풀의 SQL Server 인스턴스로 리디렉션하고, 쿼리를 실행하고, 결과 집합을 반환합니다. 데이터 풀의 데이터는 수집하거나 쿼리할 수만 있고 수정할 수는 없습니다. 따라서 데이터를 새로 고치려면 테이블을 삭제한 다음, 테이블을 다시 만들고 후속 데이터를 다시 채워야 합니다. 

## <a name="data-pool-scenarios"></a>데이터 풀 시나리오

 보고 용도는 일반적인 데이터 풀 시나리오입니다. 예를 들어 주간 보고서에 사용되는 여러 PolyBase 데이터 원본을 조인하는 복합 쿼리는 데이터 풀로 오프로드할 수 있습니다. 캐시된 데이터는 빠른 로컬 컴퓨팅을 제공하고, 원본 데이터 세트로 다시 이동할 필요가 없습니다. 마찬가지로, 정기적으로 새로 고쳐야 하는 대시보드 데이터는 최적화된 보고를 위해 데이터 풀에 캐시될 수 있습니다. Machine Learning 반복 검색에서도 데이터 풀의 데이터 세트 캐싱을 활용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)
- [워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
