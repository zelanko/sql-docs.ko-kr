---
title: WAITFOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- WAITFOR
- WAITFOR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TIME option
- delaying executions [SQL Server]
- batches [SQL Server], execution times
- stored procedures [SQL Server], executing
- DELAY
- time [SQL Server], execution delays
- blocking executions
- transactions [SQL Server], execution times
- WAITFOR statement
- timing executions
ms.assetid: 8e896e73-af27-4cae-a725-7a156733f3bd
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: bee373167ee406e9383053af0f312925441b8895
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="waitfor-transact-sql"></a>WAITFOR(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  지정된 시간 또는 시간 간격에 도달하거나 지정된 문이 최소 한 행을 수정 또는 반환할 때까지 일괄 처리, 저장 프로시저 또는 트랜잭션의 실행을 차단합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
WAITFOR   
{  
    DELAY 'time_to_pass'   
  | TIME 'time_to_execute'   
  | [ ( receive_statement ) | ( get_conversation_group_statement ) ]   
    [ , TIMEOUT timeout ]  
}  
```  
  
## <a name="arguments"></a>인수  
 DELAY  
 일괄 처리, 저장 프로시저 또는 트랜잭션을 실행하기 전에 대기하도록 지정된 시간으로 최대 24시간이 될 수 있습니다.  
  
 '*time_to_pass*'  
 대기할 총 시간입니다. *time_to_pass*는 **datetime** 데이터로 사용할 수 있는 형식 중 하나를 사용하여 지정하거나 지역 변수로 지정할 수 있습니다. 날짜를 지정할 수 없으므로 **datetime** 값의 날짜 부분은 허용되지 않습니다. 이 형식은 hh:mm[[:ss].mss]로 지정됩니다.
  
 TIME  
 일괄 처리, 저장 프로시저 또는 트랜잭션을 실행하도록 지정된 시간입니다.  
  
 '*time_to_execute*'  
 WAITFOR 문이 종료되는 시간입니다. *time_to_execute*는 **datetime** 데이터로 사용할 수 있는 형식 중 하나를 사용하여 지정하거나 지역 변수로 지정할 수 있습니다. 날짜를 지정할 수 없으므로 **datetime** 값의 날짜 부분은 허용되지 않습니다. 이 형식은 hh:mm[[:ss].mss]로 지정되고, 선택적으로 1900-01-01의 날짜를 포함할 수 있습니다.
  
 *receive_statement*  
 유효한 RECEIVE 문입니다.  
  
> [!IMPORTANT]  
>  *receive_statement*가 있는 WAITFOR는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지에만 적용됩니다. 자세한 내용은 [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)을 참조하세요.  
  
 *get_conversation_group_statement*  
 유효한 GET CONVERSATION GROUP 문입니다.  
  
> [!IMPORTANT]  
>  *get_conversation_group_statement*가 있는 WAITFOR는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지에만 적용됩니다. 자세한 내용은 [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)을 참조하세요.  
  
 TIMEOUT *제한 시간*  
 메시지가 큐에 도착하기를 대기할 시간(밀리초)을 지정합니다.  
  
> [!IMPORTANT]  
>  TIMEOUT이 있는 WAITFOR는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지에만 적용됩니다. 자세한 내용은 [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md) 및 [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 WAITFOR 문을 실행하는 동안 트랜잭션이 실행되며 같은 트랜잭션에서 다른 요청을 실행할 수 없습니다.  
  
 실제 시간 지연은 *time_to_pass*, *time_to_execute* 또는 *timeout*에 지정된 시간과 다를 수 있으며 서버의 작업 수준에 따라 달라집니다. 시간 카운터는 WAITFOR 문과 연결된 스레드가 예약된 시간에 시작합니다. 서버가 사용 중이면 스레드가 즉시 예약되지 않을 수도 있으므로 시간 지연이 지정된 시간보다 길어질 수 있습니다.  
  
 WAITFOR는 쿼리의 기능을 변경하지 않습니다. 쿼리가 행을 반환할 수 없을 경우 WAITFOR는 계속 대기하거나 TIMEOUT(지정된 경우)에 도달할 때까지 대기합니다.  
  
 WAITFOR 문에서는 커서를 열 수 없습니다.  
  
 WAITFOR 문에서는 뷰를 정의할 수 없습니다.  
  
 쿼리가 query wait 옵션을 초과하면 WAITFOR 문 인수를 실행하지 않고 완료할 수 있습니다. 자세한 내용은 [query wait 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md)을 참조하세요. 활성 및 대기 프로세스를 보려면 [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)를 사용합니다.  
  
 각 WAITFOR 문에는 연결된 스레드가 있습니다. 같은 서버에 많은 WAITFOR 문이 지정된 경우 많은 스레드가 이러한 문의 실행을 대기하느라 정체될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 WAITFOR 문과 연결된 스레드의 수를 모니터링하고 서버에 스레드 부족이 발생하기 시작할 경우 이러한 스레드 중 일부를 임의로 선택하여 종료합니다.  
  
 WAITFOR 문이 액세스를 시도하는 행 집합에 대한 변경을 방지하는 잠금을 보유한 트랜잭션 내에서 WAITFOR를 사용하여 쿼리를 실행하면 교착 상태가 발생할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이러한 시나리오를 식별하고 이러한 교착 상태가 존재할 가능성이 있는 경우 빈 결과 집합을 반환합니다.  
  
> [!CAUTION]  
>  WAITFOR를 포함하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스의 완료 속도가 저하되고 응용 프로그램에서 시간 초과 메시지가 나타날 수 있습니다. 필요할 경우 응용 프로그램 수준에서 연결에 대한 제한 시간 설정을 조정하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-waitfor-time"></a>1. WAITFOR TIME 사용  
 다음 예에서는 msdb 데이터베이스에서 `sp_update_job` 저장 프로시저를 오후 10시 20분에 실행합니다. (`22:20`).  
  
```  
EXECUTE sp_add_job @job_name = 'TestJob';  
BEGIN  
    WAITFOR TIME '22:20';  
    EXECUTE sp_update_job @job_name = 'TestJob',  
        @new_name = 'UpdatedJob';  
END;  
GO  
```  
  
### <a name="b-using-waitfor-delay"></a>2. WAITFOR DELAY 사용  
 다음 예에서는 2시간 지연 후에 저장 프로시저를 실행합니다.  
  
```  
BEGIN  
    WAITFOR DELAY '02:00';  
    EXECUTE sp_helpdb;  
END;  
GO  
```  
  
### <a name="c-using-waitfor-delay-with-a-local-variable"></a>3. 지역 변수와 함께 WAITFOR DELAY 사용  
 다음 예에서는 지역 변수를 `WAITFOR DELAY` 옵션과 함께 사용하는 방법을 보여 줍니다. 저장 프로시저는 정해진 시간 동안 변수를 기다린 다음 사용자에게 경과된 시간, 분 및 초 수 정보를 반환하도록 생성됩니다.  
  
```  
IF OBJECT_ID('dbo.TimeDelay_hh_mm_ss','P') IS NOT NULL  
    DROP PROCEDURE dbo.TimeDelay_hh_mm_ss;  
GO  
CREATE PROCEDURE dbo.TimeDelay_hh_mm_ss   
    (  
    @DelayLength char(8)= '00:00:00'  
    )  
AS  
DECLARE @ReturnInfo varchar(255)  
IF ISDATE('2000-01-01 ' + @DelayLength + '.000') = 0  
    BEGIN  
        SELECT @ReturnInfo = 'Invalid time ' + @DelayLength   
        + ',hh:mm:ss, submitted.';  
        -- This PRINT statement is for testing, not use in production.  
        PRINT @ReturnInfo   
        RETURN(1)  
    END  
BEGIN  
    WAITFOR DELAY @DelayLength  
    SELECT @ReturnInfo = 'A total time of ' + @DelayLength + ',   
        hh:mm:ss, has elapsed! Your time is up.'  
    -- This PRINT statement is for testing, not use in production.  
    PRINT @ReturnInfo;  
END;  
GO  
/* This statement executes the dbo.TimeDelay_hh_mm_ss procedure. */  
EXEC TimeDelay_hh_mm_ss '00:00:10';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `A total time of 00:00:10, in hh:mm:ss, has elapsed. Your time is up.`  
  
## <a name="see-also"></a>참고 항목  
 [흐름 제어 언어 &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)   
 [sp_who&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  
