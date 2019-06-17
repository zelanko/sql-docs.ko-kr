---
title: Create an Updatable Subscription to a Transactional Publication (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- updateable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f9c04c03c08f118314dc96c8b491e61be317f40c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691592"
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication-management-studio"></a>트랜잭션 게시에 업데이트할 수 있는 구독 만들기(Management Studio)

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
트랜잭션 복제에서는 즉시 업데이트 구독 또는 지연 업데이트 구독을 사용하여 구독자에서 변경된 내용을 게시자에 다시 전파할 수 있습니다. 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 업데이트 구독을 만들 수 있습니다.

**새 구독 마법사**의 **업데이트할 수 있는 구독** 페이지에서 업데이트할 수 있는 구독을 구성할 수 있습니다. 이 페이지는 업데이트할 수 있는 구독에 대해 트랜잭션 게시를 설정한 경우에만 사용할 수 있습니다. 업데이트할 수 있는 구독을 사용하도록 설정하는 방법에 대한 자세한 내용은 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](enable-updating-subscriptions-for-transactional-publications.md)을 참조하세요.   
  
## <a name="configure-an-updatable-subscription-from-the-publisher"></a>게시자에서 업데이트할 수 있는 구독 구성  

1. Microsoft SQL Server Management Studio에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.
2. **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.
3. 구독 업데이트에 대해 설정된 트랜잭션 게시를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 클릭합니다.
4. 마법사의 페이지에 따라 배포 에이전트의 실행 위치 같은 구독 옵션을 지정합니다.
5. **새 구독 마법사**의 **업데이트할 수 있는 구독** 페이지에서 **복제**가 선택되었는지 확인합니다.
6. **게시자에서 커밋** 드롭다운 목록에서 옵션을 선택합니다.

    *  즉시 업데이트 구독을 사용하려면 **동시에 변경 내용 커밋**을 선택합니다. 이 옵션을 선택하고 게시에서 지연 업데이트 구독을 허용하면(새 게시 마법사로 만든 게시의 기본 설정) 구독 속성 **update_mode**가 **failover**로 설정됩니다. 이 모드에서는 필요하면 나중에 지연 업데이트로 전환할 수 있습니다.
    *  지연 업데이트 구독을 사용하려면 **변경 내용 대기 및 가능 시 커밋**을 선택합니다. 이 옵션을 선택하고 게시에서 즉시 업데이트 구독을 허용하며(새 게시 마법사로 만든 게시의 기본 설정) 구독자에서 SQL Server 2005 이상 버전이 실행될 경우 구독 속성 **update_mode**가 queued failover로 설정됩니다. 이 모드에서는 나중에 필요에 맞게 즉시 업데이트로 전환할 수 있습니다.

    업데이트 모드를 전환하는 방법에 대한 자세한 내용은 [업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드 전환](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)을 참조하세요.

