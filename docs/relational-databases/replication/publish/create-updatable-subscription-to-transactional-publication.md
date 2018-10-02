---
title: 트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 07/21/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- updateable transactional subscriptions, T-SQL
ms.assetid: a6e80857-0a69-4867-b6b7-f3629d00c312
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8150c81a52efb13a26b8fa0706d58fc0b6ee289
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713801"
---
# <a name="create-updatable-subscription-to-transactional-publication"></a>트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
> [!NOTE]  
>  이 기능은 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 2012부터 2016 버전에서 계속 지원됩니다.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
트랜잭션 복제에서는 즉시 업데이트 구독 또는 지연 업데이트 구독을 사용하여 구독자에서 변경된 내용을 게시자에 다시 전파할 수 있습니다. 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 업데이트 구독을 만들 수 있습니다. [트랜잭션 게시에 업데이트할 수 있는 구독 만들기(Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)도 참조하세요. 

## <a name="to-create-an-immediate-updating-pull-subscription"></a>즉시 업데이트 끌어오기 구독을 만들려면 ##

1. 게시자에서 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 즉시 업데이트 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_sync_tran` 값이 `1`이면 게시는 즉시 업데이트 구독을 지원합니다.

    * 결과 집합의 `allow_sync_tran` 값이 `0`이면 즉시 업데이트 구독을 설정하여 게시를 다시 만들어야 합니다.

2. 게시자에서 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 끌어오기 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_pull` 값이 `1`이면 게시에서 끌어오기 구독을 지원합니다.

    * `allow_pull` 값이 `0`이면 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행하여 `allow_pull` 에 대해 `@property` 을, `true` 에 대해 `@value`를 지정합니다. 

3. 구독자에서 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)을 실행합니다. `@publisher` 및 `@publication`를 지정하고 `@update_mode`에 다음 값 중 하나를 지정합니다.

    * `sync tran` - 구독에서 즉시 업데이트를 사용하도록 설정합니다.

    * `failover` - 즉시 업데이트 구독을 사용하고 지연 업데이트를 장애 조치(Failover) 옵션으로 설정합니다.

    > [!NOTE]  
>  `failover` 를 사용하려면 게시에서 지연 업데이트 구독도 설정해야 합니다. 
 
4. 구독자에서 [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)를 실행합니다. 다음을 지정합니다.

    * `@publisher`, `@publisher_db`및 `@publication` 매개 변수. 

    * `@job_login` 및 `@job_password`에 대해 구독자에서 배포 에이전트가 실행되는 Microsoft Windows 자격 증명. 

    > [!NOTE]  
>  Windows 통합 인증을 사용하여 만든 연결은 항상 `@job_login` 및 `@job_password`로 지정한 Windows 자격 증명을 사용합니다. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 구독자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 배포자에 연결합니다. 
 
    * (선택 사항) `0` 에 대한 `@distributor_security_mode` 값과, `@distributor_login` 및 `@distributor_password`에 대한 Microsoft SQL Server 로그인 정보(배포자에 연결할 때 SQL Server 인증을 사용 해야하는 경우). 

    * 이 구독에 대한 배포 에이전트 작업 일정. 

5. 구독 데이터베이스의 구독자에서 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)을 실행합니다. `@publisher`, `@publication`그리고 `@publisher_db`에 대한 게시 데이터베이스 이름을 지정하고 `@security_mode`에 다음 값 중 하나를 지정합니다. 

    * `0` - 게시자에서 업데이트할 때 SQL Server 인증을 사용합니다. 이 옵션을 사용하려면 `@login` 및 `@password`에 대해 게시자에 유효한 로그인을 지정해야 합니다.

    * `1` - 게시자에 연결할 때 구독자에서 변경 작업을 수행하는 사용자의 보안 컨텍스트를 사용합니다. 이 보안 모드에 관한 제한 사항에 대해서는 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 을 참조하세요.

    * `2`[sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)를 사용하여 만든 기존의 사용자 정의 연결된 서버 로그인을 사용합니다.

