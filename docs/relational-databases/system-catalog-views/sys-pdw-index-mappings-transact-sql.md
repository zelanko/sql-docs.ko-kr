---
title: sys.pdw_index_mappings (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: e331dbea1232febefc8b0b4848dfd51a085ec692
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035654"
---
# <a name="syspdwindexmappings-transact-sql"></a>sys.pdw_index_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  논리적 인덱스의 고유한 조합 하 여 반영 된 대로 계산 노드에서 사용 되는 실제 이름에 매핑됩니다 **object_id** 인덱스를 보관 하는 테이블의 하며 **index_id** 내 특정 인덱스 테이블입니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|이 인덱스 존재 하는 논리 테이블에 대 한 개체 ID입니다. 참조 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)합니다.<br /><br /> **physical_name** 하 고 **object_id** 이 보기에 대 한 키를 형성 합니다.||  
|index_id|**nvarchar(32)**|인덱스의 ID입니다. 참조 [sys.indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)합니다.||  
|physical_name|**nvarchar(36)**|계산 노드에서 데이터베이스에서 인덱스의 이름입니다.<br /><br /> **physical_name** 하 고 **object_id** 이 보기에 대 한 키를 형성 합니다.||  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.pdw_table_mappings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [sys.pdw_database_mappings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  
