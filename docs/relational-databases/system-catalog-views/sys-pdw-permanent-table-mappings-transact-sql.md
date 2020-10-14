---
title: sys.pdw_permanent_table_mappings (Transact-sql)
ms.custom: ''
ms.date: 07/24/2020
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: mstehrani
ms.author: emtehran
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: c164399e11cd5824017dafbc8e0f7d7e277e1a0c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035737"
---
# <a name="syspdw_permanent_table_mappings-transact-sql"></a>sys.pdw_permanent_table_mappings (Transact-sql)
[!INCLUDE [applies-to-version/asa](../../includes/applies-to-version/asa.md)]

  **Object_id**를 사용 하 여 영구 사용자 테이블을 내부 개체 이름과 연결 합니다.  
  
> [!NOTE]
> **sys.pdw_permanent_table_mappings** 영구 테이블에 대 한 매핑을 보유 하며 임시 또는 외부 테이블 매핑을 포함 하지 않습니다.

|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|physical_name|**nvarchar (36)**|테이블의 실제 이름입니다.<br /><br /> **physical_name** 및 **object_id** 이 보기의 키를 구성 합니다.||  
|object_id|**int**|테이블의 개체 ID입니다. [Sys.debug &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.<br /><br /> **physical_name** 및 **object_id** 이 보기의 키를 구성 합니다.||  
  
## <a name="see-also"></a>참고 항목  
 [Azure Synapse Analytics 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Transact-sql&#41;sys.pdw_index_mappings &#40;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
  