6. 게시자에서 [,](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) , `@publication`를 지정하고 `@subscriber`에 대한 가져오기 값, `@destination_db`에 대해 3단계에서 지정한 동일한 값을 지정하여 `@subscription_type`sp_addsubscription `@update_mode`을 실행합니다.

이렇게 하면 게시자에서 끌어오기 구독이 등록됩니다. 


## <a name="to-create-an-immediate-updating-push-subscription"></a>즉시 업데이트 밀어넣기 구독을 만들려면 ##

1. 게시자에서 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 즉시 업데이트 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_sync_tran` 값이 `1`이면 게시는 즉시 업데이트 구독을 지원합니다.

    * 결과 집합의 `allow_sync_tran` 값이 `0`이면 즉시 업데이트 구독을 설정하여 게시를 다시 만들어야 합니다.

2. 게시자에서 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 밀어넣기 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_push` 값이 `1`이면 게시에서 밀어넣기 구독을 지원합니다.

    * `allow_push` 값이 `0`이면 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행하여 `allow_push` 에 대해 `@property` 을, `true` 에 대해 `@value`를 지정합니다. 

3. 게시자에서 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)을 실행합니다. `@publication`, `@subscriber`, `@destination_db`를 지정하고 `@update_mode`에 다음 값 중 하나를 지정합니다.

    * `sync tran` - 즉시 업데이트 지원을 설정합니다.

    * `failover` - 즉시 업데이트 지원을 설정하고 지연 업데이트를 장애 조치 옵션으로 설정합니다.

    > [!NOTE]  
>  `failover` 를 사용하려면 게시에서 지연 업데이트 구독도 설정해야 합니다. 
 
4. 게시자에서 [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)를 실행합니다. 다음 매개 변수를 지정합니다.

    * `@subscriber`, `@subscriber_db`및 `@publication`. 

    * `@job_login` 및 `@job_password`에 대해 배포자에서 배포 에이전트가 실행되는 Windows 자격 증명 

    > [!NOTE]  
>  Windows 통합 인증을 사용하여 만든 연결은 항상 `@job_login` 및 `@job_password`로 지정한 Windows 자격 증명을 사용합니다. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 배포자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 구독자에 연결합니다. 

    * (선택 사항) `0` 에 대한 `@subscriber_security_mode` 값과, `@subscriber_login` 및 `@subscriber_password`에 대한 SQL Server 로그인 정보(구독자에 연결할 때 SQL Server 인증을 사용 해야하는 경우). 

    * 이 구독에 대한 배포 에이전트 작업 일정.

5. 구독 데이터베이스의 구독자에서 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)을 실행합니다. `@publisher`, `@publication`그리고 `@publisher_db`에 대한 게시 데이터베이스 이름을 지정하고 `@security_mode`에 다음 값 중 하나를 지정합니다. 

     * `0` - 게시자에서 업데이트할 때 SQL Server 인증을 사용합니다. 이 옵션을 사용하려면 `@login` 및 `@password`에 대해 게시자에 유효한 로그인을 지정해야 합니다.

     * `1` - 게시자에 연결할 때 구독자에서 변경 작업을 수행하는 사용자의 보안 컨텍스트를 사용합니다. 이 보안 모드에 관한 제한 사항에 대해서는 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 을 참조하세요.

     * `2`[sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)를 사용하여 만든 기존의 사용자 정의 연결된 서버 로그인을 사용합니다.


## <a name="to-create-a-queued-updating-pull-subscription"></a>지연 업데이트 끌어오기 구독을 만들려면 ##

1. 게시자에서 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 지연 업데이트 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_queued_tran` 값이 `1`이면 게시는 즉시 업데이트 구독을 지원합니다.

    * 결과 집합의 `allow_queued_tran` 값이 `0`이면 지연 업데이트 구독을 설정하여 게시를 다시 만들어야 합니다.

2. 게시자에서 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 끌어오기 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_pull` 값이 `1`이면 게시에서 끌어오기 구독을 지원합니다.

    * `allow_pull` 값이 `0`이면 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행하여 `allow_pull` 에 대해 `@property` 을, `true` 에 대해 `@value`를 지정합니다. 

