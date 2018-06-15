---
title: 복제 스크립트 업그레이드(복제 Transact-SQL 프로그래밍) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server replication], upgrading
- upgrading SQL Server, replicated databases
- upgrading replication applications
- replication [SQL Server], scripting
- replication [SQL Server], upgrading
- upgrading replicated databases
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
caps.latest.revision: 41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 19e2adba0742454e039f106f1ed5c3cd693384f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32957308"
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>복제 스크립트 업그레이드(복제 Transact-SQL 프로그래밍)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트 파일을 사용하여 복제 토폴로지를 프로그래밍 방식으로 구성할 수 있습니다. 자세한 내용은 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  **sysadmin** 역할의 멤버에 의해 실행되는 스크립트는 반드시 업그레이드할 필요는 없지만 이 항목에서 설명하는 대로 기존 스크립트를 수정하는 것이 좋습니다. [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)항목의 "에이전트에 필요한 사용 권한" 섹션에서 설명하는 대로 각 복제 에이전트에 대해 최소 사용 권한이 있는 계정을 지정합니다.  
  
 이러한 향상된 보안 기능은 복제 에이전트 작업이 실행되는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 계정을 명시적으로 지정할 수 있도록 함으로써 사용 권한을 보다 잘 제어할 수 있게 해 주며, 기존 스크립트의 다음 저장 프로시저에 영향을 줍니다.  
  
-   **sp_addpublication_snapshot**:  
  
     이제 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)을 실행하여 배포자에서 스냅숏 에이전트가 실행되는 작업을 만들 때 Windows 자격 증명을 **@job_login** 및 **@job_password**로 제공해야 합니다.  
  
-   **sp_addpushsubscription_agent**:  
  
     이제 [sp_addpushsubscription_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)를 실행하여 명시적으로 작업을 추가하고 배포자에서 배포 에이전트 작업이 실행되는 Windows 자격 증명(**@job_login** 및 **@job_password**)을 제공해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 이 작업은 밀어넣기 구독이 만들어질 때 자동으로 수행되었습니다.  
  
-   **sp_addmergepushsubscription_agent**:  
  
     이제 [sp_addmergepushsubscription_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)를 실행하여 명시적으로 작업을 추가하고 배포자에서 병합 에이전트 작업이 실행되는 Windows 자격 증명(**@job_login** 및 **@job_password**)을 제공해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 이 작업은 밀어넣기 구독이 만들어질 때 자동으로 수행되었습니다.  
  
-   **sp_addpullsubscription_agent**:  
  
     이제 [sp_addpullsubscription_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)를 실행하여 구독자에서 배포 에이전트가 실행되는 작업을 만들 때 Windows 자격 증명을 **@job_login** 및 **@job_password**로 제공해야 합니다.  
  
-   **sp_addmergepullsubscription_agent**:  
  
     이제 [sp_addmergepullsubscription_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)를 실행하여 구독자에서 병합 에이전트가 실행되는 작업을 만들 때 Windows 자격 증명을 **@job_login** 및 **@job_password**로 제공해야 합니다.  
  
-   **sp_addlogreader_agent**:  
  
     이제 [sp_addlogreader_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)를 실행하여 수동으로 작업을 추가하고 배포자에서 로그 판독기 에이전트가 실행되는 Windows 자격 증명을 지정해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 이 작업은 트랜잭션 게시가 만들어질 때 자동으로 수행되었습니다.  
  
-   **sp_addqreader_agent**:  
  
     이제 [sp_addqreader_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)를 실행하여 수동으로 작업을 추가하고 배포자에서 큐 판독기 에이전트가 실행되는 Windows 자격 증명을 지정해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 이 작업은 지연 업데이트를 지원하는 트랜잭션 게시가 만들어질 때 자동으로 수행되었습니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 보안 모델에서 복제 에이전트는 항상 **@job_name** 및 **@job_password**에 지정된 자격 증명을 사용하는 Windows 인증을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 로컬 인스턴스에 연결합니다. 복제 에이전트 작업을 실행할 때 사용되는 Windows 계정의 요구 사항에 대한 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 스크립트 파일에 자격 증명을 저장하는 경우에는 파일 자체에 보안이 설정되도록 합니다.  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시를 구성하는 스크립트를 업그레이드하려면  
  
