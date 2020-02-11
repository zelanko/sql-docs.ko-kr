---
title: sys. hash_indexes (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 99e3a647c55380e1731b97c267eb754a1f3c6a32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68122738"
---
# <a name="syshash_indexes-transact-sql"></a>sys.hash_indexes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 해시 인덱스 및 해시 인덱스 속성을 보여줍니다. 해시 인덱스는 메모리 내 [OLTP &#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)에서만 지원 됩니다.  
  
 Hash_indexes 뷰에는 다른 열과 동일한 열과 **bucket_count**라는 열이 포함 되어 있습니다. Hash_indexes 뷰의 다른 열에 대 한 자세한 내용은 [&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)을 참조 하십시오.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<상속 된 열>**||[Transact-sql&#41;&#40;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)에서 열을 상속 합니다.|  
|**bucket_count**|**int**|해시 인덱스에 대한 해시 버킷 수입니다.<br /><br /> 값 설정에 대 한 지침을 포함 하 여 bucket_count 값에 대 한 자세한 내용은 [CREATE TABLE &#40;transact-sql&#41;](../../t-sql/statements/create-table-transact-sql.md)를 참조 하세요.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
```  
SELECT object_name([object_id]) AS 'table_name', [object_id],  
     [name] AS 'index_name', [type_desc], [bucket_count]   
FROM sys.hash_indexes   
WHERE OBJECT_NAME([object_id]) = 'T1';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
