---
title: sys. dm_exec_compute_pools (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_compute_pools
- dm_exec_compute_pools_TSQL
- dm_exec_compute_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_pools dynamic management view
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d749b9a7d9689426bffafe20ee7ab46ce199ffbb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75254607"
---
# <a name="sysdm_exec_compute_pools-transact-sql"></a>sys. dm_exec_compute_pools (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|`sysname`|계산 풀의 이름입니다. Null을 허용하지 않습니다. 기본 `default` 계산 풀에 대해를 반환 합니다. |
|compute_pool_id|`int`|풀에 대 한 고유 식별자입니다. 이 보기의 키입니다.|  
|위치|`sysname`|SQL 빅 데이터 클러스터의 컨트롤러에 대 한 끝점입니다. Null을 허용하지 않습니다. |

## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 권한이 `VIEW SERVER STATE` 필요 합니다.

## <a name="see-also"></a>참고 항목

[무엇 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] ](../../big-data-cluster/big-data-cluster-overview.md)인가요?
