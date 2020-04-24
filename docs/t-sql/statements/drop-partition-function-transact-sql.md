---
title: DROP PARTITION FUNCTION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP PARTITION FUNCTION
- DROP_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting partition functions
- DROP PARTITION FUNCTION statement
- partition functions [SQL Server], removing
- dropping partition functions
- removing partition functions
ms.assetid: a4bb055a-a538-4db9-a6fb-550d1eabfa18
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 10cc3cacdf62dd4c8f02b0bd4715f5d0b2fae6b7
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635322"
---
# <a name="drop-partition-function-transact-sql"></a>DROP PARTITION FUNCTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 파티션 함수를 제거합니다. CREATE PARTITION FUNCTION으로 파티션 함수를 만들고 ALTER PARTITION FUNCTION으로 파티션 함수를 수정할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
DROP PARTITION FUNCTION partition_function_name [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *partition_function_name*  
 삭제될 파티션 함수의 이름입니다.  
  
## <a name="remarks"></a>설명  
 현재 파티션 함수를 사용하는 파티션 구성표가 없는 경우에만 파티션 함수를 삭제할 수 있습니다. 파티션 함수를 사용하는 파티션 구성표가 있는 경우 DROP PARTITION FUNCTION은 오류를 반환합니다.  
  
## <a name="permissions"></a>사용 권한  
 DROP PARTITION FUNCTION 함수를 실행하는 데 다음 권한을 사용할 수 있습니다.  
  
-   ALTER ANY DATASPACE 권한. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할 및 **db_owner** 및 **db_ddladmin** 고정 데이터베이스 역할의 멤버에게 부여됩니다.  
  
-   파티션 함수가 생성된 데이터베이스에 대한 CONTROL 또는 ALTER 권한  
  
-   파티션 함수가 생성된 데이터베이스의 서버에 대한 CONTROL SERVER 또는 ALTER ANY DATABASE 권한  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스에 파티션 함수 `myRangePF`가 이미 있는 것으로 가정합니다.  
  
```  
DROP PARTITION FUNCTION myRangePF;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_functions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
