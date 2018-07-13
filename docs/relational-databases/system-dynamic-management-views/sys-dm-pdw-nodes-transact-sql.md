---
title: sys.dm_pdw_nodes (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 3f307d70f7c161743d81c33916046e88cadad9e9
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926794"
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  에 있는 노드의 모든 정보를 담고 [!INCLUDE[ssAPS](../../includes/ssaps-md.md)]합니다. 어플라이언스의 노드 당 하나의 행을 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.<br /><br /> 이 보기에 대 한 키입니다.|형식에 관계 없이 어플라이언스에서 고유 합니다.|  
|유형|**nvarchar(32)**|노드의 형식입니다.|' 계산 ', 'CONTROL', '관리'|  
|NAME|**nvarchar(32)**|노드의 논리적 이름입니다.|적절 한 길이의 문자열입니다.|  
|address|**nvarchar(32)**|이 노드의 IP 주소입니다.|형식 [0-255]입니다. [0-255]입니다. [0-255]입니다. [0-255]입니다.|  
|is_passive|**int**|노드를 실행 하는 가상 컴퓨터는 할당 된 서버에서 실행 되 고 예비 서버로 장애 조치에 하는지 여부를 나타냅니다.|0 – 노드 VM은 원본 서버에서 실행 됩니다.<br /><br /> 1-노드 VM가 서버에서 실행 됩니다.|  
|영역(region)|**nvarchar(32)**|노드가 실행 되 고 있는 지역입니다.|' PDW', 'HDINSIGHT'|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