3. 구독자에서 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)을 실행합니다. `@publisher` 및 `@publication`를 지정하고 `@update_mode`에 다음 값 중 하나를 지정합니다.

    * `queued tran` - 지연 업데이트 구독을 설정합니다.

    * `queued failover` - 지연 업데이트 지원을 설정하고 즉시 업데이트를 장애 조치 옵션으로 설정합니다.

    > [!NOTE]  
>  `queued failover` 를 사용하려면 게시에서 즉시 업데이트 구독도 설정해야 합니다. 즉시 업데이트로 장애 조치를 수행하려면 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 을 사용하여 구독자의 변경 내용을 게시자에 복제할 때 사용할 자격 증명을 정의해야 합니다.
 
4. 구독자에서 [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)를 실행합니다. 다음 매개 변수를 지정합니다.

    * @publisher, `@publisher_db`및 `@publication`. 

    * `@job_login` 및 `@job_password`에 대해 구독자에서 배포 에이전트가 실행되는 Windows 자격 증명 

    > [!NOTE]  
>  Windows 통합 인증을 사용하여 만든 연결은 항상 `@job_login` 및 `@job_password`로 지정한 Windows 자격 증명을 사용합니다. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 구독자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 배포자에 연결합니다. 
 
    * (선택 사항) `0` 에 대한 `@distributor_security_mode` 값과, `@distributor_login` 및 `@distributor_password`에 대한 SQL Server 로그인 정보(배포자에 연결할 때 SQL Server 인증을 사용 해야하는 경우). 

    * 이 구독에 대한 배포 에이전트 작업 일정.

5. 게시자에서 [,](../../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md) , `@publication`를 지정하고 `@subscriber`에 대한 가져오기 값, `@destination_db`에 대해 3단계에서 지정한 동일한 값을 지정하여 `@subscription_type`sp_addsubscription `@update_mode`을 실행하고 게시자에서 구독자를 등록합니다.

이렇게 하면 게시자에서 끌어오기 구독이 등록됩니다. 


## <a name="to-create-a-queued-updating-push-subscription"></a>지연 업데이트 밀어넣기 구독을 만들려면 ##

1. 게시자에서 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 지연 업데이트 구독을 지원하는지 확인합니다. 

    * 결과 집합의 allow_queued_tran 값이 1이면 게시는 즉시 업데이트 구독을 지원합니다.

    * 결과 집합의 allow_queued_tran 값이 0이면 지연 업데이트 구독을 설정하여 게시를 다시 만들어야 합니다. 자세한 내용은 방법: 트랜잭션 게시에 대한 구독 업데이트 설정(복제 Transact-SQL 프로그래밍)을 참조하세요.

