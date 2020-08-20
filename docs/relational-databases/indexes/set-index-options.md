---
description: 인덱스 옵션 설정
title: 인덱스 옵션 설정 | Microsoft 문서
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- ALLOW_ROW_LOCKS option
- SORT_IN_TEMPDB option
- DROP_EXISTING clause
- large data, indexes
- PAD_INDEX
- STATISTICS_NORECOMPUTE
- MAXDOP index option, setting
- index options [SQL Server]
- MAXDOP index option
- IGNORE_DUP_KEY option
- ALLOW_PAGE_LOCKS option
- OPTIMIZE_FOR_SEQUENTIAL_KEY option
- ONLINE
ms.assetid: 7969af33-e94c-41f7-ab89-9d9a2747cd5c
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1427a47837063db4fd617c8489d99a3ab7927d15
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499392"
---
# <a name="set-index-options"></a>인덱스 옵션 설정

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 인덱스 속성을 수정하는 방법에 대해 설명합니다.

 **문서 내용**

- **시작하기 전 주의 사항:**

   [제한 사항](#Restrictions)

   [보안](#Security)

- **인덱스 속성을 수정하려면:**

   [SQL Server Management Studio](#SSMSProcedure)

   [Transact-SQL](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에

### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항

- ALLOW_PAGE_LOCKS, ALLOW_ROW_LOCKS, IGNORE_DUP_KEY 및 STATISTICS_NORECOMPUTE 옵션은 ALTER INDEX 문에서 SET 절을 사용하면 즉시 인덱스에 적용됩니다.(###)
- PAD_INDEX, FILLFACTOR, SORT_IN_TEMPDB, IGNORE_DUP_KEY, STATISTICS_NORECOMPUTE, ONLINE, ALLOW_ROW_LOCKS, ALLOW_PAGE_LOCKS, MAXDOP 및 DROP_EXISTING(CREATE INDEX의 경우에만) 옵션은 ALTER INDEX REBUILD 또는 CREATE INDEX WITH DROP_EXISTING 중 하나를 사용하여 인덱스를 다시 작성할 때 설정할 수 있습니다.

### <a name="security"></a><a name="Security"></a> 보안

#### <a name="permissions"></a><a name="Permissions"></a> 권한

테이블이나 뷰에 대한 ALTER 권한이 필요합니다.

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용

### <a name="to-modify-the-properties-of-an-index-in-table-designer"></a>테이블 디자이너에서 인덱스 속성을 수정하려면

1. 개체 탐색기에서 더하기 기호를 클릭하여 인덱스 속성을 수정할 테이블이 포함된 데이터베이스를 확장합니다.
2. 더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.
3. 인덱스 속성을 수정할 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.
4. **테이블 디자이너** 메뉴에서 **인덱스/키**를 클릭합니다.
5. 수정할 인덱스를 선택합니다. 주 표에 속성이 표시됩니다.
6. 속성의 설정을 변경하여 인덱스를 사용자 지정합니다.
7. **닫기**를 클릭합니다.
8. **파일** 메뉴에서 _table_name_**저장**을 선택합니다.

### <a name="to-modify-the-properties-of-an-index-in-object-explorer"></a>개체 탐색기에서 인덱스 속성을 수정하려면

1. 개체 탐색기에서 더하기 기호를 클릭하여 인덱스 속성을 수정할 테이블이 포함된 데이터베이스를 확장합니다.
2. 더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.
3. 더하기 기호를 클릭하여 인덱스 속성을 수정할 테이블을 확장합니다.
4. 더하기 기호를 클릭하여 **인덱스** 폴더를 확장합니다.
5. 속성을 수정할 인덱스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.
6. **페이지 선택**아래에서 **옵션**을 선택합니다.
7. 속성의 설정을 변경하여 인덱스를 사용자 지정합니다.
8. 인덱스 열을 추가 또는 제거하거나 그 위치를 변경하려면 **인덱스 속성 -** _index_name_ 대화 상자의 **일반** 페이지를 선택합니다. 자세한 내용은 [Index Properties F1 Help](../../relational-databases/indexes/index-properties-f1-help.md)를 참조하세요.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용

### <a name="to-see-the-properties-of-all-the-indexes-in-a-table"></a>테이블에 있는 모든 인덱스의 속성을 보려면

다음 예제에서는 AdventureWorks 데이터베이스에서 테이블에 있는 모든 인덱스의 속성을 보여 줍니다.

```sql
SELECT i.name AS index_name
   , i.type_desc
   , i.is_unique
   , ds.type_desc AS filegroup_or_partition_scheme
   , ds.name AS filegroup_or_partition_scheme_name
   , i.ignore_dup_key
   , i.is_primary_key
   , i.is_unique_constraint
   , i.fill_factor
   , i.is_padded
   , i.is_disabled
   , i.allow_row_locks
   , i.allow_page_locks
   , i.has_filter
   , i.filter_definition
FROM sys.indexes AS i
   INNER JOIN sys.data_spaces AS ds
      ON i.data_space_id = ds.data_space_id
   WHERE is_hypothetical = 0 AND i.index_id <> 0
       AND i.object_id = OBJECT_ID('HumanResources.Employee')
;
```

#### <a name="to-set-the-properties-of-an-index"></a>인덱스의 속성을 설정하려면

다음 예제에서는 AdventureWorks 데이터베이스에서 인덱스의 속성을 설정합니다.

[!code-sql[IndexDDL#AlterIndex4](../../relational-databases/indexes/codesnippet/tsql/set-index-options_1.sql)]

[!code-sql[IndexDDL#AlterIndex2](../../relational-databases/indexes/codesnippet/tsql/set-index-options_2.sql)]

자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.
