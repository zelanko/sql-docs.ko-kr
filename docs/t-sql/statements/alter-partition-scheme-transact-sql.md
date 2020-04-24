---
title: ALTER PARTITION SCHEME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION SCHEME
- ALTER_PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PARTITION SCHEME statement
- partition schemes [SQL Server], modifying
- modifying partition schemes
- adding filegroups
- NEXT USED filegroups
ms.assetid: f01d6880-9800-4cfb-8d11-d4be21efc8ca
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c701ad852eb7c33dbf2721be765d2df9fe36f1cd
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81627283"
---
# <a name="alter-partition-scheme-transact-sql"></a>ALTER PARTITION SCHEME(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  파티션 구성표에 파일 그룹을 추가하거나 파티션 구성표의 NEXT USED 파일 그룹 지정을 변경합니다. 

>[!NOTE]
>Azure SQL Database에서는 기본 파일 그룹만 지원됩니다.  
  
 ![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
ALTER PARTITION SCHEME partition_scheme_name   
NEXT USED [ filegroup_name ] [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *partition_scheme_name*  
 변경할 파티션 구성표의 이름입니다.  
  
 *filegroup_name*  
 파티션 구성표에서 NEXT USED로 표시할 파일 그룹을 지정합니다. 즉, [ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md) 문을 사용하여 만들어지는 새 파티션에 해당 파일 그룹이 적용됩니다.  
  
 파티션 구성표에서 파일 그룹 하나만 NEXT USED로 지정할 수 있습니다. 비어 있지 않은 파일 그룹을 지정할 수 있습니다. *filegroup_name*이 지정되고 현재 NEXT USED로 표시된 파일 그룹이 없는 경우 *filegroup_name*이 NEXT USED로 표시됩니다. *filegroup_name*이 지정되고 NEXT USED 속성이 있는 파일 그룹이 이미 있다면 기존 파일 그룹에서 *filegroup_name*으로 NEXT USED 속성이 전달됩니다.  
  
 *filegroup_name*이 지정되지 않았고 NEXT USED 속성이 있는 파일 그룹이 이미 있다면 해당 파일 그룹의 NEXT USED 상태가 상실되어 *partition_scheme_name*에는 NEXT USED 파일 그룹이 없는 상태가 됩니다.  
  
 *filegroup_name*이 지정되지 않았고 NEXT USED로 표시된 파일 그룹이 없다면 ALTER PARTITION SCHEME에서 경고를 반환합니다.  
  
## <a name="remarks"></a>설명  
 ALTER PARTITION SCHEME가 적용되는 모든 파일 그룹은 온라인 상태여야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 다음 사용 권한을 통해 ALTER PARTITION SCHEME을 실행할 수 있습니다.  
  
-   ALTER ANY DATASPACE 권한. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할 및 **db_owner** 및 **db_ddladmin** 고정 데이터베이스 역할의 멤버에게 부여됩니다.  
  
-   파티션 구성표가 생성된 데이터베이스에 대한 CONTROL 또는 ALTER 권한  
  
-   파티션 구성표가 생성된 데이터베이스의 서버에 대한 CONTROL SERVER 또는 ALTER ANY DATABASE 권한  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스에 `MyRangePS1` 파티션 구성표와 `test5fg` 파일 그룹이 있다고 가정합니다.  
  
```  
ALTER PARTITION SCHEME MyRangePS1  
NEXT USED test5fg;  
```  
  
 `test5fg` 파일 그룹은 ALTER PARTITION FUNCTION 문의 결과로 분할된 테이블이나 인덱스의 추가 파티션을 받습니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_schemes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
