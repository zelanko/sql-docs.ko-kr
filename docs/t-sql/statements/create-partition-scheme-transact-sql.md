---
title: "파티션 구성표 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE PARTITION SCHEME
- SCHEME
- PARTITION SCHEME
- CREATE_PARTITION_SCHEME_TSQL
- SCHEME_TSQL
- PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- partitioned indexes [SQL Server], schemes
- partitioned tables [SQL Server], schemes
- CREATE PARTITION SCHEME statement
- partition schemes [SQL Server], creating
- filegroups [SQL Server], partitions
- partitioned indexes [SQL Server], filegroups
- partitioned tables [SQL Server], filegroups
- mapping partitions [SQL Server]
ms.assetid: 5b21c53a-b4f4-4988-89a2-801f512126e4
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13bd8b623604f8bfe93dcf4483c65be14f43f003
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-partition-scheme-transact-sql"></a>CREATE PARTITION SCHEME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 분할된 테이블 또는 인덱스의 파티션을 파일 그룹에 매핑하는 구성표를 만듭니다. 분할된 테이블 또는 인덱스의 파티션 수 및 도메인은 파티션 함수에서 결정됩니다. 파티션 함수는 먼저 만들어야는 [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md) 파티션 구성표를 만들기 전에 문을 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE PARTITION SCHEME partition_scheme_name  
AS PARTITION partition_function_name  
[ ALL ] TO ( { file_group_name | [ PRIMARY ] } [ ,...n ] )  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *partition_scheme_name*  
 파티션 구성표의 이름입니다. 파티션 구성표 이름은 데이터베이스 내에서 고유 해야 하며 규칙을 따라야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 *partition_function_name*  
 파티션 구성표를 사용하는 파티션 함수의 이름입니다. 파티션 함수로 생성한 파티션은 파티션 구성표에서 지정한 파일 그룹으로 매핑됩니다. *partition_function_name* 데이터베이스에 이미 있어야 합니다. 단일 파티션에는 FILESTREAM 파일 그룹과 FILESTREAM이 아닌 파일 그룹이 둘 다 포함될 수 없습니다.  
  
 ALL  
 모든 파티션이에 제공 된 파일 그룹에 매핑하는 지정 *file_group_name*, 또는 주 파일 그룹에 경우 **[**기본**]** 지정 됩니다. ALL을 지정 하는 경우 하나의 *file_group_name* 지정할 수 있습니다.  
  
 *file_group_name* | **[** 기본 **]** [ **,***...n*]  
 지정한 파티션을 보유할 파일 그룹의 이름을 지정 *partition_function_name*합니다. *file_group_name* 데이터베이스에 이미 있어야 합니다.  
  
 경우 **[**기본**]** 를 지정 된 파티션은 주 파일 그룹에 저장 됩니다. ALL을 지정 하는 경우 하나의 *file_group_name* 지정할 수 있습니다. 시작 하 여 파티션을 1에 나열 된 파일 그룹의 순서로 파일 그룹에 할당 [**,***...n*]. 동일한 *file_group_name* 에서 여러 번 지정할 수 있습니다 [**,***...n*]. 경우  *n*  에 지정 된 파티션 수를 보유 하기에 부족 *partition_function_name*, CREATE PARTITION SCHEME 실패 오류가 발생 합니다.  
  
 경우 *partition_function_name* 생성 파일 그룹 보다 적은 파티션을는 첫 번째 할당 되지 않은 파일 그룹이 NEXT USED로 표시 된 및 정보 메시지가 NEXT USED 파일 그룹 이름 지정을 표시 합니다. ALL을 지정 하는 경우 유일 *file_group_name* 이 NEXT USED 속성을 유지 관리 *partition_function_name*합니다. ALTER PARTITION FUNCTION 문에서 파티션을 생성한 경우 NEXT USED 파일 그룹이 추가 파티션을 받습니다. 할당되지 않은 파일 그룹을 추가로 만들어 새 파티션을 보유하려면 ALTER PARTITION SCHEME을 사용하십시오.  
  
 주 파일 그룹을 지정 하는 경우 *file_group_name* [1**,***...n*]에서 같이 구분 해야 **[**주**]** 키워드 이기 때문에, 합니다.  
  
 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]에는 PRIMARY만 사용할 수 있습니다. E 아래 예제를 참조 하십시오. 
  
## <a name="permissions"></a>Permissions  
 CREATE PARTITION SCHEME을 실행하는 데 필요한 권한은 다음과 같습니다.  
  
-   ALTER ANY DATASPACE 권한. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할 및 **db_owner** 및 **db_ddladmin** 고정 데이터베이스 역할의 멤버에게 부여됩니다.  
  
-   파티션 구성표가 생성된 데이터베이스에 대한 CONTROL 또는 ALTER 권한  
  
