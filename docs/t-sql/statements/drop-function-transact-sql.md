---
title: DROP FUNCTION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_FUNCTION_TSQL
- DROP FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined functions [SQL Server], removing
- removing user-defined functions
- DROP FUNCTION statement
- dropping user-defined functions
- deleting user-defined functions
ms.assetid: ee5ad283-9e44-4109-902f-0ce12669ee11
caps.latest.revision: 49
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 1654d9d81598edb09c3fafe09b808ecbabe8c812
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39458257"
---
# <a name="drop-function-transact-sql"></a>DROP FUNCTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  현재 데이터베이스에서 하나 이상의 사용자 정의 함수를 제거합니다. 사용자 정의 함수는 [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md)을 사용하여 만들고 [ALTER FUNCTION](../../t-sql/statements/alter-function-transact-sql.md)을 사용하여 수정할 수 있습니다.  
  
 DROP 함수는 고유하게 컴파일된 사용자 정의 스칼라 함수를 지원합니다. 자세한 내용은 [메모리 내 OLTP에 대한 사용자 정의 스칼라 함수](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
 -- SQL Server, Azure SQL Database 

DROP FUNCTION [ IF EXISTS ] { [ schema_name. ] function_name } [ ,...n ]   
[;]
```

```  
 -- Azure SQL Data Warehouse, Parallel Data Warehouse 

DROP FUNCTION [ schema_name. ] function_name
[;] 
```  
   
  
## <a name="arguments"></a>인수  
 *IF EXISTS*    
 이미 있는 경우에만 함수를 조건적으로 삭제합니다. [!INCLUDE[ssnoversion_md](../../includes/ssnoversion_md.md)] 2016과 [!INCLUDE[sssds_md](../../includes/sssds_md.md)]부터 사용할 수 있습니다.
  
 *schema_name*  
 사용자 정의 함수가 속한 스키마의 이름입니다.  
  
 *function_name*  
 제거할 사용자 정의 함수의 이름입니다. 필요에 따라 스키마 이름을 지정할 수 있지만 서버 이름과 데이터베이스 이름은 지정할 수 없습니다.  
  
## <a name="remarks"></a>Remarks  
 DROP FUNCTION은 데이터베이스에 이 함수를 참조하고 SCHEMABINDING을 사용하여 만든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수나 뷰가 있거나 해당 함수를 참조하는 계산 열, CHECK 제약 조건 또는 DEFAULT 제약 조건이 있는 경우 실패합니다.  
  
 DROP FUNCTION은 이 함수를 참조하고 인덱싱된 계산 열이 있는 경우 실패합니다.  
  
## <a name="permissions"></a>Permissions  
 DROP FUNCTION을 실행하려면 사용자에게 최소한 해당 함수가 속한 스키마에 대한 ALTER 권한이나 해당 함수에 대한 CONTROL 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-function"></a>1. 함수 삭제  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]예제 데이터베이스의 `Sales` 스키마에서 `fn_SalesByStore` 사용자 정의 함수를 삭제합니다. 이 함수를 만들려면의 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)에서 예제 B를 참조 하십시오.  
  
```  
DROP FUNCTION Sales.fn_SalesByStore;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [OBJECT_ID&#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
