---
title: max worker threads 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4881cefee350d34d93b539c56be6f43866d3ddfe
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935659"
---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>max worker threads 서버 구성 옵션 구성
  이 항목에서는 **또는**을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]max worker threads[!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **max worker threads** 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 사용할 수 있는 작업자 스레드 수를 구성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 운영 체제의 네이티브 스레드 서비스를 사용하여 하나 이상의 스레드가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 지원하는 각 네트워크를 동시에 지원하고 또 다른 스레드가 데이터베이스 검사점을 처리하고 스레드 풀이 모든 사용자를 처리하도록 합니다. **max worker threads** 의 기본값은 0입니다. 이 값을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작할 때 작업자 스레드 수가 자동으로 구성됩니다. 기본 설정은 대부분의 시스템에 적합합니다. 그러나 시스템 구성에 따라 **max worker threads** 를 특정 값으로 설정하면 성능이 향상되기도 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **최대 작업자 스레드 수 옵션을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [최대 작업자 스레드 수 옵션을 구성한 후](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   실제 쿼리 요청 수가 **max worker threads**에 설정된 값보다 적으면 각 쿼리 요청마다 스레드 하나가 사용됩니다. 그러나 실제 쿼리 요청 수가 **max worker threads**에 설정 된 크기를 초과 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음에 사용할 수 있는 작업자 스레드가 요청을 처리할 수 있도록 작업자 스레드를 풀링합니다.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자만 변경해야 합니다.  
  
-   스레드 풀링을 사용하면 많은 클라이언트가 서버에 연결되어 있을 때 성능이 최적화됩니다. 보통 각 쿼리 요청마다 별도의 운영 체제 스레드가 생성됩니다. 그러나 서버에 대한 연결 수가 수백 개인 경우 쿼리 요청별로 스레드를 하나씩 사용하면 시스템 리소스를 상당히 많이 소비하게 될 수 있습니다. **max worker threads** 옵션을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 작업자 스레드 풀을 만들어 많은 쿼리 요청을 처리할 수 있으므로 성능이 향상됩니다.  
  
-   다음 표에서는 다양한 CPU 조합과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에 대해 자동으로 구성되는 최대 작업자 스레드 수를 보여 줍니다.  
  
    |CPU 수|32비트 컴퓨터|64비트 컴퓨터|  
    |--------------------|----------------------|----------------------|  
    |\<4개 이하 프로세서|256|512|  
    |8개의 프로세서|288|576|  
    |16개의 프로세서|352|704|  
    |32개의 프로세서|480|960|  
    |64개의 프로세서|736|1472|  
    |128개의 프로세서|4224|4480|  
    |256개의 프로세서|8320|8576|  
  
    > [!NOTE]  
    >  64개가 넘는 CPU 사용에 대한 권장 사항은 [64개를 초과하는 CPU가 있는 컴퓨터에서 SQL Server를 실행하기 위한 최선의 방법](https://technet.microsoft.com/library/ee210547\(SQL.105\).aspx)을 참조하세요.  
  
    > [!WARNING]  
    >  32비트 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 최대 작업자 스레드 수는 1024로 설정하는 것이 좋습니다.  
  
-   장기 실행 쿼리의 모든 작업자 스레드가 활성 상태이면 작업자 스레드가 완료되어 사용 가능 상태가 되기 전에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 응답하지 않을 수 있습니다. 이는 오류는 아니지만 바람직한 상태는 아닙니다. 프로세스가 응답할 수 없고 새 쿼리를 처리할 수 없으면 DAC(관리자 전용 연결)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결한 다음 해당 프로세스를 중지합니다. 이를 방지하려면 max worker threads 수를 증가시킵니다.  
  
 **최대 작업자 스레드 수** 서버 구성 옵션은 가용성 그룹, Service Broker, 잠금 관리자 등의 모든 시스템 태스크에 필요한 스레드 수를 고려하지 않습니다.  다음 쿼리는 구성된 스레드 수를 초과할 경우 추가 스레드를 생성한 시스템 태스크에 대한 정보를 제공합니다.  
  
```  
SELECT  
s.session_id,  
r.command,  
r.status,  
r.wait_type,  
r.scheduler_id,  
w.worker_address,  
w.is_preemptive,  
w.state,  
t.task_state,  
t.session_id,  
t.exec_context_id,  
t.request_id  
FROM sys.dm_exec_sessions AS s  
INNERJOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
WHERE s.is_user_process = 0;  
  
```  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>최대 작업자 스레드 수 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **프로세서** 노드를 클릭합니다.  
  
3.  **최대 작업자 스레드** 상자에 128에서 32767 까지의 값을 입력 하거나 선택 합니다.  
  
     **max worker threads** 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 사용할 수 있는 작업자 스레드 수를 구성할 수 있습니다. 대부분의 시스템에는 **max worker threads** 의 기본 설정을 사용하는 것이 최상의 방법입니다. 그러나 시스템 구성에 따라 **max worker threads** 를 더 작은 값으로 설정하면 성능이 향상되기도 합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>최대 작업자 스레드 수 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예제에서는 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 를 사용하여 `max worker threads` 옵션을 `900`으로 구성하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'max worker threads', 900 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="follow-up-after-you-configure-the-max-worker-threads-option"></a><a name="FollowUp"></a> 후속 작업: 최대 작업자 스레드 수 옵션을 구성한 후  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 다시 시작할 필요 없이 변경 사항이 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [데이터베이스 관리자를 위한 진단 연결](diagnostic-connection-for-database-administrators.md)  
  
  