-   파티션 구성표가 생성된 데이터베이스의 서버에 대한 CONTROL SERVER 또는 ALTER ANY DATABASE 권한  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-partition-scheme-that-maps-each-partition-to-a-different-filegroup"></a>1. 각 파티션을 다른 파일 그룹에 매핑하는 파티션 구성표 만들기  
 다음 예에서는 테이블이나 인덱스를 4개의 파티션으로 분할하는 파티션 함수를 만듭니다. 4개의 파티션 각각을 보유하도록 파일 그룹을 지정하는 파티션 구성표를 만듭니다. 이 예에서는 데이터베이스에 이미 파일 그룹이 있다고 가정합니다.  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
TO (test1fg, test2fg, test3fg, test4fg);  
```  
  
 파티션 함수를 사용 하는 테이블의 파티션을 `myRangePF1` 분할 열에 **col1** 다음 표와 같이 할당 됩니다.  
  
||||||  
|-|-|-|-|-|  
|**파일 그룹**|`test1fg`|`test2fg`|`test3fg`|`test4fg`|  
|**파티션**|1.|2|3|4|  
|**값**|**col1** <= `1`|**col1**  >  `1` AND **col1** <= `100`|**col1**  >  `100` AND **col1** <= `1000`|**col1** > `1000`|  
  
### <a name="b-creating-a-partition-scheme-that-maps-multiple-partitions-to-the-same-filegroup"></a>2. 여러 파티션을 같은 파일 그룹에 매핑하는 파티션 구성표 만들기  
 모든 파티션을 같은 파일 그룹에 매핑하는 경우 ALL 키워드를 사용하십시오. 그러나 모든 파티션이 아니라 여러 개의 일부 파티션을 같은 파일 그룹에 매핑하는 경우 다음 예와 같이 파일 그룹 이름을 반복해야 합니다.  
  
```  
CREATE PARTITION FUNCTION myRangePF2 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS2  
AS PARTITION myRangePF2  
TO ( test1fg, test1fg, test1fg, test2fg );  
```  
  
 파티션 함수를 사용 하는 테이블의 파티션을 `myRangePF2` 분할 열에 **col1** 다음 표와 같이 할당 됩니다.  
  
||||||  
|-|-|-|-|-|  
|**파일 그룹**|`test1fg`|`test1fg`|`test1fg`|`test2fg`|  
|**파티션**|1.|2|3|4|  
|**값**|**col1** <= `1`|**col1** > 1 AND **col1** <= `100`|**col1**  >  `100` AND **col1** <= `1000`|**col1** > `1000`|  
  
### <a name="c-creating-a-partition-scheme-that-maps-all-partitions-to-the-same-filegroup"></a>3. 모든 파티션을 같은 파일 그룹에 매핑하는 파티션 구성표 만들기  
 다음 예에서는 앞의 예와 같은 파티션 함수를 만들고 모든 파티션을 같은 파일 그룹에 매핑하는 파티션 구성표를 만드는 방법을 보여 줍니다.  
  
```  
CREATE PARTITION FUNCTION myRangePF3 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS3  
AS PARTITION myRangePF3  
ALL TO ( test1fg );  
```  
  
### <a name="d-creating-a-partition-scheme-that-specifies-a-next-used-filegroup"></a>4. 'NEXT USED' 파일 그룹을 지정하는 파티션 구성표 만들기  
 다음 예에서는 앞의 예와 같은 파티션 함수를 만들고 연관된 파티션 함수가 생성한 파티션보다 많은 파일 그룹을 나열하는 파티션 구성표를 만드는 방법을 보여 줍니다.  
  
```  
CREATE PARTITION FUNCTION myRangePF4 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS4  
AS PARTITION myRangePF4  
TO (test1fg, test2fg, test3fg, test4fg, test5fg)  
```  
  
 문을 실행하면 다음 메시지가 반환됩니다.  
  
파티션 구성표 'myRangePS4' 성공적으로 만들어졌습니다. 'test5fg' 파티션 구성표 'myRangePS4'에 다음 사용 되는 파일 그룹으로 표시 됩니다.  
  
  
 파티션을 추가하도록 `myRangePF4` 파티션 함수를 변경한 경우 `test5fg` 파일 그룹이 새로 만들어진 파티션을 받습니다.  

### <a name="e-creating-a-partition-schema-only-on-primary---only-primary-is-supported-for-includesqldbesaincludessqldbesa-mdmd"></a>5. 에 파티션 스키마를 만드는 기본-기본을 사용할 수[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]

 다음 예에서는 테이블이나 인덱스를 4개의 파티션으로 분할하는 파티션 함수를 만듭니다. 파티션 구성표 모든 파티션은 주 파일 그룹에 생성 되어 있음을 지정 하는 만들어집니다.  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
ALL TO ( [PRIMARY] );  
```
   
## <a name="see-also"></a>관련 항목:  
 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION scheme&#40; Transact SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [DROP PARTITION scheme&#40; Transact SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [분할 된 테이블 및 인덱스 만들기](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)   
 [sys.partition_schemes &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  

