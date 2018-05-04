---
title: sys.dm_pdw_nodes (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: eba290b9858c50a14892d62baee8dd5baf456cf4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  모든 노드는에 대 한 정보를 보관 [!INCLUDE[ssAPS](../../includes/ssaps-md.md)]합니다. 노드 기기에서 당 하나의 행을 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.<br /><br /> 이 보기에 대 한 키입니다.|형식에 관계 없이 기기에서 고유 합니다.|  
|유형|**nvarchar(32)**|노드의 유형입니다.|' COMPUTE', '제어', '관리'|  
|name|**nvarchar(32)**|노드의 논리적 이름입니다.|적절 한 길이의 문자열입니다.|  
|address|**nvarchar(32)**|이 노드의 IP 주소입니다.|[0-255]의 형식입니다. [0-255]입니다. [0-255]입니다. [0-255]입니다.|  
|is_passive|**int**|노드를 실행 하는 가상 컴퓨터 할당 된 서버에서 실행 중인 장애 조치를 수행 예비 서버 하는지 여부를 나타냅니다.|0 – VM 노드는 원래 서버에서 실행 중입니다.<br /><br /> 1-노드 VM 예비 서버에서 실행 중입니다.|  
|영역(region)|**nvarchar(32)**|노드가 실행 되 고 있는 영역입니다.|' PDW', 'HDINSIGHT'|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
