---
title: sys. column_store_dictionaries (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_store_dictionaries_TSQL
- column_store_dictionaries
- column_store_dictionaries_TSQL
- sys.column_store_dictionaries
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_dictionaries catalog view
ms.assetid: 56efd563-2f72-4caf-94e3-8a182385c173
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2348633a2c357868e4688d7b37c5cf28aed6441a
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304760"
---
# <a name="syscolumn_store_dictionaries-transact-sql"></a>sys.column_store_dictionaries(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  xVelocity 메모리 최적화 columnstore 인덱스에 사용되는 각 사전에 대한 행을 포함합니다. 사전은 일부 데이터 형식을 인코딩하는 데 사용되므로 columnstore 인덱스의 일부 열에만 사전이 있습니다. 사전은 모든 세그먼트의 기본 사전으로 있을 수 있으며 열 세그먼트의 하위 집합에 사용되는 다른 보조 사전으로 있을 수도 있습니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**hobt_id**|**bigint**|이 columnstore 인덱스가 있는 테이블에 대 한 힙 또는 B-트리 인덱스 (HoBT)의 ID입니다.|  
|**column_id**|**int**|1로 시작 하는 columnstore 열의 ID입니다. 첫 번째 열에는 ID = 1, 두 번째 열에는 ID = 2 등이 있습니다.|  
|**dictionary_id**|**int**|열 세그먼트와 연결 된 두 가지 종류의 사전 (전역 및 로컬)이 있을 수 있습니다. Dictionary_id 0은 해당 열에 대 한 모든 열 세그먼트 (각 행 그룹에 대해 하나씩)에서 공유 되는 전역 사전을 나타냅니다.|  
|**version**|**int**|사전 형식의 버전입니다.|  
|**유형**|**int**|사전 종류입니다.<br /><br /> 1- **int** 값을 포함 하는 해시 사전<br /><br /> 2-사용 되지 않음<br /><br /> 3-문자열 값을 포함 하는 해시 사전<br /><br /> 4- **float** 값을 포함 하는 해시 사전<br /><br /> 사전에 대 한 자세한 내용은 [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md)를 참조 하세요.|  
|**last_id**|**int**|사전의 마지막 데이터 ID입니다.|  
|**entry_count**|**bigint**|사전에 있는 항목의 개수입니다.|  
|**on_disc_size**|**bigint**|사전의 크기(바이트)입니다.|  
|**partition_id**|**bigint**|파티션 ID를 나타냅니다. 데이터베이스 내에서 고유합니다.|  
  
## <a name="permissions"></a>사용 권한  
테이블에 대한 `VIEW DEFINITION` 권한이 필요합니다. 사용자에 게 `SELECT` 권한이 없는 경우 (last_id, entry_count, data_ptr 열은 null을 반환 합니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [all_columns &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [computed_columns &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_segments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