1.  기존 스크립트의 [sp_addpublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 전에 게시 데이터베이스의 게시자에서 [sp_addlogreader_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)를 실행합니다. **@job_name** 및 **@job_password**에 로그 판독기 에이전트가 실행되는 Windows 자격 증명을 지정합니다. 게시자에 연결할 때 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하면 **@publisher_security_mode** 에 대해 값 **@publisher_security_mode** 을 지정하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @publisher_login **@publisher_login** @job_login **@publisher_password**을 참조하세요. 이렇게 하면 게시 데이터베이스에 대한 로그 판독기 에이전트가 만들어집니다.  
  
    > [!NOTE]  
    >  이 단계는 트랜잭션 게시 전용이며 스냅숏 게시에는 필요하지 않습니다.  
  
2.  (옵션) [sp_addpublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 전에 배포 데이터베이스의 배포자에서 [sp_addqreader_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)를 실행합니다. **@job_name** 및 **@job_password**에 큐 판독기 에이전트가 실행되는 Windows 자격 증명을 지정합니다. 이렇게 하면 배포자에 대한 큐 판독기 에이전트가 만들어집니다.  
  
    > [!NOTE]  
    >  이 단계는 지연 업데이트 구독자를 지원하는 트랜잭션 게시에만 필요합니다.  
  
3.  (옵션) 새 복제 기능을 구현하는 매개 변수에 대해 기본값이 아닌 값을 설정하려면 [sp_addpublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 실행을 업데이트합니다.  
  
4.  [sp_addpublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 다음에 게시 데이터베이스의 게시자에서 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)을 실행합니다. 스냅숏 에이전트가 **@job_name** 및 **@job_password**에 대해 실행되는 **@publication** 및 Windows 자격 증명을 지정합니다. 게시자에 연결할 때 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하면 **@publisher_security_mode** 에 대해 값 **@publisher_security_mode** 을 지정하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @publisher_login **@publisher_login** @job_login **@publisher_password**을 참조하세요. 이렇게 하면 게시에 대해 스냅숏 에이전트 작업이 만들어집니다.  
  
5.  (옵션) 새 복제 기능을 구현하는 매개 변수에 대해 기본값이 아닌 값을 설정하려면 [sp_addarticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 실행을 업데이트합니다.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 구독을 추가하는 스크립트를 업그레이드하려면  
  
1.  구독을 만드는 저장 프로시저를 실행한 후 구독을 동기화할 구독 에이전트 작업을 만드는 저장 프로시저를 실행합니다. 사용하는 저장 프로시저는 구독 유형에 따라 달라집니다.  
  
    -   끌어오기 구독의 경우 [sp_addpullsubscription_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)의 실행을 업데이트하여 **@job_name** 및 **@job_password**에 대해 구독자에서 배포 에이전트가 실행되는 Windows 자격 증명을 지정합니다. 이 작업은 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)을 실행한 후에 수행합니다. 자세한 내용은 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)을 참조하세요.  
  
    -   밀어넣기 구독의 경우 게시자에서 [sp_addpushsubscription_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)를 실행합니다. **@subscriber**, **@subscriber_db**, **@publication**을 지정하고, **@job_name** 및 **@job_password**에 대해 배포자에서 배포 에이전트가 실행되는 Windows 자격 증명을 지정한 다음 이 에이전트 작업의 일정을 지정합니다. 자세한 내용은 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요. 이 작업은 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)을 실행한 후에 수행됩니다. 자세한 내용은 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)을 참조하세요.  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>병합 게시를 구성하는 스크립트를 업그레이드하려면  
  
