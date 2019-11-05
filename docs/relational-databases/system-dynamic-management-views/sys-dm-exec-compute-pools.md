---
title: sys. dm __l _aastastggggggs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_dm_compute_pools
- dm_dm_compute_pools_TSQL
- dm_dm_compute_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_dm_compute_pools dynamic management view
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 0b21f517b540c69822dd8b1da4aa6a4cf8b8616f
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532955"
---
# <a name="sysdm_dm_compute_pools-transact-sql"></a>sys. dm __l _aastaggggg_l (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|name|`sysname`|계산 풀의 이름입니다. Null을 허용하지 않습니다. 기본 계산 풀에 대 한 `default`를 반환 합니다. |
|compute_pool_id|`int`|풀에 대 한 고유 식별자입니다. 이 보기의 키입니다.|  
|위치|`sysname`|SQL 빅 데이터 클러스터의 컨트롤러에 대 한 끝점입니다. Null을 허용하지 않습니다. |

## <a name="permissions"></a>사용 권한

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 `VIEW SERVER STATE` 권한이 필요 합니다.

## <a name="see-also"></a>관련 항목:

[[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)]이란 ](../../big-data-cluster/big-data-cluster-overview.md)?
