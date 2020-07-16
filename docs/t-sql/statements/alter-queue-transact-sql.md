---
title: ALTER QUEUE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_QUEUE_TSQL
- ALTER QUEUE
dev_langs:
- TSQL
helpviewer_keywords:
- number of queue readers
- modifying queues
- ALTER QUEUE statement
- queue readers [SQL Server]
- queues [Service Broker], modifying
- unavailable queues [SQL Server]
- activation stored procedures [Service Broker]
ms.assetid: d54aa325-8761-4cd4-8da7-acf33df12296
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e7856a54070b58f6a834dd5a65b18b58e9667682
ms.sourcegitcommit: b2ab989264dd9d23c184f43fff2ec8966793a727
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86381187"
---
# <a name="alter-queue-transact-sql"></a>ALTER QUEUE(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  큐의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ALTER QUEUE <object>   
   queue_settings  
   | queue_action  
[ ; ]  
  
<object> : :=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }
  
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
{ database_name.schema_name.stored_procedure_name | schema_name.stored_procedure_name | stored_procedure_name }
  
<queue_rebuild_options> : :=  
{  
   ( MAXDOP = max_degree_of_parallelism )  
}  
  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *database_name*(개체)  
 변경할 큐가 포함된 데이터베이스의 이름입니다. *database_name*을 제공하지 않으면 기본값은 현재 데이터베이스입니다.  
  
 *schema_name*(개체)  
 새로운 큐가 속할 스키마 이름입니다. *schema_name*을 제공하지 않으면 기본값은 현재 사용자의 기본 스키마입니다.  
  
 *queue_name*  
 변경할 큐의 이름입니다.  
  
 STATUS (Queue)  
 큐의 사용 가능 여부(ON 또는 OFF)를 지정합니다. 큐를 사용할 수 없을 경우 큐에서 메시지를 추가하거나 제거할 수 없습니다.  
  
 RETENTION  
 큐에 대한 보존 설정을 지정합니다. RETENTION = ON인 경우 이 큐의 대화에서 주고받은 모든 메시지가 대화가 끝날 때까지 큐에 남아 있습니다. 그러므로 오류가 발생할 때 보정 트랜잭션을 수행하거나 감사할 목적으로 메시지를 유지할 수 있습니다.  
  
> [!NOTE]  
>  RETENTION = ON으로 설정하면 성능이 저하될 수 있습니다. 애플리케이션의 서비스 수준 계약을 충족시켜야 할 경우에만 이 설정을 사용해야 합니다.  
  
 ACTIVATION  
 이 큐에 도착한 메시지를 처리하기 위해 활성화된 저장 프로시저에 대한 정보를 지정합니다.  
  
 STATUS (Activation)  
 큐에서 저장 프로시저의 활성화 여부를 지정합니다. STATUS = ON이면 현재 실행 중인 프로시저 수가 MAX_QUEUE_READERS보다 작고, 큐에 도착하는 메시지가 저장 프로시저의 메시지 수신 속도보다 빠른 경우 큐에서 PROCEDURE_NAME에 지정된 저장 프로시저를 시작합니다. STATUS = OFF이면 큐에서 저장 프로시저를 활성화하지 않습니다.  
  
 REBUILD [ WITH \<queue_rebuild_options> ]  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상  
  
 큐 내부 테이블의 모든 인덱스를 다시 작성합니다. 과부하로 인해 조각화 문제가 발생하면 이 기능을 사용합니다. 지원되는 큐 다시 작성 옵션은 MAXDOP뿐입니다. REBUILD는 항상 오프라인 작업입니다.  
  
 REORGANIZE [ WITH ( LOB_COMPACTION = { ON | OFF } ) ]  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상  
  
 큐 내부 테이블의 모든 인덱스를 다시 구성합니다.   
사용자 테이블에 대한 REORGANIZE와 달리 큐에 대한 REORGANIZE는 큐에서 페이지 수준 잠금이 명시적으로 비활성화되기 때문에 항상 오프라인 작업으로 수행됩니다.  
  