1.  (옵션) 기존 스크립트에서 새 복제 기능을 구현하는 매개 변수에 대해 기본값이 아닌 값을 설정하려면 [sp_addmergepublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 실행을 업데이트합니다.  
  
2.  [sp_addmergepublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 다음에 게시 데이터베이스의 게시자에서 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)을 실행합니다. 스냅숏 에이전트가 **@job_name** 및 **@job_password**에 대해 실행되는 **@publication** 및 Windows 자격 증명을 지정합니다. 게시자에 연결할 때 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하면 **@publisher_security_mode** 에 대해 값 **@publisher_security_mode** 을 지정하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @publisher_login **@publisher_login** @job_login **@publisher_password**을 참조하세요. 이렇게 하면 게시에 대해 스냅숏 에이전트 작업이 만들어집니다.  
  
3.  (옵션) 새 복제 기능을 구현하는 매개 변수에 대해 기본값이 아닌 값을 설정하려면 [sp_addmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 실행을 업데이트합니다.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>병합 게시에 구독을 추가하는 스크립트를 업그레이드하려면  
  
1.  구독을 만드는 저장 프로시저를 실행한 후 구독을 동기화할 병합 에이전트를 만드는 저장 프로시저를 실행합니다. 사용하는 저장 프로시저는 구독 유형에 따라 달라집니다.  
  
    -   끌어오기 구독의 경우 [sp_addmergepullsubscription_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)의 실행을 업데이트하여 **@job_name** 및 **@job_password**에 대해 구독자에서 병합 에이전트가 실행되는 Windows 자격 증명을 지정합니다. 이 작업은 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)을 실행한 후 수행합니다. 자세한 내용은 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)을 참조하세요.  
  
    -   밀어넣기 구독의 경우 게시자에서 [sp_addmergepushsubscription_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)를 실행합니다. **@subscriber**, **@subscriber_db**, **@publication**을 지정하고, **@job_name** 및 **@job_password**에 배포자에서 병합 에이전트가 실행되는 Windows 자격 증명을 지정한 다음 이 에이전트 작업의 일정을 지정합니다. 자세한 내용은 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요. 이 작업은 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)을 실행한 후 수행합니다. 자세한 내용은 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음은 Product 테이블의 트랜잭션 게시를 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 이 게시에서는 지연 업데이트를 장애 조치로 사용하는 즉시 업데이트를 지원합니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_1.sql)]  
  
## <a name="example"></a>예제  
 다음은 트랜잭션 게시를 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 이 게시에서는 지연 업데이트를 장애 조치로 사용하는 즉시 업데이트를 지원합니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>  Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_2.sql)]  
  
## <a name="example"></a>예제  
 다음은 Customers 테이블의 병합 게시를 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_3.sql)]  
  
## <a name="example"></a>예제  
 다음은 병합 게시를 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>  Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_4.sql)]  
  
## <a name="example"></a>예제  
 다음은 트랜잭션 게시에 밀어넣기 구독을 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_5.sql)]  
  
## <a name="example"></a>예제  
 다음은 트랜잭션 게시에 밀어넣기 구독을 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>  Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_6.sql)]  
  
## <a name="example"></a>예제  
 다음은 병합 게시에 밀어넣기 구독을 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>예제  
 다음은 병합 게시에 밀어넣기 구독을 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>  Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_8.sql)]  
  
## <a name="example"></a>예제  
 다음은 트랜잭션 게시에 끌어오기 구독을 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>예제  
 다음은 트랜잭션 게시에 끌어오기 구독을 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>  Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_9.sql)]  
  
## <a name="example"></a>예제  
 다음은 병합 게시에 끌어오기 구독을 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_10.sql)]  
  
## <a name="example"></a>예제  
 다음은 병합 게시에 끌어오기 구독을 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>  Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_11.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)   
 [복제 보안 설정 보기 및 수정](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../../../relational-databases/replication/mssql-eng021797.md)   
 [MSSQL_ENG021798](../../../relational-databases/replication/mssql-eng021798.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [복제된 데이터베이스 업그레이드](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
