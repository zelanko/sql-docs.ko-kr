---
title: ALTER PARTITION SCHEME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION SCHEME
- ALTER_PARTITION_SCHEME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ALTER PARTITION SCHEME statement
- partition schemes [SQL Server], modifying
- modifying partition schemes
- adding filegroups
- NEXT USED filegroups
ms.assetid: f01d6880-9800-4cfb-8d11-d4be21efc8ca
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 16b15945c8e6f56621516f16707d61be908e9972
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-partition-scheme-transact-sql"></a>ALTER PARTITION SCHEME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  파티션 구성표에 파일 그룹을 추가하거나 파티션 구성표의 NEXT USED 파일 그룹 지정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER PARTITION SCHEME partition_scheme_name   
NEXT USED [ filegroup_name ] [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *partition_scheme_name*  
 변경할 파티션 구성표의 이름입니다.  
  
 *filegroup_name*  
 파티션 구성표에서 NEXT USED로 표시할 파일 그룹을 지정합니다. 즉, 파일 그룹에 새 파티션을 사용 하 여 만든 수락할는 [ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md) 문.  
  
 파티션 구성표에서 파일 그룹 하나만 NEXT USED로 지정할 수 있습니다. 비어 있지 않은 파일 그룹을 지정할 수 있습니다. 경우 *filegroup_name* 지정 되어 있으므로 현재 NEXT USED 파일 그룹이 표시 *filegroup_name* NEXT USED로 표시 합니다. 경우 *filegroup_name* 를 지정 하 고 NEXT USED 속성을 포함 한 파일 이미 있으면 기존 파일 그룹에서 NEXT USED 속성이 전달 *filegroup_name*합니다.  
  
 경우 *filegroup_name* 지정 하지 않으면 NEXT USED 속성을 포함 한 파일 이미 있으면 해당 파일 그룹에 NEXT USED 파일 그룹이 되도록 NEXT USED 상태의 손실 및 *partition_scheme_name*.  
  
 경우 *filegroup_name* 를 지정 하지 않으면 가지 파일 그룹이 NEXT USED로 표시, ALTER PARTITION SCHEME에서 경고를 반환 합니다.  
  
## <a name="remarks"></a>주의  
 ALTER PARTITION SCHEME가 적용되는 모든 파일 그룹은 온라인 상태여야 합니다.  
  
## <a name="permissions"></a>Permissions  
 다음 권한을 사용하여 ALTER PARTITION SCHEME를 실행할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [DROP PARTITION scheme&#40; Transact SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION function&#40; Transact SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION function&#40; Transact SQL &#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_schemes &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
