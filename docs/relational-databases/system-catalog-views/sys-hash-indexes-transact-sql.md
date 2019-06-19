---
title: sys.hash_indexes (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.hash_indexes_TSQL
- hash_indexes
- sys.hash_indexes
- hash_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.hash_indexes catalog view
ms.assetid: d9e230fb-d3ff-486f-86ef-44898f0a703e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 59d98fe6c7def4073bf0f2cd7cb631c143a766b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004694"
---
# <a name="syshashindexes-transact-sql"></a>sys.hash_indexes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 해시 인덱스 및 해시 인덱스 속성을 보여줍니다. 해시 인덱스의 경우에 지원 됩니다 [In-memory OLTP &#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)합니다.  
  
 Sys.hash_indexes 뷰에 sys.indexes 뷰와 동일한 열 및 라는 추가 열 **bucket_count**합니다. Sys.hash_indexes 뷰의 다른 열에 대 한 자세한 내용은 참조 하세요. [sys.indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<열을 상속 >**||열을 상속 [sys.indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)합니다.|  
|**bucket_count**|**int**|해시 인덱스에 대한 해시 버킷 수입니다.<br /><br /> 값을 설정 하는 것에 대 한 지침을 포함 하는 bucket_count 값에 대 한 자세한 내용은 참조 하세요 [CREATE TABLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)합니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]에서 분할된 테이블 또는 인덱스를 만들 수 있습니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
```  
SELECT object_name([object_id]) AS 'table_name', [object_id],  
     [name] AS 'index_name', [type_desc], [bucket_count]   
FROM sys.hash_indexes   
WHERE OBJECT_NAME([object_id]) = 'T1';  
```  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