7. 즉시 업데이트를 사용하거나 **update_mode**가 **queued failover**로 설정된 구독에 대해 **업데이트할 수 있는 구독에 대한 로그인** 페이지가 표시됩니다. **업데이트할 수 있는 구독에 대한 로그인** 페이지에서 즉시 업데이트 구독을 위해 게시자로의 연결이 설정된 연결된 서버를 지정합니다. 이 연결은 구독자에서 발생되는 트리거에 사용되고 게시자로 변경 내용을 전파합니다. 다음 옵션 중 하나를 선택합니다.

    * **다음 SQL Server 인증을 사용하여 연결되는 연결된 서버 만들기.** 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의하지 않은 경우 이 옵션을 선택하세요. 복제 시 연결된 서버가 자동으로 생성됩니다. 지정한 계정은 게시자에 이미 있어야 합니다.
    * **이미 정의한 연결된 서버나 원격 서버 사용** [sp_addserver(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), [sp_addlinkedserver(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql), SQL Server Management Studio 또는 다른 메서드를 사용하여 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의한 경우 이 옵션을 선택합니다.

    연결된 서버 계정에 필요한 사용 권한에 대한 자세한 내용은 [여기에 링크 설명 입력](../security/secure-the-subscriber.md)의 **지연 업데이트 구독**을 참조하세요.

8. 마법사를 완료합니다.

## <a name="configure-an-updatable-subscription-from-the-subscriber"></a>구독자에서 업데이트할 수 있는 구독 구성


1. SQL Server Management Studio에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.
2. **복제** 폴더를 확장합니다.
3. **로컬 구독** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 클릭합니다.
4. **새 구독 마법사**의 **게시** 페이지에 있는 **게시자** 드롭다운 목록에서 **SQL Server 게시자 찾기**를 선택합니다.
5. **서버에 연결** 대화 상자에서 게시자에 연결합니다.
6. **게시** 페이지에서 구독 업데이트에 대해 설정된 트랜잭션 게시를 선택합니다.
7. 마법사의 페이지에 따라 배포 에이전트의 실행 위치 같은 구독 옵션을 지정합니다.
8. 새 구독 마법사의 **업데이트할 수 있는 구독** 페이지에서 **복제**가 선택되었는지 확인합니다.
9. **게시자에서 커밋** 드롭다운 목록에서 옵션을 선택합니다.

    * 즉시 업데이트 구독을 사용하려면 **동시에 변경 내용 커밋**을 선택합니다. 이 옵션을 선택하고 게시에서 지연 업데이트 구독을 허용하면(새 게시 마법사로 만든 게시의 기본 설정) 구독 속성 **update_mode**가 **failover**로 설정됩니다. 이 모드에서는 필요하면 나중에 지연 업데이트로 전환할 수 있습니다.
    * 지연 업데이트 구독을 사용하려면 **변경 내용 대기 및 가능 시 커밋**을 선택합니다. 이 옵션을 선택하고 게시에서 즉시 업데이트 구독을 허용하며(새 게시 마법사로 만든 게시의 기본 설정) 구독자에서 SQL Server 2005 이상 버전이 실행될 경우 구독 속성 **update_mode**가 queued **failover**로 설정됩니다. 이 모드에서는 나중에 필요에 맞게 즉시 업데이트로 전환할 수 있습니다.

    업데이트 모드를 전환하는 방법에 대한 자세한 내용은 [업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드 전환](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)을 참조하세요.

10. 즉시 업데이트를 사용하거나 **update_mode**가 **queued failover**로 설정된 구독에 대해 **업데이트할 수 있는 구독에 대한 로그인** 페이지가 표시됩니다. **업데이트할 수 있는 구독에 대한 로그인** 페이지에서 즉시 업데이트 구독을 위해 게시자로의 연결이 설정된 연결된 서버를 지정합니다. 이 연결은 구독자에서 발생되는 트리거에 사용되고 게시자로 변경 내용을 전파합니다. 다음 옵션 중 하나를 선택합니다.

    * **다음 SQL Server 인증을 사용하여 연결되는 연결된 서버 만들기.** 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의하지 않은 경우 이 옵션을 선택하세요. 복제 시 연결된 서버가 자동으로 생성됩니다. 지정한 계정은 게시자에 이미 있어야 합니다.
    * **이미 정의한 연결된 서버나 원격 서버 사용** [sp_addserver(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), [sp_addlinkedserver(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql), SQL Server Management Studio 또는 다른 메서드를 사용하여 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의한 경우 이 옵션을 선택합니다.

    연결된 서버 계정에 필요한 사용 권한에 대한 자세한 내용은 [여기에 링크 설명 입력](../security/secure-the-subscriber.md)의 **지연 업데이트 구독**을 참조하세요.

11. 마법사를 완료합니다.

## <a name="create-an-immediate-updating-pull-subscription"></a>즉시 업데이트 끌어오기 구독 만들기

1. 게시자에서 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)을 실행하여 게시에서 즉시 업데이트 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_sync_tran` 값이 `1`이면 게시는 즉시 업데이트 구독을 지원합니다.
    * 결과 집합의 `allow_sync_tran` 값이 `0`이면 즉시 업데이트 구독을 설정하여 게시를 다시 만들어야 합니다.

2. 게시자에서 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)을 실행하여 게시에서 끌어오기 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_pull` 값이 `1`이면 게시에서 끌어오기 구독을 지원합니다.
    * `allow_pull` 값이 `0`이면 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)을 실행하여 `allow_pull` 에 대해 `@property` 을, `true` 에 대해 `@value`를 지정합니다. 

3. 구독자에서 [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)을 실행합니다. `@publisher` 및 `@publication`를 지정하고 `@update_mode`에 다음 값 중 하나를 지정합니다.

    * `sync tran` - 구독에서 즉시 업데이트를 사용하도록 설정합니다.
    * `failover` - 즉시 업데이트 구독을 사용하고 지연 업데이트를 장애 조치(Failover) 옵션으로 설정합니다.

    > [!NOTE]  
>  `failover` 를 사용하려면 게시에서 지연 업데이트 구독도 설정해야 합니다. 
 
4. 구독자에서 [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)를 실행합니다. 다음을 지정합니다.

    * `@publisher`, `@publisher_db`및 `@publication` 매개 변수. 
    * `@job_login` 및 `@job_password`에 대해 구독자에서 배포 에이전트가 실행되는 Microsoft Windows 자격 증명. 

    > [!NOTE]  
>  Windows 통합 인증을 사용하여 만든 연결은 항상 `@job_login` 및 `@job_password`로 지정한 Windows 자격 증명을 사용합니다. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 구독자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 배포자에 연결합니다. 
 
    * (선택 사항) `0` 에 대한 `@distributor_security_mode` 값과, `@distributor_login` 및 `@distributor_password`에 대한 Microsoft SQL Server 로그인 정보(배포자에 연결할 때 SQL Server 인증을 사용 해야하는 경우). 
    * 이 구독에 대한 배포 에이전트 작업 일정. 

5. 구독 데이터베이스의 구독자에서 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)을 실행합니다. `@publisher`, `@publication`그리고 `@publisher_db`에 대한 게시 데이터베이스 이름을 지정하고 `@security_mode`에 다음 값 중 하나를 지정합니다. 

    * `0` - 게시자에서 업데이트할 때 SQL Server 인증을 사용합니다. 이 옵션을 사용하려면 `@login` 및 `@password`에 대해 게시자에 유효한 로그인을 지정해야 합니다.
    * `1` - 게시자에 연결할 때 구독자에서 변경 작업을 수행하는 사용자의 보안 컨텍스트를 사용합니다. 이 보안 모드에 관한 제한 사항에 대해서는 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) 을 참조하세요.
    * `2`[sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)를 사용하여 만든 기존의 사용자 정의 연결된 서버 로그인을 사용합니다.

