---
title: 복제 스크립트 업그레이드(복제 Transact-SQL 프로그래밍) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c47101c76ca2c585accd493b74f0e59c56bf009e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055749"
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>복제 스크립트 업그레이드(복제 Transact-SQL 프로그래밍)
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트 파일을 사용하여 복제 토폴로지를 프로그래밍 방식으로 구성할 수 있습니다. 자세한 내용은 [복제 시스템 저장 프로시저 개념](../concepts/replication-system-stored-procedures-concepts.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  `sysadmin` 역할의 멤버에 의해 실행되는 스크립트는 반드시 업그레이드할 필요는 없지만 이 항목에서 설명하는 대로 기존 스크립트를 수정하는 것이 좋습니다. [Replication Agent Security Model](../security/replication-agent-security-model.md)항목의 "에이전트에 필요한 사용 권한" 섹션에서 설명하는 대로 각 복제 에이전트에 대해 최소 사용 권한이 있는 계정을 지정합니다.  
  
 이러한 향상된 보안 기능은 복제 에이전트 작업이 실행되는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 계정을 명시적으로 지정할 수 있도록 함으로써 사용 권한을 보다 잘 제어할 수 있게 해 주며, 기존 스크립트의 다음 저장 프로시저에 영향을 줍니다.  
  
-   **sp_addpublication_snapshot**:  
  
     이제 **@job_login** **@job_password** [sp_addpublication_snapshot &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) 를 실행 하 여 배포자에서 스냅숏 에이전트 실행 되는 작업을 만들 때 Windows 자격 증명을 제공 해야 합니다.  
  
-   **sp_addpushsubscription_agent**:  
  
     이제 [sp_addpushsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)를 실행하여 명시적으로 작업을 추가하고 배포자에서 배포 에이전트 작업이 실행되는 Windows 자격 증명(**@job_login** 및 **@job_password**)을 제공해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 이 작업은 밀어넣기 구독이 만들어질 때 자동으로 수행되었습니다.  
  
-   **sp_addmergepushsubscription_agent**:  
  
     이제 [sp_addmergepushsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)를 실행하여 명시적으로 작업을 추가하고 배포자에서 병합 에이전트 작업이 실행되는 Windows 자격 증명(**@job_login** 및 **@job_password**)을 제공해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 이 작업은 밀어넣기 구독이 만들어질 때 자동으로 수행되었습니다.  
  
-   **sp_addpullsubscription_agent**:  
  
     이제 **@job_login** **@job_password** [sp_addpullsubscription_agent &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) 를 실행 하 여 구독자에서 배포 에이전트 실행 되는 작업을 만들 때 Windows 자격 증명을 제공 해야 합니다.  
  
-   **sp_addmergepullsubscription_agent**:  
  
     이제 **@job_login** **@job_password** [sp_addmergepullsubscription_agent &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) 를 실행 하 여 구독자에서 병합 에이전트 실행 되는 작업을 만들 때 Windows 자격 증명을 제공 해야 합니다.  
  
-   **sp_addlogreader_agent**:  
  
     이제 [sp_addlogreader_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)를 실행하여 수동으로 작업을 추가하고 배포자에서 로그 판독기 에이전트가 실행되는 Windows 자격 증명을 지정해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 이 작업은 트랜잭션 게시가 만들어질 때 자동으로 수행되었습니다.  
  
-   **sp_addqreader_agent**:  
  
     이제 [sp_addqreader_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql)를 실행하여 수동으로 작업을 추가하고 배포자에서 큐 판독기 에이전트가 실행되는 Windows 자격 증명을 지정해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 이 작업은 지연 업데이트를 지원하는 트랜잭션 게시가 만들어질 때 자동으로 수행되었습니다.  
  
 에 도입 된 보안 모델에서 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 복제 에이전트는 항상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및에 제공 된 자격 증명을 사용 하 여 Windows 인증을 통해의 로컬 인스턴스에 연결 합니다 **@job_name** **@job_password** . 복제 에이전트 작업을 실행할 때 사용되는 Windows 계정의 요구 사항에 대한 자세한 내용은 [Replication Agent Security Model](../security/replication-agent-security-model.md)을 참조하십시오.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 스크립트 파일에 자격 증명을 저장하는 경우에는 파일 자체에 보안이 설정되도록 합니다.  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시를 구성하는 스크립트를 업그레이드하려면  
  
1.  기존 스크립트의 [sp_addpublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 전에 게시 데이터베이스의 게시자에서 [sp_addlogreader_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)를 실행합니다. 및에 대 한 로그 판독기 에이전트 실행 되는 Windows 자격 증명을 지정 합니다 **@job_name** **@job_password** . 게시자에 연결할 때 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하면 **@publisher_security_mode** @allow_subscriber_initiated_snapshot **@publisher_security_mode** 에 1단계에 사용된 게시 이름, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 **@publisher_login** 에 **@publisher_password**을 참조하세요. 이렇게 하면 게시 데이터베이스에 대한 로그 판독기 에이전트가 만들어집니다.  
  
    > [!NOTE]  
    >  이 단계는 트랜잭션 게시 전용이며 스냅샷 게시에는 필요하지 않습니다.  
  
2.  (옵션) [sp_addpublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 전에 배포 데이터베이스의 배포자에서 [sp_addqreader_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql)를 실행합니다. 및에 대 한 큐 판독기 에이전트 실행 되는 Windows 자격 증명을 지정 합니다 **@job_name** **@job_password** . 이렇게 하면 배포자에 대한 큐 판독기 에이전트가 만들어집니다.  
  
    > [!NOTE]  
    >  이 단계는 지연 업데이트 구독자를 지원하는 트랜잭션 게시에만 필요합니다.  
  
3.  (옵션) 새 복제 기능을 구현하는 매개 변수에 대해 기본값이 아닌 값을 설정하려면 [sp_addpublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 실행을 업데이트합니다.  
  
4.  [sp_addpublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 다음에 게시 데이터베이스의 게시자에서 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)을 실행합니다. 및 **@publication** 에 대 한 스냅숏 에이전트 실행 되는 및 Windows 자격 증명을 지정 합니다 **@job_name** **@job_password** . 게시자에 연결할 때 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하면 **@publisher_security_mode** @allow_subscriber_initiated_snapshot **@publisher_security_mode** 에 1단계에 사용된 게시 이름, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 **@publisher_login** 에 **@publisher_password**을 참조하세요. 이렇게 하면 게시에 대해 스냅샷 에이전트 작업이 만들어집니다.  
  
5.  (옵션) 새 복제 기능을 구현하는 매개 변수에 대해 기본값이 아닌 값을 설정하려면 [sp_addarticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 실행을 업데이트합니다.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에 구독을 추가하는 스크립트를 업그레이드하려면  
  
1.  구독을 만드는 저장 프로시저를 실행한 후 구독을 동기화할 구독 에이전트 작업을 만드는 저장 프로시저를 실행합니다. 사용하는 저장 프로시저는 구독 유형에 따라 달라집니다.  
  
    -   끌어오기 구독의 경우 [sp_addpullsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)의 실행을 업데이트하여 **@job_name** 및 **@job_password**에 대해 구독자에서 배포 에이전트가 실행되는 Windows 자격 증명을 지정합니다. 이 작업은 [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)을 실행한 후에 수행합니다. 자세한 내용은 [끌어오기 구독 만들기](../create-a-pull-subscription.md)를 참조하세요.  
  
    -   밀어넣기 구독의 경우 게시자에서 [sp_addpushsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)를 실행합니다. **@subscriber** **@subscriber_db** **@publication** 및에 대 한 배포자에서 배포 에이전트 실행 되는,,, Windows 자격 **@job_name** 증명 **@job_password** 및이 에이전트 작업의 일정을 지정 합니다. 자세한 내용은 [동기화 일정 지정](../specify-synchronization-schedules.md)을 참조 하세요. 이 작업은 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)을 실행한 후에 수행됩니다. 자세한 내용은 [밀어넣기 구독 만들기](../create-a-push-subscription.md)을 참조하세요.  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>병합 게시를 구성하는 스크립트를 업그레이드하려면  
  
1.  (옵션) 기존 스크립트에서 새 복제 기능을 구현하는 매개 변수에 대해 기본값이 아닌 값을 설정하려면 [sp_addmergepublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) 실행을 업데이트합니다.  
  
2.  [sp_addmergepublication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) 다음에 게시 데이터베이스의 게시자에서 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)을 실행합니다. 및 **@publication** 에 대 한 스냅숏 에이전트 실행 되는 및 Windows 자격 증명을 지정 합니다 **@job_name** **@job_password** . 게시자에 연결할 때 에이전트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하면 **@publisher_security_mode** @allow_subscriber_initiated_snapshot **@publisher_security_mode** 에 1단계에 사용된 게시 이름, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 **@publisher_login** 에 **@publisher_password**을 참조하세요. 이렇게 하면 게시에 대해 스냅샷 에이전트 작업이 만들어집니다.  
  
3.  (옵션) 새 복제 기능을 구현하는 매개 변수에 대해 기본값이 아닌 값을 설정하려면 [sp_addmergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 실행을 업데이트합니다.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>병합 게시에 구독을 추가하는 스크립트를 업그레이드하려면  
  
1.  구독을 만드는 저장 프로시저를 실행한 후 구독을 동기화할 병합 에이전트를 만드는 저장 프로시저를 실행합니다. 사용하는 저장 프로시저는 구독 유형에 따라 달라집니다.  
  
    -   끌어오기 구독의 경우 [sp_addmergepullsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)의 실행을 업데이트하여 **@job_name** 및 **@job_password**에 대해 구독자에서 병합 에이전트가 실행되는 Windows 자격 증명을 지정합니다. 이 작업은 [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)을 실행한 후 수행합니다. 자세한 내용은 [끌어오기 구독 만들기](../create-a-pull-subscription.md)를 참조하세요.  
  
    -   밀어넣기 구독의 경우 게시자에서 [sp_addmergepushsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)를 실행합니다. **@subscriber**, **@subscriber_db** ,을 지정 하 고, **@publication** 및에 대해 배포자의 병합 에이전트를 실행 하는 데 사용할 Windows 자격 증명을 지정 **@job_name** **@job_password** 하 고,이 에이전트 작업의 일정을 지정 합니다. 자세한 내용은 [동기화 일정 지정](../specify-synchronization-schedules.md)을 참조 하세요. 이 작업은 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)을 실행한 후 수행합니다. 자세한 내용은 [밀어넣기 구독 만들기](../create-a-push-subscription.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음은 Product 테이블의 트랜잭션 게시를 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 이 게시에서는 지연 업데이트를 장애 조치로 사용하는 즉시 업데이트를 지원합니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpub80.sql#sp_createtranpub_nwpreupgrade)]  
  
## <a name="example"></a>예제  
 다음은 트랜잭션 게시를 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 이 게시에서는 지연 업데이트를 장애 조치로 사용하는 즉시 업데이트를 지원합니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>   Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpublication.sql#sp_createtranpub_nwpostupgrade)]  
  
## <a name="example"></a>예제  
 다음은 Customers 테이블의 병합 게시를 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepub80.sql#sp_createmergepub_nwpreupgrade)]  
  
## <a name="example"></a>예제  
 다음은 병합 게시를 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>   Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepublication.sql#sp_createmergepub_nwpostupgrade)]  
  
## <a name="example"></a>예제  
 다음은 트랜잭션 게시에 밀어넣기 구독을 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpushsub80.sql#sp_createtranpushsub_nwpreupgrade)]  
  
## <a name="example"></a>예제  
 다음은 트랜잭션 게시에 밀어넣기 구독을 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>   Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpushsub.sql#sp_createtranpushsub_nwpostupgrade)]  
  
## <a name="example"></a>예제  
 다음은 병합 게시에 밀어넣기 구독을 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepushsub80.sql#sp_createmergepushsub_nwpreupgrade)]  
  
## <a name="example"></a>예제  
 다음은 병합 게시에 밀어넣기 구독을 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>   Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpushsub.sql#sp_createmergepushsub_nwpostupgrade)]  
  
## <a name="example"></a>예제  
 다음은 트랜잭션 게시에 끌어오기 구독을 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepushsub80.sql#sp_createmergepushsub_nwpreupgrade)]  
  
## <a name="example"></a>예제  
 다음은 트랜잭션 게시에 끌어오기 구독을 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>   Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpullsub.sql#sp_createtranpullsub_nwpostupgrade)]  
  
## <a name="example"></a>예제  
 다음은 병합 게시에 끌어오기 구독을 만드는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 스크립트의 예제입니다. 읽기 쉽도록 기본 매개 변수가 삭제되었습니다.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepullsub80.sql#sp_createmergepullsub_nwpreupgrade)]  
  
## <a name="example"></a>예제  
 다음은 병합 게시에 끌어오기 구독을 만드는 앞의 스크립트를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 성공적으로 실행되도록 업그레이드하는 예제입니다. 새 매개 변수의 기본값이 명시적으로 선언되었습니다.  
  
> [!NOTE]  
>   Windows 자격 증명은 **sqlcmd** 스크립팅 변수를 사용하여 런타임에 제공됩니다.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpullsub.sql#sp_createmergepullsub_nwpostupgrade)]  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../publish/create-a-publication.md)   
 [밀어넣기 구독 만들기](../create-a-push-subscription.md)   
 [Create a Pull Subscription](../create-a-pull-subscription.md)   
 [복제 보안 설정 보기 및 수정](../security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../mssql-eng021797.md)   
 [MSSQL_ENG021798](../mssql-eng021798.md)   
 [복제 시스템 저장 프로시저 개념](../concepts/replication-system-stored-procedures-concepts.md)   
 [복제된 데이터베이스 업그레이드](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
