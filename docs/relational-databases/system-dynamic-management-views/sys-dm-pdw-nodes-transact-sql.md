---
description: sys.dm_pdw_nodes (Transact-sql)
title: sys.dm_pdw_nodes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b758dafadc743ffc6c51c6d1c94ab3a5ea597e2d
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037688"
---
# <a name="sysdm_pdw_nodes-transact-sql"></a>sys.dm_pdw_nodes (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  의 모든 노드에 대 한 정보를 저장 [!INCLUDE[ssAPS](../../includes/ssaps-md.md)] 합니다. 어플라이언스의 노드당 하나의 행을 나열 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.<br /><br /> 이 보기의 키입니다.|형식에 관계 없이 어플라이언스 전체에서 고유 합니다.|  
|type|**nvarchar(32)**|노드의 유형입니다.|' COMPUTE ', ' CONTROL ', ' MANAGEMENT '|  
|name|**nvarchar(32)**|노드의 논리적 이름입니다.|적절 한 길이의 문자열입니다.|  
|address|**nvarchar(32)**|이 노드의 IP 주소입니다.|[0-255] 형식으로 되어 있습니다. [0-255]. [0-255]. [0-255].|  
|is_passive|**int**|노드를 실행 하는 가상 머신이 할당 된 서버에서 실행 되 고 있는지 또는 예비 서버로 장애 조치 (failover) 되었는지 여부를 나타냅니다.|0-노드 VM이 원래 서버에서 실행 중입니다.<br /><br /> 1-노드 VM이 예비 서버에서 실행 중입니다.|  
|region|**nvarchar(32)**|노드가 실행 되는 영역입니다.|' PDW ', ' HDINSIGHT '|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