6. 게시자에서 [,](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) , `@publication`를 지정하고 `@subscriber`에 대한 가져오기 값, `@destination_db`에 대해 3단계에서 지정한 동일한 값을 지정하여 `@subscription_type`sp_addsubscription `@update_mode`을 실행합니다.

이렇게 하면 게시자에서 끌어오기 구독이 등록됩니다. 


## <a name="create-an-immediate-updating-push-subscription"></a>즉시 업데이트 밀어넣기 구독 만들기 

1. 게시자에서 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)을 실행하여 게시에서 즉시 업데이트 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_sync_tran` 값이 `1`이면 게시는 즉시 업데이트 구독을 지원합니다.
    * 결과 집합의 `allow_sync_tran` 값이 `0`이면 즉시 업데이트 구독을 설정하여 게시를 다시 만들어야 합니다.

2. 게시자에서 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)을 실행하여 게시에서 밀어넣기 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_push` 값이 `1`이면 게시에서 밀어넣기 구독을 지원합니다.
    * `allow_push` 값이 `0`이면 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)을 실행하여 `allow_push` 에 대해 `@property` 을, `true` 에 대해 `@value`를 지정합니다. 

3. 게시자에서 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)을 실행합니다. `@publication`, `@subscriber`, `@destination_db`를 지정하고 `@update_mode`에 다음 값 중 하나를 지정합니다.

    * `sync tran` - 즉시 업데이트 지원을 설정합니다.
    * `failover` - 즉시 업데이트 지원을 설정하고 지연 업데이트를 장애 조치 옵션으로 설정합니다.

    > [!NOTE]  
>  `failover` 를 사용하려면 게시에서 지연 업데이트 구독도 설정해야 합니다. 
 
4. 게시자에서 [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)를 실행합니다. 다음 매개 변수를 지정합니다.

    * `@subscriber`, `@subscriber_db`및 `@publication`. 
    * `@job_login` 및 `@job_password`에 대해 배포자에서 배포 에이전트가 실행되는 Windows 자격 증명 

    > [!NOTE]  