2. 게시자에서 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 밀어넣기 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_push` 값이 `1`이면 게시에서 밀어넣기 구독을 지원합니다.

    * `allow_push` 값이 `0`이면 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행하여 `@property` 에 대해 allow_push를, `true` 에 대해 `@value`를 지정합니다. 

3. 게시자에서 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)을 실행합니다. `@publication`, `@subscriber`, `@destination_db`를 지정하고 `@update_mode`에 다음 값 중 하나를 지정합니다.

    * `queued tran` - 지연 업데이트 구독을 설정합니다.

    * `queued failover` - 지연 업데이트 지원을 설정하고 즉시 업데이트를 장애 조치 옵션으로 설정합니다.

    > [!NOTE]  
>  queued failover 옵션을 사용하려면 게시에서 즉시 업데이트 구독도 설정해야 합니다. 즉시 업데이트로 장애 조치를 수행하려면 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 을 사용하여 구독자의 변경 내용을 게시자에 복제할 때 사용할 자격 증명을 정의해야 합니다.

4. 게시자에서 [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)를 실행합니다. 다음 매개 변수를 지정합니다.

    * `@subscriber`, `@subscriber_db`및 `@publication`. 

    * `@job_login` 및 `@job_password`에 대해 배포자에서 배포 에이전트가 실행되는 Windows 자격 증명 

    > [!NOTE]  
>  Windows 통합 인증을 사용하여 만든 연결은 항상 `@job_login` 및 `@job_password`로 지정한 Windows 자격 증명을 사용합니다. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 배포자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 구독자에 연결합니다. 
 
    * (선택 사항) `0` 에 대한 `@subscriber_security_mode` 값과, `@subscriber_login` 및 `@subscriber_password`에 대한 SQL Server 로그인 정보(구독자에 연결할 때 SQL Server 인증을 사용 해야하는 경우). 

    * 이 구독에 대한 배포 에이전트 작업 일정.


## <a name="example"></a>예제 ##

이 예에서는 즉시 업데이트 구독을 지원하는 게시에 대해 즉시 업데이트 끌어오기 구독을 만듭니다. 로그인 및 암호 값은 sqlcmd 스크립팅 변수를 사용하여 런타임에 제공됩니다.

> [!NOTE]  
>  이 스크립트는 sqlcmd 스크립팅 변수를 사용합니다. 형식은 `$(MyVariable)`입니다. SQL Server Management Studio와 명령줄에서 스크립팅 변수를 사용하는 방법에 대한 내용은 **복제 시스템 저장 프로시저 개념** 항목의 [복제 스크립트 실행](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)섹션을 참조하세요.

```
-- Execute this batch at the Subscriber.
DECLARE @publication AS sysname;
DECLARE @publicationDB AS sysname;
DECLARE @publisher AS sysname;
DECLARE @login AS sysname;
DECLARE @password AS nvarchar(512);
SET @publication = N'AdvWorksProductTran';
SET @publicationDB = N'AdventureWorks2008R2';
SET @publisher = $(PubServer);
SET @login = $(Login);
SET @password = $(Password);

-- At the subscription database, create a pull subscription to a transactional 
-- publication using immediate updating with queued updating as a failover.
EXEC sp_addpullsubscription 
    @publisher = @publisher, 
    @publication = @publication, 
    @publisher_db = @publicationDB, 
    @update_mode = N'failover', 
    @subscription_type = N'pull';

-- Add an agent job to synchronize the pull subscription, 
-- which uses Windows Authentication when connecting to the Distributor.
EXEC sp_addpullsubscription_agent 
    @publisher = @publisher, 
    @publisher_db = @publicationDB, 
    @publication = @publication,
    @job_login = @login,
    @job_password = @password; 

-- Add a Windows Authentication-based linked server that enables the 
-- Subscriber-side triggers to make updates at the Publisher. 
EXEC sp_link_publication 
    @publisher = @publisher, 
    @publication = @publication,
    @publisher_db = @publicationDB, 
    @security_mode = 0,
    @login = @login,
    @password = @password;
GO

USE AdventureWorks2008R2;
GO

-- Execute this batch at the Publisher.
DECLARE @publication AS sysname;
DECLARE @subscriptionDB AS sysname;
DECLARE @subscriber AS sysname;
SET @publication = N'AdvWorksProductTran'; 
SET @subscriptionDB = N'AdventureWorks2008R2Replica'; 
SET @subscriber = $(SubServer);

-- At the Publisher, register the subscription, using the defaults.
USE [AdventureWorks2008R2]
EXEC sp_addsubscription 
    @publication = @publication, 
    @subscriber = @subscriber, 
    @destination_db = @subscriptionDB, 
    @subscription_type = N'pull', 
    @update_mode = N'failover';
GO
```

## <a name="see-also"></a>참고 항목 ##

[트랜잭션 복제를 위한 업데이트 가능 구독](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[스크립팅 변수와 함께 sqlcmd 사용](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)

[트랜잭션 게시에 업데이트할 수 있는 구독 만들기(Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)

