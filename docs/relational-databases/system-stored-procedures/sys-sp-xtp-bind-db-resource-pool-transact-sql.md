---
title: sys.sp_xtp_bind_db_resource_pool (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_xtp_bind_db_resource_pool_TSQL
- sp_xtp_bind_db_resource_pool
- sys.sp_xtp_bind_db_resource_pool_TSQL
- sys.sp_xtp_bind_db_resource_pool
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xtp_bind_db_resource_pool
- sys.sp_xtp_bind_db_resource_pool
ms.assetid: c2a78073-626b-4159-996e-1808f6bfb6d2
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8bcac671ebd335be8e6f22a1385d0c038e61e365
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysspxtpbinddbresourcepool-transact-sql"></a>sys.sp_xtp_bind_db_resource_pool(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  지정된 리소스 풀에 지정된 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 데이터베이스를 바인딩합니다. `sys.sp_xtp_bind_db_resource_pool` 실행 전에 데이터베이스와 리소스 풀 모두 있어야 합니다.  
  
 이 시스템 프로시저는 resource_pool_name으로 식별되는 리소스 관리자와 database_name으로 식별되는 데이터베이스 사이의 바인딩을 만듭니다. 바인딩 시 메모리 최적화 개체가 데이터베이스에 있을 필요는 없습니다. 메모리 최적화 개체가 없을 경우 리소스 풀에서 메모리를 가져오지 않습니다. 이 바인딩은 아래에 설명된 바와 같이 리소스 관리자가 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 할당자에 의해 할당된 메모리를 관리하는 데 사용됩니다.  
  
 지정된 데이터베이스를 위한 바인딩이 이미 있는 경우 절차에서 오류를 반환합니다.  데이터베이스에 활성 바인딩이 여러 개 있을 수 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  
## <a name="syntax"></a>구문  
  
```sql  
sys.sp_xtp_bind_db_resource_pool 'database_name', 'resource_pool_name'  
```  
  
## <a name="arguments"></a>인수  
 database_name  
 기존 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 사용 데이터베이스의 이름입니다.  
  
 resource_pool_name  
 기존 리소스 풀의 이름입니다.  
  
## <a name="messages"></a>메시지  
 오류 발생 시 `sp_xtp_bind_db_resource_pool`에서 다음 메시지 중 하나를 반환합니다.  
  
 **데이터베이스가 존재 하지 않습니다.**  
 Database_name은 기존 데이터베이스를 참조해야 합니다. 지정된 ID의 데이터베이스가 없는 경우 다음 메시지가 반환됩니다.   
*데이터베이스 ID %d 존재 하지 않습니다.  이 바인딩에 대 한 올바른 데이터베이스 ID를 사용 하십시오.*  
  
```  
Msg 911, Level 16, State 18, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Database 'Hekaton_DB213' does not exist. Make sure that the name is entered correctly.  
```  
  
**데이터베이스는 시스템 데이터베이스**  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 시스템 데이터베이스에서 테이블을 만들 수 없습니다.  따라서 이러한 데이터베이스에 대해 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 메모리의 바인딩을 만들 수 없습니다.  다음 오류가 반환됩니다.  
*A s e _ %s 시스템 데이터베이스를 가리킵니다.  리소스 풀 사용자 데이터베이스에 바인딩될 수도 있습니다.*  
  
```  
Msg 41371, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Binding to a resource pool is not supported for system database 'master'. This operation can only be performed on a user database.  
```  
  
**리소스 풀이 없습니다.**  
 `sp_xtp_bind_db_resource_pool` 실행 전에 Resource_pool_name으로 식별되는 리소스 풀이 있어야 합니다.  지정된 ID의 풀이 없는 경우 다음 오류가 반환됩니다.  
*리소스 풀 %s 존재 하지 않습니다.  올바른 리소스 풀 이름을 입력 하십시오.*  
  
```  
Msg 41370, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Resource pool 'Pool_Hekaton' does not exist or resource governor has not been reconfigured.  
```  
  
**Pool_name 이라는 예약된 된 시스템 풀 참조**  
 풀 이름 "INTERNAL"과 "DEFAULT"는 시스템 풀용으로 예약되어 있습니다.  이들 중 하나에 데이터베이스를 명시적으로 바인딩할 수 없습니다.  시스템 풀 이름을 입력하면 다음 오류가 반환됩니다.  
*리소스 풀 %s 시스템 리소스 풀이입니다.  이 절차를 사용 하 여 데이터베이스에 시스템 리소스 풀을 명시적으로 바인딩할 수 있습니다.*  
  
```  
Msg 41373, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Database 'Hekaton_DB' cannot be explicitly bound to the resource pool 'internal'. A database can only be bound only to a user resource pool.  
```  
  
**데이터베이스가 이미 다른 리소스 풀에 바인딩된**  
 언제든지 단 하나의 리소스 풀에 데이터베이스를 바인딩할 수 있습니다. 리소스 풀에 대한 데이터베이스 바인딩은 명시적으로 제거해야 다른 풀에 바인딩할 수 있습니다. 참조 [sys.sp_xtp_unbind_db_resource_pool&#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md).  
*데이터베이스 %s 리소스 풀 %s 이미 바인딩되어 있습니다.  새 바인딩을 만들기 전에 했으면 바인딩을 해제 해야 합니다.*  
  
```  
Msg 41372, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 54  
Database 'Hekaton_DB' is currently bound to a resource pool. A database must be unbound before creating a new binding.  
```  
  
 성공 시 `sp_xtp_bind_db_resource_pool`에서 다음 메시지를 반환합니다.  
  
**바인딩 성공**  
 성공 시 SQL ERRORLOG에 기록되는 다음 성공 메시지가 반환됩니다  
*ID %d와 데이터베이스와 리소스 풀 id %d 사이 리소스 바인딩이 성공적으로 생성 되었습니다.*  
  
## <a name="examples"></a>예  
1.  다음 코드 예제에서는 리소스 풀 Pool_Hekaton에 데이터베이스 Hekaton_DB를 바인딩합니다.  
  
```sql  
sys.sp_xtp_bind_db_resource_pool N'Hekaton_DB', N'Pool_Hekaton'  
```  
 
 다음에 데이터베이스를 온라인 상태로 전환할 때 바인딩이 적용됩니다.  
 
 2. 확장 된 예제 위 일부 기본 검사를 포함 하는 예제입니다.  다음 실행 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]\:
 
```sql
DECLARE @resourcePool sysname = N'Pool_Hekaton';
DECLARE @database sysname = N'Hekaton_DB';

-- Check whether resource pool exists
IF NOT EXISTS (
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = @resourcePool
    )
BEGIN
    SELECT N'Resource pool "' + @resourcePool + N'" does not exist or resource governor has not been reconfigured.';
END
-- Check whether database is already bound to a resource pool
ELSE IF EXISTS (
    SELECT p.name
    FROM sys.databases d
    JOIN sys.resource_governor_resource_pools p
    ON d.resource_pool_id = p.pool_id
    WHERE d.name = @database
    )
BEGIN
    SELECT N'Database "' + @database + N'" is currently bound to resource pool "' + @resourcePool  + N'". A database must be unbound before creating a new binding.';
END
-- Bind resource pool to database.
ELSE BEGIN
    EXEC sp_xtp_bind_db_resource_pool @database, @resourcePool; 
END 
``` 
  
## <a name="requirements"></a>요구 사항  
  
-   `database_name`으로 지정된 데이터베이스와 `resource_pool_name`으로 지정된 리소스 풀 모두 바인딩하기 전에 있어야 합니다.  
  
-   CONTROL SERVER 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [메모리 액세스에 최적화된 테이블이 있는 데이터베이스를 리소스 풀에 바인딩](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_unbind_db_resource_pool&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)  
  
  
