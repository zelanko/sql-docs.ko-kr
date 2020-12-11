---
title: PolyBase 스케일 아웃 그룹 | Microsoft Docs
description: PolyBase 그룹 기능을 사용하여 SQL Server 인스턴스 클러스터를 만듭니다. 이렇게 하면 외부 원본에서 가져온 대량 데이터 세트의 쿼리 성능이 향상됩니다.
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sql13.swb.polybasescaleoutcluster.page.f1
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 3ab1841c009094831ae114d701d526a1d3036dba
ms.sourcegitcommit: 773c1203e3c4617606cecb2626f6b2f2c855a53d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535277"
---
# <a name="polybase-scale-out-groups"></a>PolyBase 스케일 아웃 그룹

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

PolyBase를 사용하는 독립 실행형 SQL Server 인스턴스는 Hadoop 또는 Azure Blob 스토리지에서 대규모 데이터 집합을 처리하는 경우 성능상의 병목 지점이 될 수 있습니다. PolyBase 그룹 기능을 사용하면 SQL Server 인스턴스 클러스터를 만들어 Hadoop 또는 Azure Blob Storage와 같은 외부 데이터 원본에서 쿼리 성능을 향상하기 위해 스케일 아웃 방식으로 대규모 데이터를 처리할 수 있습니다. 이제 워크로드의 성능 요구에 맞게 SQL Server 컴퓨팅을 확장할 수 있습니다. SQL Server 인스턴스 그룹인 PolyBase 스케일 아웃 그룹을 사용하여 병렬 처리 아키텍처에서 대규모 외부 데이터 집합을 처리할 수 있습니다. 그룹에 더 많은 SQL Server 인스턴스를 추가하면 데이터 부하 및 쿼리 성능이 비례해서 증가할 수 있습니다. 
  
[PolyBase 시작](./polybase-guide.md) 및 [PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md)를 참조하세요.
  
![PolyBase 스케일 아웃 그룹 다이어그램](../../relational-databases/polybase/media/polybase-scale-out-groups.png "PolyBase 스케일 아웃 그룹")  
  
## <a name="head-node"></a>헤드 노드  

헤드 노드는 PolyBase 쿼리가 제출되는 SQL Server 인스턴스를 포함합니다. 각 PolyBase 그룹은 헤드 노드를 하나만 가질 수 있습니다. 헤드 노드는 SQL Server 인스턴스에 있는 SQL Server 데이터베이스 엔진, PolyBase 엔진 및 PolyBase 데이터 이동 서비스의 논리적 그룹입니다. SQL Server 2017 및 SQL Server 2016를 사용하는 경우 헤드 노드는 Enterprise Edition이어야 합니다. SQL Server 2019부터 PolyBase 헤드 노드는 Enterprise 또는 Standard Edition일 수 있습니다.
  
## <a name="compute-node"></a>컴퓨팅 노드

컴퓨팅 노드는 외부 데이터에서 확장 쿼리를 지원하는 SQL Server 인스턴스를 포함합니다. 컴퓨팅 노드는 SQL Server 인스턴스에 있는 SQL Server 및 PolyBase 데이터 이동 서비스의 논리적 그룹입니다. PolyBase 그룹은 여러 컴퓨팅 노드를 가질 수 있습니다. 헤드 노드와 컴퓨팅 노드는 동일한 SQL Server 버전을 실행해야 합니다. SQL Server 2016의 초기 릴리스의 컴퓨팅 노드는 Enterprise 또는 Standard Edition일 수 있습니다. SQL Server 2016 SP1부터는 SQL Server의 모든 버전이 컴퓨팅 노드일 수 있습니다.

## <a name="scale-out-reads"></a>스케일 아웃 읽기

외부 SQL Server, Oracle 또는 Teradata 인스턴스를 쿼리할 경우 분할된 테이블은 스케일 아웃 읽기에서 혜택을 얻습니다. PolyBase 스케일 아웃 그룹의 각 노드는 최대 8개 Reader를 회전시켜 외부 데이터를 읽을 수 있습니다. 또한 각 Reader에는 외부 테이블에서 읽을 하나의 파티션이 할당됩니다. 

예를 들어 12개월 파티션과 3개 노드로 이루어진 PolyBase 스케일 아웃 그룹을 포함하는 외부 SQL Server 테이블이 있는 경우 각 노드는 PolyBase Reader 4개를 사용하여 12개 파티션 각각을 처리합니다. 이 내용은 아래 이미지에 설명되어 있습니다. 

> [!NOTE]
>  이 방식은 Hadoop을 통한 스케일 아웃 읽기와 다릅니다. 

![PolyBase 스케일 아웃 읽기](../../relational-databases/polybase/media/polybase-scale-out-groups2.png "PolyBase 스케일 아웃 그룹")
  
## <a name="distributed-query-processing"></a>분산형 쿼리 처리  

PolyBase 쿼리는 헤드 노드에서 SQL Server로 전송됩니다. 외부 테이블을 참조하는 쿼리 부분은 PolyBase 엔진으로 분배됩니다.
  
PolyBase 엔진은 PolyBase 쿼리 뒤에 있는 주요 구성 요소입니다. 외부 데이터에 대한 쿼리 구문을 분석하고 쿼리 계획을 생성하며 작업을 컴퓨팅 노드의 데이터 이동 서비스로 분배해 실행합니다. 작업이 완료되면 컴퓨팅 노드에서 결과를 수신한 후 SQL Server로 전송하여 처리하고 클라이언트로 반환합니다.
  
PolyBase 데이터 이동 서비스는 PolyBase 엔진에서 지침을 수신하고 헤드 및 컴퓨팅 노드의 SQL Server 인스터스 사이 및 HDFS 와 SQL Server 사이에서 데이터를 전송합니다.
  
## <a name="next-steps"></a>다음 단계

PolyBase 스케일 아웃 그룹을 구성하려면 다음 안내서를 참조하세요.

[Windows에서 PolyBase 스케일 아웃 그룹 개선](configure-scale-out-groups-windows.md)

## <a name="see-also"></a>참고 항목

 [sys-dm-exec-compute-nodes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)   
 [sys-dm-exec-compute-node-status](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)   
 [sys.dm_exec_compute_node_errors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)
