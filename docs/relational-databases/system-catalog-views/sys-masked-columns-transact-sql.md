---
title: sys.masked_columns (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.masked_columns
- masked_columns_tsql
- sys.masked_columns_tsql
- masked_columns
helpviewer_keywords:
- sys.masked_columns catalog view
ms.assetid: 671577e4-d757-4b8d-9aa9-0fc8d51ea9ca
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 432ea847081c8f0060954efdd6e7f2beea1a592d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysmaskedcolumns-transact-sql"></a>sys.masked_columns (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  사용 하 여는 **sys.masked_columns** 동적 데이터 마스킹 함수가 적용 되어 있는 테이블-열에 대 한 쿼리를 뷰. 이 보기는 **sys.columns** 보기에서 상속됩니다. **sys.columns** 뷰의 모든 열과 열이 마스킹되었는지, 그렇다면 정의된 마스킹 함수가 무엇인지 나타내는 **is_masked** 및 **masking_function** 열을 반환합니다. 이 보기는 마스킹 함수가 적용된 열만 보여줍니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|이 열이 속한 개체의 ID입니다.|  
|name|**sysname**|열의 이름입니다. 개체 내에서 고유합니다.|  
|column_id|**int**|열의 ID입니다. 개체 내에서 고유합니다.<br /><br /> 열 ID는 순차적이지 않을 수 있습니다.|  
|**sys.masked_columns** 워크시트에서 상속 되며, 반환 **sys.columns**합니다.|다양 한|참조 [sys.columns &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 더 많은 열 정의 대 한 합니다.|  
|is_masked|**bit**|열이 마스킹 경우를 나타냅니다. 1 마스킹된 나타냅니다.|  
|masking_function|**nvarchar(4000)**|열에 대 한 마스킹 함수입니다.|  
  
## <a name="remarks"></a>주의  
  
## <a name="permissions"></a>Permissions  
 이 보기를 사용자에 게 어떤 종류의 사용 권한에 테이블 또는 사용자에 게 VIEW ANY DEFINITION 권한이 있으면 테이블에 대 한 정보를 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 쿼리는 조인은 **sys.masked_columns** 를 **sys.tables** 마스크 된 열 모두에 대 한 정보를 반환 합니다.  
  
```  
SELECT tbl.name as table_name, c.name AS column_name, c.is_masked, c.masking_function  
FROM sys.masked_columns AS c  
JOIN sys.tables AS tbl   
    ON c.object_id = tbl.object_id  
WHERE is_masked = 1;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [동적 데이터 마스킹](../../relational-databases/security/dynamic-data-masking.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
