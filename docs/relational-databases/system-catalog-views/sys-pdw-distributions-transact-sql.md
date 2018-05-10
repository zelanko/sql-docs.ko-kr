---
title: sys.pdw_distributions (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 49c439e4d3b210025dfd28f45cd63b9bfcb5620d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="syspdwdistributions-transact-sql"></a>sys.pdw_distributions (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  어플라이언스에서 분포에 대 한 정보를 보유합니다. 어플라이언스 배포 마다 한 행을 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|분포에 관련 된 고유 숫자 id입니다.<br /><br /> 이 보기에 대 한 키입니다.|1부터 계산 노드당의 수를 곱한 어플라이언스의 계산 노드 수입니다.|  
|pdw_node_id|**int**|이 분포에는 노드의 ID입니다.|pdw_node_id 참조 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|name|**nvarchar(32)**|분산된 테이블에 대 한 접미사로 사용 되는 배포와 관련 된 식별자는 문자열입니다.|문자열 구성의 ' Z', ' a ~ z', ' 0-9', '_','-'.|  
|position|**int**|해당 노드에서 다른 배포에 각 노드 내에서 배포의 위치입니다.|노드당의 수는 1입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