>  Windows 통합 인증을 사용하여 만든 연결은 항상 `@job_login` 및 `@job_password`로 지정한 Windows 자격 증명을 사용합니다. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 배포자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 구독자에 연결합니다. 

    * (선택 사항) `0` 에 대한 `@subscriber_security_mode` 값과, `@subscriber_login` 및 `@subscriber_password`에 대한 SQL Server 로그인 정보(구독자에 연결할 때 SQL Server 인증을 사용 해야하는 경우). 
    * 이 구독에 대한 배포 에이전트 작업 일정.

5. 구독 데이터베이스의 구독자에서 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)을 실행합니다. `@publisher`, `@publication`그리고 `@publisher_db`에 대한 게시 데이터베이스 이름을 지정하고 `@security_mode`에 다음 값 중 하나를 지정합니다. 

     * `0` - 게시자에서 업데이트할 때 SQL Server 인증을 사용합니다. 이 옵션을 사용하려면 `@login` 및 `@password`에 대해 게시자에 유효한 로그인을 지정해야 합니다.
     * `1` - 게시자에 연결할 때 구독자에서 변경 작업을 수행하는 사용자의 보안 컨텍스트를 사용합니다. 이 보안 모드에 관한 제한 사항에 대해서는 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) 을 참조하세요.
     * `2`[sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)를 사용하여 만든 기존의 사용자 정의 연결된 서버 로그인을 사용합니다.


## <a name="create-a-queued-updating-pull-subscription"></a>지연 업데이트 끌어오기 구독 만들기 ##

1. 게시자에서 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)을 실행하여 게시에서 지연 업데이트 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_queued_tran` 값이 `1`이면 게시는 즉시 업데이트 구독을 지원합니다.
    * 결과 집합의 `allow_queued_tran` 값이 `0`이면 지연 업데이트 구독을 설정하여 게시를 다시 만들어야 합니다.

2. 게시자에서 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)을 실행하여 게시에서 끌어오기 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_pull` 값이 `1`이면 게시에서 끌어오기 구독을 지원합니다.
    * `allow_pull` 값이 `0`이면 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)을 실행하여 `allow_pull` 에 대해 `@property` 을, `true` 에 대해 `@value`를 지정합니다. 

3. 구독자에서 [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)을 실행합니다. `@publisher` 및 `@publication`를 지정하고 `@update_mode`에 다음 값 중 하나를 지정합니다.

    * `queued tran` - 지연 업데이트 구독을 설정합니다.
    * `queued failover` - 지연 업데이트 지원을 설정하고 즉시 업데이트를 장애 조치 옵션으로 설정합니다.

    > [!NOTE]  
>  `queued failover` 를 사용하려면 게시에서 즉시 업데이트 구독도 설정해야 합니다. 즉시 업데이트로 장애 조치를 수행하려면 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) 을 사용하여 구독자의 변경 내용을 게시자에 복제할 때 사용할 자격 증명을 정의해야 합니다.
 
4. 구독자에서 [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)를 실행합니다. 다음 매개 변수를 지정합니다.

    * @publisher, `@publisher_db`및 `@publication`. 
    * `@job_login` 및 `@job_password`에 대해 구독자에서 배포 에이전트가 실행되는 Windows 자격 증명 

    > [!NOTE]  
>  Windows 통합 인증을 사용하여 만든 연결은 항상 `@job_login` 및 `@job_password`로 지정한 Windows 자격 증명을 사용합니다. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 구독자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 배포자에 연결합니다. 
 
    * (선택 사항) `0` 에 대한 `@distributor_security_mode` 값과, `@distributor_login` 및 `@distributor_password`에 대한 SQL Server 로그인 정보(배포자에 연결할 때 SQL Server 인증을 사용 해야하는 경우). 
    * 이 구독에 대한 배포 에이전트 작업 일정.

5. 게시자에서 [,](/sql/relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql) , `@publication`를 지정하고 `@subscriber`에 대한 가져오기 값, `@destination_db`에 대해 3단계에서 지정한 동일한 값을 지정하여 `@subscription_type`sp_addsubscription `@update_mode`을 실행하고 게시자에서 구독자를 등록합니다.

이렇게 하면 게시자에서 끌어오기 구독이 등록됩니다. 


## <a name="to-create-a-queued-updating-push-subscription"></a>지연 업데이트 밀어넣기 구독을 만들려면 ##

