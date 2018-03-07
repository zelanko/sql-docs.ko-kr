---
title: $PARTITION (transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- $partition_TSQL
- $partition
dev_langs:
- TSQL
helpviewer_keywords:
- $PARTITION function
- partitions [SQL Server], numbers
ms.assetid: abc865d0-57a8-49da-8821-29457c808d2a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7fb60ef43ba359bef366a113704a784ce0f73902
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="partition-transact-sql"></a>$PARTITION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 지정된 파티션 함수에 대해 분할 열 값 집합이 매핑되는 파티션 번호를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
[ database_name. ] $PARTITION.partition_function_name(expression)  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 파티션 함수가 포함된 데이터베이스의 이름입니다.  
  
 *partition_function_name*  
 분할 열 값 집합이 적용되는 기존 파티션 함수의 이름입니다.  
  
 *expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 데이터 형식이 일치 하거나 해당 분할 열의 데이터 형식을 암시적으로 변환할 수 있어야 합니다. *식* 에 현재 참여 하는 분할 열의 이름일 수도 있습니다 *partition_function_name*합니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 $PARTITION 반환은 **int** 파티션 함수의 파티션 수에서 1 사이의 값입니다.  
  
 $PARTITION은 값이 현재 파티션 함수를 사용하는 분할된 테이블이나 인덱스에 있는지에 관계없이 올바른 값의 파티션 번호를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-getting-the-partition-number-for-a-set-of-partitioning-column-values"></a>1. 분할 열 값 집합에 대한 파티션 번호 가져오기  
 다음 예에서는 테이블이나 인덱스를 4개의 파티션으로 분할하는 파티션 함수 `RangePF1`을 만듭니다. $PARTITION은 `10`의 분할 열을 나타내는 `RangePF1` 값이 테이블의 파티션 1에 포함되는지 확인하는 데 사용됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE PARTITION FUNCTION RangePF1 ( int )  
AS RANGE FOR VALUES (10, 100, 1000) ;  
GO  
SELECT $PARTITION.RangePF1 (10) ;  
GO  
```  
  
### <a name="b-getting-the-number-of-rows-in-each-nonempty-partition-of-a-partitioned-table-or-index"></a>2. 분할된 테이블이나 인덱스의 비어 있지 않은 각 파티션에 있는 행 수 가져오기  
 다음 예에서는 데이터가 있는 `TransactionHistory` 테이블의 각 파티션에 있는 행 수를 반환합니다. `TransactionHistory` 테이블은 파티션 함수 `TransactionRangePF1`을 사용하며 `TransactionDate` 열에서 분할됩니다.  
  
 이 예를 실행하려면 먼저 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예 데이터베이스에 대해 PartitionAW.sql 스크립트를 실행해야 합니다. 자세한 내용은 참조 [PartitioningScript](http://go.microsoft.com/fwlink/?LinkId=201015)합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT $PARTITION.TransactionRangePF1(TransactionDate) AS Partition,   
COUNT(*) AS [COUNT] FROM Production.TransactionHistory   
GROUP BY $PARTITION.TransactionRangePF1(TransactionDate)  
ORDER BY Partition ;  
GO  
```  
  
### <a name="c-returning-all-rows-from-one-partition-of-a-partitioned-table-or-index"></a>3. 분할된 테이블이나 인덱스의 특정 파티션에서 모든 행 반환  
 다음 예에서는 `5` 테이블의 파티션 `TransactionHistory`에 있는 모든 행을 반환합니다.  
  
> [!NOTE]  
>  이 예를 실행하려면 먼저 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예 데이터베이스에 대해 PartitionAW.sql 스크립트를 실행해야 합니다. 자세한 내용은 참조 [PartitioningScript](http://go.microsoft.com/fwlink/?LinkId=201015)합니다.  
  
```  
SELECT * FROM Production.TransactionHistory  
WHERE $PARTITION.TransactionRangePF1(TransactionDate) = 5 ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)  
  
  
