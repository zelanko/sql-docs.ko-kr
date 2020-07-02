---
title: sys. dm_cluster_endpoints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cluster_endpoints
- dm_cluster_endpoints_TSQL
- dm_cluster_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cluster_endpoints dynamic management view
ms.assetid: ''
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 95f251db2efe471455d18f4735be99ecee962a7d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717503"
---
# <a name="sysdm_cluster_endpoints-transact-sql"></a>sys. dm_cluster_endpoints (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/applies-to-version/sqlserver2019.md)]

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|`sysname`|SQL 빅 데이터 클러스터에서 외부에 노출 되는 서비스의 이름입니다. 끝점에 대 한 고유 식별자입니다. 이 보기의 키입니다. Null을 허용하지 않습니다. |  
|description|`nvarchar(4000)`|서비스에 대한 설명입니다. Null을 허용하지 않습니다. |
|엔드포인트(endpoint)|`sysname`|끝점 url 또는 연결 특성입니다. Null을 허용하지 않습니다. |
|protocol_desc|`sysname`|끝점 프로토콜에 대 한 설명 |

## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.

## <a name="see-also"></a>참고 항목

[무엇 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] ](../../big-data-cluster/big-data-cluster-overview.md)인가요?
