---
title: sys.debug dm (Transact-sql) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 05076a6b694ff5861c5a7862b1f8f913ddb67fd6
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536168"
---
# <a name="sysdm_cluster_endpoints-transact-sql"></a>sys.debug dm (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|name|`sysname`|SQL 빅 데이터 클러스터에서 외부에 노출 되는 서비스의 이름입니다. 끝점에 대 한 고유 식별자입니다. 이 보기의 키입니다. Null을 허용하지 않습니다. |  
|description|`nvarchar(4000)`|서비스에 대 한 설명입니다. Null을 허용하지 않습니다. |
|엔드포인트(endpoint)|`sysname`|끝점 url 또는 연결 특성입니다. Null을 허용하지 않습니다. |
|protocol_desc|`sysname`|끝점 프로토콜에 대 한 설명 |

## <a name="permissions"></a>사용 권한

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 `VIEW SERVER STATE` 권한이 필요 합니다.

## <a name="see-also"></a>관련 항목:

[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)](. /.. /v-data-ui-a-aa