> [!TIP]  
>  인덱스 조각화와 관련된 일반적인 지침은 조각화가 5%~30% 사이이면 인덱스를 다시 구성합니다. 조각화가 30%를 초과하면 인덱스를 다시 작성합니다. 하지만 이러한 숫자는 환경에 대한 시작점으로 일반적인 지침일뿐입니다. 인덱스 조각화의 양을 결정하려면 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)를 사용하세요 예제는 이 문서의 예제 G를 참조하세요.  
  
 MOVE TO { *file_group* | "default" }  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상  
  
 큐 내부 테이블(인덱스 포함)을 사용자가 지정한 파일 그룹으로 이동합니다.  새 파일 그룹은 읽기 전용이 아니어야 합니다.  
  
 PROCEDURE_NAME = \<procedure>  
 큐에 처리할 메시지가 포함된 경우 활성화할 저장 프로시저의 이름을 지정합니다. 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자여야 합니다.  
  
 *database_name*(프로시저)  
 저장 프로시저가 포함된 데이터베이스의 이름입니다.  
  
 *schema_name*(프로시저)  
 저장 프로시저를 소유한 스키마의 이름입니다.  
  
 *stored_procedure_name*  
 저장 프로시저의 이름입니다.  
  
 MAX_QUEUE_READERS =*max_reader*  
 큐에서 동시에 시작하는 활성화 저장 프로시저의 최대 인스턴스 수를 지정합니다. *max_readers*의 값은 0에서 32767 사이의 숫자여야 합니다.  
  
 EXECUTE AS  
 활성화 저장 프로시저를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 사용자 계정을 지정합니다. 큐에서 저장 프로시저를 시작할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 사용자의 권한을 확인할 수 있어야 합니다. Windows 도메인 사용자의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 도메인에 연결해야 하며 프로시저가 활성화되거나 활성화가 실패할 때 데이터베이스 엔진에서 지정한 사용자의 권한을 확인할 수 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자의 경우에는 서버에서 항상 권한을 확인할 수 있습니다.  
  
 SELF  
 저장 프로시저가 현재 사용자로 실행되도록 지정합니다(이 ALTER QUEUE 문을 실행하는 데이터베이스 보안 주체).  
  
 '*user_name*'  
 저장 프로시저가 실행되는 사용자 이름입니다. *user_name*은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자로 지정된 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자여야 합니다. 현재 사용자에게 지정한 *user_name*에 대한 IMPERSONATE 권한이 있어야 합니다.  
  
 OWNER  
 저장 프로시저가 큐의 소유자로 실행되도록 지정합니다.  
  
 DROP  
 큐와 연관된 모든 활성화 정보를 삭제합니다.  
  
 POISON_MESSAGE_HANDLING  
 포이즌 메시지 처리를 사용하는지 여부를 지정합니다. 기본값은 ON입니다.  
  
 포이즌 메시지 처리가 OFF로 설정된 큐는 트랜잭션 롤백이 연속으로 5회 발생하더라도 비활성화되지 않습니다. 이렇게 하면 애플리케이션에서 사용자 지정 포이즌 메시지 처리 시스템을 정의할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 활성화 저장 프로시저가 지정된 큐에 메시지가 포함된 경우 활성화 상태를 OFF에서 ON으로 변경하면 활성화 저장 프로시저가 즉시 활성화됩니다. 활성화 상태를 ON에서 OFF로 변경하면 Broker에서 저장 프로시저 인스턴스를 활성화하는 것을 중지하지만 현재 실행 중인 저장 프로시저 인스턴스는 중지하지 않습니다.  
  
 큐를 변경하여 활성화 저장 프로시저를 추가해도 큐의 활성화 상태는 변경되지 않습니다. 또한 큐의 활성화 저장 프로시저를 변경해도 현재 실행 중인 활성화 저장 프로시저 인스턴스에는 영향을 주지 않습니다.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서는 활성화 프로세스의 일부로 큐에 대한 최대 큐 판독기 수를 확인합니다. 그러므로 큐를 변경하여 최대 큐 판독기 수를 늘리면 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 즉시 더 많은 활성화 저장 프로시저 인스턴스를 시작할 수 있습니다. 또한 큐를 변경하여 최대 큐 판독기 수를 줄여도 현재 실행 중인 활성화 저장 프로시저 인스턴스에는 영향을 주지 않습니다. 그러나 활성화 저장 프로시저의 인스턴스 수가 구성된 최대 수 아래로 떨어질 때까지 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 저장 프로시저의 새 인스턴스를 시작하지 않습니다.  
  
 큐를 사용할 수 없는 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 데이터베이스 전송 큐에서 큐를 사용하는 서비스에 대한 메시지를 보유합니다. [sys.transmission_queue](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md) 카탈로그 뷰에서는 전송 큐 보기를 제공합니다.  
  
 RECEIVE 문 또는 GET CONVERSATION GROUP 문에서 사용할 수 없는 큐를 지정하는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 오류로 인해 이 문은 실패합니다.  
  
