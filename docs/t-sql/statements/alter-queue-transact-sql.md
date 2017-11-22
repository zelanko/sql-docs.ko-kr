---
title: ALTER QUEUE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2016
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
- ALTER_QUEUE_TSQL
- ALTER QUEUE
dev_langs: TSQL
helpviewer_keywords:
- number of queue readers
- modifying queues
- ALTER QUEUE statement
- queue readers [SQL Server]
- queues [Service Broker], modifying
- unavailable queues [SQL Server]
- activation stored procedures [Service Broker]
ms.assetid: d54aa325-8761-4cd4-8da7-acf33df12296
caps.latest.revision: "49"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2774da9a0a75c4645a4bd64237ec99a7cf92d771
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="alter-queue-transact-sql"></a>ALTER QUEUE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  큐의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER QUEUE <object>   
   queue_settings  
   | queue_action  
[ ; ]  
  
<object> : :=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]  
        queue_name  
}   
  
<queue_settings> : :=  
WITH  
   [ STATUS = { ON | OFF } [ , ] ]  
   [ RETENTION = { ON | OFF } [ , ] ]  
   [ ACTIVATION (  
       { [ STATUS = { ON | OFF } [ , ] ]   
         [ PROCEDURE_NAME = <procedure> [ , ] ]  
         [ MAX_QUEUE_READERS = max_readers [ , ] ]  
         [ EXECUTE AS { SELF | 'user_name'  | OWNER } ]  
       |  DROP }  
          ) [ , ]]  
         [ POISON_MESSAGE_HANDLING (  
          STATUS = { ON | OFF } )  
         ]   
  
<queue_action> : :=  
   REBUILD [ WITH <query_rebuild_options> ]  
   | REORGANIZE [ WITH (LOB_COMPACTION = { ON | OFF } ) ]  
   | MOVE TO { file_group | "default" }  
  
<procedure> : :=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]  
        stored_procedure_name  
}  
  
<queue_rebuild_options> : :=  
{  
   ( MAXDOP = max_degree_of_parallelism )  
}  
  