1. 게시자에서 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)을 실행하여 게시에서 지연 업데이트 구독을 지원하는지 확인합니다. 

    * 결과 집합의 allow_queued_tran 값이 1이면 게시는 즉시 업데이트 구독을 지원합니다.
    * 결과 집합의 allow_queued_tran 값이 0이면 지연 업데이트 구독을 설정하여 게시를 다시 만들어야 합니다. 자세한 내용은 방법: 트랜잭션 게시에 대한 구독 업데이트를 설정합니다(복제 Transact-SQL 프로그래밍).

2. 게시자에서 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)을 실행하여 게시에서 밀어넣기 구독을 지원하는지 확인합니다. 

    * 결과 집합의 `allow_push` 값이 `1`이면 게시에서 밀어넣기 구독을 지원합니다.
    * `allow_push` 값이 `0`이면 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)을 실행하여 `@property` 에 대해 allow_push를, `true` 에 대해 `@value`를 지정합니다. 

3. 게시자에서 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)을 실행합니다. `@publication`, `@subscriber`, `@destination_db`를 지정하고 `@update_mode`에 다음 값 중 하나를 지정합니다.

    * `queued tran` - 지연 업데이트 구독을 설정합니다.
    * `queued failover` - 지연 업데이트 지원을 설정하고 즉시 업데이트를 장애 조치 옵션으로 설정합니다.

    > [!NOTE]  
>  queued failover 옵션을 사용하려면 게시에서 즉시 업데이트 구독도 설정해야 합니다. 즉시 업데이트로 장애 조치를 수행하려면 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) 을 사용하여 구독자의 변경 내용을 게시자에 복제할 때 사용할 자격 증명을 정의해야 합니다.

4. 게시자에서 [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)를 실행합니다. 다음 매개 변수를 지정합니다.

    * `@subscriber`, `@subscriber_db`및 `@publication`. 
    * `@job_login` 및 `@job_password`에 대해 배포자에서 배포 에이전트가 실행되는 Windows 자격 증명 

    > [!NOTE]  
>  Windows 통합 인증을 사용하여 만든 연결은 항상 `@job_login` 및 `@job_password`로 지정한 Windows 자격 증명을 사용합니다. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 배포자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 구독자에 연결합니다. 
 
    * (선택 사항) `0` 에 대한 `@subscriber_security_mode` 값과, `@subscriber_login` 및 `@subscriber_password`에 대한 SQL Server 로그인 정보(구독자에 연결할 때 SQL Server 인증을 사용 해야하는 경우). 
    * 이 구독에 대한 배포 에이전트 작업 일정.


## <a name="example"></a>예제 ##

이 예에서는 즉시 업데이트 구독을 지원하는 게시에 대해 즉시 업데이트 끌어오기 구독을 만듭니다. 로그인 및 암호 값은 sqlcmd 스크립팅 변수를 사용하여 런타임에 제공됩니다.

> [!NOTE]  
>  이 스크립트는 sqlcmd 스크립팅 변수를 사용합니다. 형식은 `$(MyVariable)`입니다. SQL Server Management Studio와 명령줄에서 스크립팅 변수를 사용하는 방법에 대한 내용은 **복제 시스템 저장 프로시저 개념** 항목의 [복제 스크립트 실행](../concepts/replication-system-stored-procedures-concepts.md)섹션을 참조하세요.

```sql
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

## <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>지연 업데이트 충돌 해결 옵션 설정(SQL Server Management Studio)
  **게시 속성 - \<Publication>** 대화 상자의 **구독 옵션** 페이지에서 지연 업데이트 구독을 지원하는 게시에 대한 충돌 해결 옵션을 설정할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](view-and-modify-publication-properties.md)을 참조하세요.  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>지연 업데이트 충돌 해결 옵션을 설정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **구독 옵션** 페이지에서 **충돌 해결 정책** 옵션에 대해 다음 값 중 하나를 선택합니다.    
    -   **게시자 변경 내용 유지**    
    -   **구독자 변경 내용 유지**    
    -   **구독 다시 초기화**    
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="see-also"></a>관련 항목 ##
 [Create a Publication](create-a-publication.md)   
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)   
 [스크립팅 변수와 함께 sqlcmd 사용](../../scripting/sqlcmd-use-with-scripting-variables.md)   

  
