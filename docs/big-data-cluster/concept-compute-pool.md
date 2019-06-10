---
title: 계산 풀이란?
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 계산 풀을 설명합니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: ec1223e9255dd4dda40fb26fb9e8306bec57d926
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800725"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터에 계산 풀이란?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 설명의 역할 *SQL Server 계산 풀* SQL Server 2019 미리 보기 빅 데이터 클러스터에 있습니다. 계산 풀 빅 데이터 클러스터에 대 한 스케일 아웃 계산 리소스를 제공합니다. 다음 섹션에서는 아키텍처 및 계산 풀의 기능을 설명합니다.

## <a name="compute-pool-architecture"></a>계산 풀 아키텍처

계산 풀 이루어져 있습니다. 하나 또는 더 많은 Kubernetes에서 실행 되는 pod를 계산 합니다. 자동된 생성 및 관리 이러한 pod에서 조정 되는 [SQL Server 마스터 인스턴스](concept-master-instance.md). 각 pod에는 SQL Server 데이터베이스 엔진의 인스턴스 및 기본 서비스 집합이 포함 되어 있습니다.

## <a name="scale-out-groups"></a>확장 그룹

계산 풀-HDFS, Oracle, MongoDB, Terradata 등 다양 한 데이터 원본에 대 한 분산된 쿼리에 대 한 PolyBase 스케일 아웃 그룹으로 작동할 수 있습니다. Kubernetes의 계산 pod를 사용 하 여 빅 데이터 클러스터를 만들고 계산 pod PolyBase 스케일 아웃 그룹에 대 한 구성 자동화할 수 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [SQL Server 2019 빅 데이터 클러스터는 무엇 인가요?](big-data-cluster-overview.md)
- [워크숍: Microsoft SQL Server 빅 데이터 클러스터 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