```  
  
## <a name="arguments"></a>인수  
 *a s e _* (개체)  
 변경할 큐가 포함된 데이터베이스의 이름입니다. No *database_name* 현재 데이터베이스에는 기본적으로이 제공 됩니다.  
  
 *schema_name* (개체)  
 새로운 큐가 속할 스키마 이름입니다. No *schema_name* 제공 현재 사용자에 대 한 기본 스키마로 기본 설정 됩니다.  
  
 *queue_name*  
 변경할 큐의 이름입니다.  
  
 STATUS (Queue)  
 큐의 사용 가능 여부(ON 또는 OFF)를 지정합니다. 큐를 사용할 수 없을 경우 큐에서 메시지를 추가하거나 제거할 수 없습니다.  
  
 RETENTION  
 큐에 대한 보존 설정을 지정합니다. RETENTION = ON인 경우 이 큐의 대화에서 주고받은 모든 메시지가 대화가 끝날 때까지 큐에 남아 있습니다. 그러므로 오류가 발생할 때 보정 트랜잭션을 수행하거나 감사할 목적으로 메시지를 유지할 수 있습니다.  
  
> [!NOTE]  
>  RETENTION = ON으로 설정하면 성능이 저하될 수 있습니다. 응용 프로그램의 서비스 수준 계약을 충족시켜야 할 경우에만 이 설정을 사용해야 합니다.  
  
 ACTIVATION  
 이 큐에 도착한 메시지를 처리하기 위해 활성화된 저장 프로시저에 대한 정보를 지정합니다.  
  
 STATUS (Activation)  
 큐에서 저장 프로시저의 활성화 여부를 지정합니다. STATUS = ON이면 현재 실행 중인 프로시저 수가 MAX_QUEUE_READERS보다 작고, 큐에 도착하는 메시지가 저장 프로시저의 메시지 수신 속도보다 빠른 경우 큐에서 PROCEDURE_NAME에 지정된 저장 프로시저를 시작합니다. STATUS = OFF이면 큐에서 저장 프로시저를 활성화하지 않습니다.  
  
 REBUILD [WITH \<queue_rebuild_options >]  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 큐 내부 테이블의 모든 인덱스 다시 작성합니다. 과부하로 인해 조각화 문제가 발생 하는 경우이 기능을 사용 합니다. MAXDOP만 지원 되는 큐 rebuild 옵션입니다. 다시 작성은 항상 오프 라인 작업입니다.  
  
 다시 구성 [와 (LOB_COMPACTION = {ON | OFF})]  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 큐 내부 테이블의 모든 인덱스 다시 구성 합니다.   
큐에 REORGANIZE 사용자 테이블에 인덱스 다시 구성, 달리 항상 큐에서 페이지 수준 잠금이 비활성화 명시적으로 하기 때문에 오프 라인 작업으로 수행 됩니다.  
  
> [!TIP]  
>  인덱스 조각화에 대 한 일반적인 지침에 대 한 조각화가 30% 5% 사이 이면 인덱스를 재구성 합니다. 조각화가 30% 보다 이면 인덱스를 다시 작성 합니다. 그러나이 숫자는 사용자 환경에 대 한 시작 점으로 일반적인 지침에 대해서만. 사용 하 여 인덱스 조각화의 양은 확인 하려면 [sys.dm_db_index_physical_stats&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) -G 예제 예제를 보려면 해당 문서를 참조 하십시오.  
  
 MOVE TO { *file_group* | "default"을 (를)  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 사용자가 지정한 파일 그룹의 큐 내부 테이블 (인덱스)으로 이동합니다.  새 파일 그룹이 읽기 전용으로 설정 되지 않아야 합니다.  
  
 PROCEDURE_NAME = \<프로시저 >  
 큐에 처리할 메시지가 포함된 경우 활성화할 저장 프로시저의 이름을 지정합니다. 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자여야 합니다.  
  
 *a s e _* (프로시저)  
 저장 프로시저가 포함된 데이터베이스의 이름입니다.  
  
 *schema_name* (프로시저)  
 저장 프로시저를 소유한 스키마의 이름입니다.  
  
 *stored_procedure_name*  
 저장 프로시저의 이름입니다.  
  
 MAX_QUEUE_READERS =*max_reader*  
 큐에서 동시에 시작하는 활성화 저장 프로시저의 최대 인스턴스 수를 지정합니다. 값 *max_readers* 0에서 32767 사이의 숫자 여야 합니다.  
  
 EXECUTE AS  
 활성화 저장 프로시저를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 사용자 계정을 지정합니다. 큐에서 저장 프로시저를 시작할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 사용자의 권한을 확인할 수 있어야 합니다. Windows 도메인 사용자의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 도메인에 연결해야 하며 프로시저가 활성화되거나 활성화가 실패할 때 데이터베이스 엔진에서 지정한 사용자의 권한을 확인할 수 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자의 경우에는 서버에서 항상 권한을 확인할 수 있습니다.  
  
 SELF  
 저장 프로시저가 현재 사용자로 실행되도록 지정합니다(이 ALTER QUEUE 문을 실행하는 데이터베이스 보안 주체).  
  
 '*user_name*'  
 저장 프로시저가 실행되는 사용자 이름입니다. *user_name* 은 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 지정 된 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자입니다. 현재 사용자에 대 한 IMPERSONATE 권한이 있어야 합니다.는 *user_name* 지정 합니다.  
  
 OWNER  
 저장 프로시저가 큐의 소유자로 실행되도록 지정합니다.  
  
 DROP  
 큐와 연관된 모든 활성화 정보를 삭제합니다.  
  
 POISON_MESSAGE_HANDLING  
 포이즌 메시지 처리를 사용하는지 여부를 지정합니다. 기본값은 ON입니다.  
  
 포이즌 메시지 처리가 OFF로 설정된 큐는 트랜잭션 롤백이 연속으로 5회 발생하더라도 비활성화되지 않습니다. 이렇게 하면 응용 프로그램에서 사용자 지정 포이즌 메시지 처리 시스템을 정의할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 활성화 저장 프로시저가 지정된 큐에 메시지가 포함된 경우 활성화 상태를 OFF에서 ON으로 변경하면 활성화 저장 프로시저가 즉시 활성화됩니다. 활성화 상태를 ON에서 OFF로 변경하면 Broker에서 저장 프로시저 인스턴스를 활성화하는 것을 중지하지만 현재 실행 중인 저장 프로시저 인스턴스는 중지하지 않습니다.  
  
 큐를 변경하여 활성화 저장 프로시저를 추가해도 큐의 활성화 상태는 변경되지 않습니다. 또한 큐의 활성화 저장 프로시저를 변경해도 현재 실행 중인 활성화 저장 프로시저 인스턴스에는 영향을 주지 않습니다.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서는 활성화 프로세스의 일부로 큐에 대한 최대 큐 판독기 수를 확인합니다. 그러므로 큐를 변경하여 최대 큐 판독기 수를 늘리면 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 즉시 더 많은 활성화 저장 프로시저 인스턴스를 시작할 수 있습니다. 또한 큐를 변경하여 최대 큐 판독기 수를 줄여도 현재 실행 중인 활성화 저장 프로시저 인스턴스에는 영향을 주지 않습니다. 그러나 활성화 저장 프로시저의 인스턴스 수가 구성된 최대 수 아래로 떨어질 때까지 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 저장 프로시저의 새 인스턴스를 시작하지 않습니다.  
  
 큐를 사용할 수 없는 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 데이터베이스 전송 큐에서 큐를 사용하는 서비스에 대한 메시지를 보유합니다. [sys.transmission_queue](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md) 카탈로그 뷰에서 전송 큐 보기를 제공 합니다.  
  
 RECEIVE 문 또는 GET CONVERSATION GROUP 문에서 사용할 수 없는 큐를 지정하는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 오류로 인해 이 문은 실패합니다.  
  
## <a name="permissions"></a>Permissions  
 큐를 변경할 수 있는 권한은 기본적으로 큐의 소유자, db_ddladmin 또는 db_owner 고정 데이터베이스 역할의 멤버 및 sysadmin 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-making-a-queue-unavailable"></a>1. 큐를 사용할 수 없게 설정  
 다음 예에서는 `ExpenseQueue` 큐에서 메시지를 받을 수 없도록 설정합니다.  
  
```  
ALTER QUEUE ExpenseQueue WITH STATUS = OFF ;  
```  
  
### <a name="b-changing-the-activation-stored-procedure"></a>2. 활성화 저장 프로시저 변경  
 다음 예에서는 큐가 시작하는 저장 프로시저를 변경합니다. 이 저장 프로시저는 `ALTER QUEUE` 문을 실행한 사용자로 실행됩니다.  
  
```  
ALTER QUEUE ExpenseQueue  
    WITH ACTIVATION (  
        PROCEDURE_NAME = new_stored_proc,  
        EXECUTE AS SELF) ;  
