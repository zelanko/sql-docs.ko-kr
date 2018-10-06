---
title: SQL 빅 데이터 클러스터 계산 풀 란? | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: c17f6ac604edc021299f473137dcf6c5e470e3d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48796658"
---
# <a name="what-is-a-sql-big-data-clusters-compute-pool"></a>SQL 빅 데이터 클러스터 계산 풀 란?

이 문서에서는 설명의 역할 *SQL Server 계산 풀* SQL Server 2019에서 빅 데이터 클러스터 미리 보기. 계산 풀 빅 데이터 클러스터에 대 한 스케일 아웃 계산 리소스를 제공합니다. 다음 섹션에서는 아키텍처 및 계산 풀의 기능을 설명합니다.

## <a name="compute-pool-architecture"></a>계산 풀 아키텍처

계산 풀 이루어져 있습니다. 하나 또는 더 많은 Kubernetes에서 실행 되는 pod를 계산 합니다. 자동된 생성 및 관리 이러한 pod에서 조정 되는 [SQL Server 마스터 인스턴스](concept-master-instance.md). 각 pod에는 SQL Server 데이터베이스 엔진의 인스턴스 및 기본 서비스 집합이 포함 되어 있습니다.

> [!NOTE]
> CTP 2.0는 클러스터당 단일 계산 풀만 지원합니다.

## <a name="scale-out-groups"></a>확장 그룹

계산 풀-HDFS, Oracle, MongoDB, Terradata 등 다양 한 데이터 원본에 대 한 분산된 쿼리에 대 한 PolyBase 스케일 아웃 그룹으로 작동할 수 있습니다. Kubernetes의 계산 pod를 사용 하 여 빅 데이터 클러스터를 만들고 계산 pod PolyBase 스케일 아웃 그룹에 대 한 구성 자동화할 수 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 다음 개요를 참조 하세요.

- [SQL Server 2019 빅 데이터 클러스터 란?](big-data-cluster-overview.md)