## <a name="permissions"></a>사용 권한  
 큐를 변경할 수 있는 권한은 기본적으로 큐의 소유자, db_ddladmin 또는 db_owner 고정 데이터베이스 역할의 멤버 및 sysadmin 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-making-a-queue-unavailable"></a>A. 큐를 사용할 수 없게 설정  
 다음 예에서는 `ExpenseQueue` 큐에서 메시지를 받을 수 없도록 설정합니다.  
  
```  
ALTER QUEUE ExpenseQueue WITH STATUS = OFF ;  
```  
  
### <a name="b-changing-the-activation-stored-procedure"></a>B. 활성화 저장 프로시저 변경  
 다음 예에서는 큐가 시작하는 저장 프로시저를 변경합니다. 이 저장 프로시저는 `ALTER QUEUE` 문을 실행한 사용자로 실행됩니다.  
  
```  
ALTER QUEUE ExpenseQueue  
    WITH ACTIVATION (  
        PROCEDURE_NAME = new_stored_proc,  
        EXECUTE AS SELF) ;  
```  
  
### <a name="c-changing-the-number-of-queue-readers"></a>C. 큐 판독기 수 변경  
 다음 예에서는 이 큐에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 시작하는 저장 프로시저 인스턴스의 최대 수를 `7`로 설정합니다.  
  
```  
ALTER QUEUE ExpenseQueue WITH ACTIVATION (MAX_QUEUE_READERS = 7) ;  
```  
  
### <a name="d-changing-the-activation-stored-procedure-and-the-execute-as-account"></a>D. 활성화 저장 프로시저 및 EXECUTE AS 계정 변경  
 다음 예에서는 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 시작하는 저장 프로시저를 변경합니다. 이 저장 프로시저는 `SecurityAccount` 사용자로 실행됩니다.  
  
```  
ALTER QUEUE ExpenseQueue  
    WITH ACTIVATION (  
        PROCEDURE_NAME = AdventureWorks2012.dbo.new_stored_proc ,  
        EXECUTE AS 'SecurityAccount') ;  
```  
  
### <a name="e-setting-the-queue-to-retain-messages"></a>E. 메시지를 유지하도록 큐 설정  
 다음 예에서는 메시지를 유지하도록 큐를 설정합니다. 이 큐에는 메시지가 포함된 대화가 종료될 때까지 이 큐를 사용하는 서비스와 주고 받은 모든 메시지가 유지됩니다.  
  
```  
ALTER QUEUE ExpenseQueue WITH RETENTION = ON ;  
```  
  
### <a name="f-removing-activation-from-a-queue"></a>F. 큐에서 활성화 제거  
 다음 예에서는 큐에서 모든 활성화 정보를 제거합니다.  
  
```  
ALTER QUEUE ExpenseQueue WITH ACTIVATION (DROP) ;  
```  
  
### <a name="g-rebuilding-queue-indexes"></a>G. 큐 인덱스 다시 작성  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상  
  
 다음 예에서는 큐 인덱스를 다시 작성합니다.  
  
```  
ALTER QUEUE ExpenseQueue REBUILD WITH (MAXDOP = 2)   
```  
  
### <a name="h-reorganizing-queue-indexes"></a>H. 큐 인덱스 다시 구성  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상  
  
 다음 예에서는 큐 인덱스를 다시 구성합니다.  
  
```  
ALTER QUEUE ExpenseQueue REORGANIZE   
```  
  
### <a name="i-moving-queue-internal-table-to-another-filegroup"></a>I: 큐 내부 테이블을 다른 파일 그룹으로 이동  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상  
  
```  
ALTER QUEUE ExpenseQueue MOVE TO [NewFilegroup]   
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [DROP QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-queue-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
  
