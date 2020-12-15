---
description: sys.pdw_index_mappings (Transact-sql)
title: sys.pdw_index_mappings (Transact-sql) | Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 31e4b7e34df647a7c3a12b187cb0067ec399bcbd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97444288"
---
# <a name="syspdw_index_mappings-transact-sql"></a>sys.pdw_index_mappings (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  는 인덱스를 포함 하는 테이블 **object_id** 의 고유 조합과 해당 테이블 내의 특정 인덱스 **index_id** 에 의해 반영 되는 논리 인덱스를 계산 노드에서 사용 되는 실제 이름에 매핑합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|이 인덱스가 있는 논리 테이블의 개체 ID입니다. [Sys.debug &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.<br /><br /> **physical_name** 및 **object_id** 이 보기의 키를 구성 합니다.||  
|index_id|**nvarchar(32)**|인덱스의 ID입니다. [&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)를 참조 하세요.||  
|physical_name|**nvarchar (36)**|계산 노드에 있는 데이터베이스의 인덱스 이름입니다.<br /><br /> **physical_name** 및 **object_id** 이 보기의 키를 구성 합니다.||  
  
## <a name="see-also"></a>참고 항목  
 [Azure Synapse Analytics 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Transact-sql&#41;sys.pdw_table_mappings &#40;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [Transact-sql&#41;sys.pdw_permanent_table_mappings &#40;](../../relational-databases/system-catalog-views/sys-pdw-permanent-table-mappings-transact-sql.md)   
 [Transact-sql&#41;sys.pdw_database_mappings &#40;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  
