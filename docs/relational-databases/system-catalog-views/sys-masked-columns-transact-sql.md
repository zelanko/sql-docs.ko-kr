---
title: sys. masked_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.masked_columns
- masked_columns_tsql
- sys.masked_columns_tsql
- masked_columns
helpviewer_keywords:
- sys.masked_columns catalog view
ms.assetid: 671577e4-d757-4b8d-9aa9-0fc8d51ea9ca
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e059265dc5f5e0d2e4bc4a3b1396d2401386d7b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68102370"
---
# <a name="sysmasked_columns-transact-sql"></a>sys. masked_columns (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **Masked_columns** 뷰를 사용 하 여 동적 데이터 마스킹 함수가 적용 된 테이블 열을 쿼리 합니다. 이 보기는 **sys.columns** 보기에서 상속됩니다. 
  **sys.columns** 뷰의 모든 열과 열이 마스킹되었는지, 그렇다면 정의된 마스킹 함수가 무엇인지 나타내는 **is_masked** 및 **masking_function** 열을 반환합니다. 이 보기는 마스킹 함수가 적용된 열만 보여줍니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|이 열이 속한 개체의 ID입니다.|  
|name|**sysname**|열의 이름입니다. 개체 내에서 고유합니다.|  
|column_id|**int**|열의 ID입니다. 개체 내에서 고유합니다.<br /><br /> 열 ID는 순차적이지 않을 수 있습니다.|  
|**masked_columns** 은 **sys 열**에서 상속 된 더 많은 열을 반환 합니다.|다양|자세한 열 정의는 [&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 를 참조 하세요.|  
|is_masked|**bit**|열이 마스킹 되는지 여부를 나타냅니다. 1은 마스킹 됨을 나타냅니다.|  
|masking_function|**nvarchar(4000)**|열에 대 한 마스킹 함수입니다.|  
  
## <a name="remarks"></a>설명  
  
## <a name="permissions"></a>사용 권한  
 이 뷰는 사용자에 게 테이블에 대 한 일부 사용 권한이 있거나 사용자에 게 VIEW ANY DEFINITION 권한이 있는 경우 테이블에 대 한 정보를 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 쿼리는 sys **. masked_columns** 를 조인 **하 여 마스킹된** 모든 열에 대 한 정보를 반환 합니다.  
  
```  
SELECT tbl.name as table_name, c.name AS column_name, c.is_masked, c.masking_function  
FROM sys.masked_columns AS c  
JOIN sys.tables AS tbl   
    ON c.object_id = tbl.object_id  
WHERE is_masked = 1;  
```  
  
## <a name="see-also"></a>참고 항목  
 [동적 데이터 마스킹](../../relational-databases/security/dynamic-data-masking.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
