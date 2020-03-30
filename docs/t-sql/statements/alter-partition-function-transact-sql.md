---
title: ALTER PARTITION FUNCTION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION FUNCTION
- ALTER_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- splitting partitions [SQL Server]
- partitioned tables [SQL Server], splitting
- ALTER PARTITION FUNCTION statement
- merging partitions [SQL Server]
- partitioned indexes [SQL Server], merging
- partitioned indexes [SQL Server], splitting
- modifying partition functions
- partition functions [SQL Server], modifying
- partitioned tables [SQL Server], merging
ms.assetid: 70866dac-0a8f-4235-8108-51547949ada4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c2418bedb172464002fd640a50c8b57f3daca712
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68071250"
---
# <a name="alter-partition-function-transact-sql"></a>ALTER PARTITION FUNCTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

경계 값을 나누거나 병합하여 파티션 함수를 변경합니다. ALTER PARTITION FUNCTION을 실행하면 파티션 함수를 사용하는 하나의 테이블 파티션 또는 인덱스를 두 개의 파티션으로 분할할 수 있습니다. 이 문은 두 개의 파티션을 하나 적은 파티션으로 병합할 수도 있습니다.  
  
> [!CAUTION]  
>  둘 이상의 테이블 또는 인덱스가 같은 파티션 함수를 사용할 수 있습니다. ALTER PARTITION FUNCTION은 단일 트랜잭션에 있는 모든 대상에 영향을 줍니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER PARTITION FUNCTION partition_function_name()  
{   
    SPLIT RANGE ( boundary_value )  
  | MERGE RANGE ( boundary_value )   
} [ ; ]  
```  
  
## <a name="arguments"></a>인수  
*partition_function_name*  
수정할 파티션 함수의 이름입니다.  
  
SPLIT RANGE ( *boundary_value* )  
하나의 파티션을 파티션 함수에 추가합니다. *boundary_value*는 새 파티션의 범위를 결정하며 반드시 파티션 함수의 기존 경계 범위와 달라야 합니다. *boundary_value*에 따라 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 하나의 기존 범위를 둘로 나눕니다. 이 두 범위 중에서 새 *boundary_value*가 있는 범위가 새 파티션입니다.  
  
파일 그룹은 온라인 상태로 존재해야 합니다. 새 파티션을 포함할 파티션 함수를 NEXT USED로 사용하는 파티션 구성표가 파일 그룹을 표시해야 합니다. CREATE PARTITION SCHEME 문은 파티션에 파일 그룹을 할당합니다. CREATE PARTITION FUNCTION 문은 파일 그룹을 포함할 파티션을 파일 그룹보다 적게 만듭니다. CREATE PARTITION SCHEME 문이 필요한 것보다 많은 파일 그룹을 확보할 수도 있습니다. 이 경우 할당되지 않은 파일 그룹으로 끝나게 됩니다. 또한 파티션 구성표는 파일 그룹 중 하나를 NEXT USED로 표시합니다. 이 파일 그룹은 새 파티션을 포함합니다. 파티션 구성표가 NEXT USED로 표시하는 파일 그룹이 없는 경우 ALTER PARTITION SCHEME 문을 사용해야 합니다. 

ALTER PARTITION SCHEME 문은 새 파티션을 포함할 파일 그룹을 추가하거나 기존 파일 그룹을 선택합니다. 이미 파티션을 포함하는 파일 그룹이 추가 파티션을 포함하도록 할당할 수 있습니다. 파티션 함수는 둘 이상의 파티션 구성표에 참여할 수 있습니다. 따라서 파티션을 추가하는 파티션 함수를 사용하는 모든 파티션 구성표에는 NEXT USED 파일 그룹이 있어야 합니다. 그렇지 않으면 ALTER PARTITION FUNCTION 문은 NEXT USED 파일 그룹이 부족한 파티션 구성표 또는 스키마를 표시하는 오류를 일으키고 실패합니다.  
  
동일한 파일 그룹에 모든 파티션을 만든 경우 파일 그룹은 초기에 자동으로 NEXT USED 파일 그룹이 되도록 할당됩니다. 그러나 분할 작업이 실행된 후에는 더 이상 선택된 NEXT USED 파일 그룹이 없습니다. ALTER PARTITION SCHEME을 사용하여 파일 그룹을 NEXT USED 파일 그룹으로 명시적으로 할당해야 합니다. 그렇지 않으면 후속 분할 작업은 실패하게 됩니다.  
  
> [!NOTE]  
>  columnstore 인덱스 관련 제한 사항: 테이블에 columnstore 인덱스가 있는 경우에는 빈 파티션만 분할할 수 있습니다. 이 작업을 수행하기 전에 columnstore 인덱스를 삭제하거나 사용하지 않도록 설정해야 합니다.  
  
MERGE [ RANGE ( *boundary_value*) ]  
파티션을 삭제하고 해당 파티션에 있는 모든 값을 나머지 파티션으로 병합합니다. RANGE(*boundary_value*)는 삭제된 파티션의 값을 병합하는 기존의 경계 값이어야 합니다. 원래 *boundary_value*를 포함한 파일 그룹을 나머지 파티션이 사용하거나 NEXT USED 속성으로 표시하지 않는 한 이 인수는 해당 파일 그룹을 파티션 구성표에서 제거합니다. 병합된 파티션은 처음에 *boundary_value*를 포함하지 않았던 파일 그룹에 있습니다. *boundary_value*는 변수(사용자 정의 형식 변수 포함) 또는 함수(사용자 정의 함수 포함)를 참조할 수 있는 상수 식입니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 식을 참조할 수 없습니다. *boundary_value*는 해당 분할 열의 데이터 형식과 일치하거나 이 데이터 형식으로의 암시적 변환되어야 합니다. *boundary_value*는 암시적인 변환 중에 값의 크기 및 소수 자릿수가 해당 *input_parameter_type*과 일치하지 않는 방식으로 자를 수도 없습니다.  
  
> [!NOTE]  
>  columnstore 인덱스 관련 제한 사항: columnstore 인덱스가 포함된 두 개의 비어 있지 않은 파티션은 병합할 수 없습니다. 이 작업을 수행하기 전에 columnstore 인덱스를 삭제하거나 사용하지 않도록 설정해야 합니다.  
  
## <a name="best-practices"></a>모범 사례  
항상 파티션 범위의 양 끝에 빈 파티션을 유지합니다. 파티션을 양 끝에 유지하여 파티션 분할 및 파티션 병합으로 인해 데이터가 이동되지 않도록 합니다. 파티션 분할은 시작 부분에서 발생하고 파티션 병합은 끝 부분에서 발생합니다. 채워진 파티션은 분할되거나 병합되지 않도록 합니다. 채워진 파티션을 분할하거나 병합하는 것은 비효율적일 수 있습니다. 분할이나 병합으로 인해 로그가 네 배 더 생성될 수 있으며 잠금이 과도하게 발생할 수 있으므로 해당 작업은 비효율적일 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
ALTER PARTITION FUNCTION은 함수를 사용하는 테이블 및 인덱스를 단일 원자성 작업 내에서 다시 분할합니다. 그러나 이 작업은 오프라인 상태로 발생하며 재분할의 범위에 따라 많은 리소스가 필요할 수 있습니다.  
  
하나의 파티션을 둘로 나누거나 두 개의 파티션을 하나로 병합하는 데는 ALTER PARTITION FUNCTION만 사용합니다. 테이블을 분할하는 방법을 변경하려면(예를 들어 10개의 파티션을 5개로 변경) 다음 옵션을 실행합니다. 시스템 구성에 따라 해당 옵션의 리소스 사용량이 달라질 수 있습니다.  
  
-   필요한 파티션 함수를 사용하여 분할된 테이블을 새로 만듭니다. 그런 다음, INSERT INTO...SELECT FROM 문을 사용하여 이전 테이블의 데이터를 새 테이블에 삽입합니다.  
  
-   힙에 분할된 클러스터형 인덱스를 만듭니다.  
  
    > [!NOTE]  
    >  분할된 클러스터형 인덱스를 삭제하면 힙이 분할됩니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX 문에 DROP EXISTING = ON 절을 사용하여 기존의 분할 인덱스를 삭제하고 다시 작성합니다.  
  
-   ALTER PARTITION FUNCTION 문의 시퀀스를 실행합니다.  
  
ALTER PARTITION FUNCTION의 영향을 받는 모든 파일 그룹이 온라인 상태여야 합니다.  
  
파티션 함수를 사용하는 테이블에 비활성화된 클러스터형 인덱스가 있으면 ALTER PARTITION FUNCTION이 실패합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 파티션 함수 수정을 위한 복제 지원을 제공하지 않습니다. 게시 데이터베이스 내의 파티션 함수에 대한 변경은 구독 데이터베이스에 수동으로 적용해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
ALTER PARTITION FUNCTION을 실행하려면 다음 중 하나의 권한이 필요합니다.  
  
-   ALTER ANY DATASPACE 권한. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할 및 **db_owner** 및 **db_ddladmin** 고정 데이터베이스 역할의 멤버에게 부여됩니다.  
  
-   파티션 함수가 생성된 데이터베이스에 대한 CONTROL 또는 ALTER 권한  
  
-   파티션 함수가 생성된 데이터베이스의 서버에 대한 CONTROL SERVER 또는 ALTER ANY DATABASE 권한  
  
## <a name="examples"></a>예  
  
### <a name="a-splitting-a-partition-of-a-partitioned-table-or-index-into-two-partitions"></a>A. 분할 테이블 또는 인덱스의 파티션을 두 개의 파티션으로 분할  
다음 예에서는 테이블이나 인덱스를 4개의 파티션으로 분할하는 파티션 함수를 만듭니다. `ALTER PARTITION FUNCTION`은 파티션 중 하나를 둘로 분할하여 총 5개의 파티션을 만듭니다.  
  
```sql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Split the partition between boundary_values 100 and 1000  
--to create two partitions between boundary_values 100 and 500  
--and between boundary_values 500 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
SPLIT RANGE (500);  
```  
  
### <a name="b-merging-two-partitions-of-a-partitioned-table-into-one-partition"></a>B. 분할된 테이블의 두 개의 파티션을 하나의 파티션으로 병합  
다음 예에서는 위의 예와 같은 파티션 함수를 만든 다음 두 개의 파티션을 하나로 병합하여 총 3개의 파티션을 만드는 방법을 보여 줍니다.  
  
```sql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Merge the partitions between boundary_values 1 and 100  
--and between boundary_values 100 and 1000 to create one partition  
--between boundary_values 1 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
MERGE RANGE (100);  
```  
  
## <a name="see-also"></a>참고 항목  
[분할된 테이블 및 인덱스](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
[CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
[DROP PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
[CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
[ALTER PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
[DROP PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
[CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
[ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
[sys.partition_functions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
[sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md) [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
[sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
[sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
[sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
[sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