```  
  
### <a name="c-changing-the-number-of-queue-readers"></a>3. 큐 판독기 수 변경  
 다음 예에서는 이 큐에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 시작하는 저장 프로시저 인스턴스의 최대 수를 `7`로 설정합니다.  
  
```  
ALTER QUEUE ExpenseQueue WITH ACTIVATION (MAX_QUEUE_READERS = 7) ;  
```  
  
### <a name="d-changing-the-activation-stored-procedure-and-the-execute-as-account"></a>4. 활성화 저장 프로시저 및 EXECUTE AS 계정 변경  
 다음 예에서는 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 시작하는 저장 프로시저를 변경합니다. 이 저장 프로시저는 `SecurityAccount` 사용자로 실행됩니다.  
  
```  
ALTER QUEUE ExpenseQueue  
    WITH ACTIVATION (  
        PROCEDURE_NAME = AdventureWorks2012.dbo.new_stored_proc ,  
        EXECUTE AS 'SecurityAccount') ;  
```  
  
### <a name="e-setting-the-queue-to-retain-messages"></a>5. 메시지를 유지하도록 큐 설정  
 다음 예에서는 메시지를 유지하도록 큐를 설정합니다. 이 큐에는 메시지가 포함된 대화가 종료될 때까지 이 큐를 사용하는 서비스와 주고 받은 모든 메시지가 유지됩니다.  
  
```  
ALTER QUEUE ExpenseQueue WITH RETENTION = ON ;  
```  
  
### <a name="f-removing-activation-from-a-queue"></a>6. 큐에서 활성화 제거  
 다음 예에서는 큐에서 모든 활성화 정보를 제거합니다.  
  
```  
ALTER QUEUE ExpenseQueue WITH ACTIVATION (DROP) ;  
```  
  
### <a name="g-rebuilding-queue-indexes"></a>7. 큐 인덱스 다시 작성  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 다음 예에서는 큐 인덱스 다시 작성  
  
```  
ALTER QUEUE ExpenseQueue REBUILD WITH (MAXDOP = 2)   
```  
  
### <a name="h-reorganizing-queue-indexes"></a>8. 큐 인덱스 다시 구성  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 다음 예에서는 큐 인덱스를 다시 구성  
  
```  
ALTER QUEUE ExpenseQueue REORGANIZE   
```  
  
### <a name="i-moving-queue-internal-table-to-another-filegroup"></a>I: 큐 내부 테이블 다른 파일 그룹으로 이동  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
ALTER QUEUE ExpenseQueue MOVE TO [NewFilegroup]   
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [DROP queue&#40; Transact SQL &#41;](../../t-sql/statements/drop-queue-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
  
