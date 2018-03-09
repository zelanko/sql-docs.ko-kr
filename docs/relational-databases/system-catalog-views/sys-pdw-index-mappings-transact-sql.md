---
title: sys.pdw_index_mappings (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00bef273eb4b71f28b83f1861c5293a9ecd7a901
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwindexmappings-transact-sql"></a>sys.pdw_index_mappings (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  논리적 인덱스의 고유한 조합에 반영 된 대로 계산 노드에서 사용 되는 실제 이름에 매핑됩니다 **object_id** 인덱스를 포함 한 테이블의 및 **index_id** 내에 특정 인덱스의 테이블입니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|이 인덱스 존재 하는 논리 테이블에 대 한 개체 ID입니다. 참조 [sys.objects&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **physical_name** 및 **object_id** 이 보기에 대 한 키를 형성 합니다.||  
|index_id|**nvarchar(32)**|인덱스에 대 한 ID입니다. 참조 [sys.indexes&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).||  
|physical_name|**nvarchar(36)**|계산 노드의 데이터베이스에 있는 인덱스의 이름입니다.<br /><br /> **physical_name** 및 **object_id** 이 보기에 대 한 키를 형성 합니다.||  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.pdw_table_mappings &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [sys.pdw_database_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  
