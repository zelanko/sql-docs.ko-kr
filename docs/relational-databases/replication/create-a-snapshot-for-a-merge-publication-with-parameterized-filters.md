---
title: 매개 변수가 있는 필터로 병합 게시에 대한 스냅숏 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 05/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
ms.assetid: 00dfb229-f1de-4d33-90b0-d7c99ab52dcb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 142822158f03c76c1c36f40fa937438c989ec3ad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811801"
---
# <a name="create-a-snapshot-for-a-merge-publication-with-parameterized-filters"></a>매개 변수가 있는 필터로 병합 게시에 대한 스냅숏 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 매개 변수가 있는 필터로 병합 게시에 대한 스냅숏을 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
-   **매개 변수가 있는 필터를 사용하여 병합 게시에 대한 스냅숏을 새로 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   매개 변수가 있는 필터를 사용하여 병합 게시에 대한 스냅숏을 만들 때는 게시된 데이터 및 구독에 대한 구독자 메타데이터를 모두 포함하는 표준(스키마) 스냅숏을 먼저 생성해야 합니다. 자세한 내용은 [초기 스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요. 스키마 스냅숏을 만든 다음에는 게시된 데이터의 구독자별 파티션을 포함하는 스냅숏을 만들 수 있습니다.  
  
-   게시에 있는 여러 아티클에 대한 필터링 시 각 구독에 고유하면서도 겹치지 않는 파티션이 생성될 경우 메타데이터는 병합 에이전트가 실행될 때마다 정리됩니다. 따라서 분할된 스냅숏은 더 빨리 만료됩니다. 이 옵션을 사용할 경우 구독자가 스냅숏 생성 및 배달을 시작하도록 허용하는 것을 고려해야 합니다. 필터링 옵션에 대한 자세한 내용은 [매개 변수가 있는 필터를 사용하는 병합 게시의 스냅숏](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)에서 "'partition options' 설정" 섹션을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **게시 속성 - \<게시>** 대화 상자의 **데이터 파티션** 페이지에서 파티션에 대한 스냅숏을 생성합니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요. 구독자가 스냅숏 생성 및 배달을 시작하고 스냅숏을 생성하도록 허용할 수 있습니다.  
  
 하나 이상의 파티션에 대한 스냅숏을 생성하기 전에 다음을 수행해야 합니다.  
  
1.  새 게시 마법사를 사용하여 병합 게시를 만들고 마법사의 **필터 추가** 페이지에서 매개 변수가 있는 행 필터를 하나 이상 지정합니다. 자세한 내용은 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
2.  게시에 대한 스키마 스냅숏을 생성합니다. 기본적으로 스키마 스냅숏은 새 게시 마법사를 완료할 때 생성됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 스키마 스냅숏을 생성할 수도 있습니다.  
  
#### <a name="to-generate-a-schema-snapshot"></a>스키마 스냅숏을 생성하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **게시** 폴더를 확장합니다.  
  
3.  스냅숏을 생성할 게시를 마우스 오른쪽 단추로 클릭한 다음 **스냅숏 에이전트 상태 보기**를 클릭합니다.  
  
4.  **스냅숏 에이전트 상태 보기 - \<게시>** 대화 상자에서 **시작**을 클릭합니다.  
  
     스냅숏 에이전트에서 스냅숏 생성을 마치면 "[100%] 17개 아티클의 스냅숏이 생성되었습니다"라는 메시지가 표시됩니다.  
  
#### <a name="to-allow-subscribers-to-initiate-snapshot-generation-and-delivery"></a>구독자가 스냅숏 생성 및 배달을 시작하도록 허용하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **데이터 파티션** 페이지에서 **새 구독자가 동기화할 때 필요한 경우 자동으로 파티션 정의 및 스냅숏 생성**을 선택합니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-generate-and-refresh-snapshots"></a>스냅숏을 생성하고 새로 고치려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **데이터 파티션** 페이지에서 **추가**를 클릭합니다.  
  
2.  스냅숏을 만들 파티션과 연결된 **HOST_NAME()** 및/또는 **SUSER_SNAME()** 값을 입력합니다.  
  
3.  선택적으로 스냅숏을 새로 고칠 일정을 지정합니다.  
  
    1.  **이 파티션에 대한 스냅숏 에이전트의 실행 시간을 다음 시간으로 예약**을 선택합니다.  
  
    2.  기본으로 제공되는 스냅숏 새로 고침 일정을 그대로 적용하거나 **변경** 을 클릭하여 다른 일정을 지정합니다.  
  
4.  **확인**을 클릭합니다. 그러면 **게시 속성 - \<게시>** 대화 상자로 돌아갑니다.  
  
5.  속성 표에서 파티션을 선택한 다음 **선택한 스냅숏 지금 생성**을 클릭합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 저장 프로시저 및 스냅숏 에이전트를 사용하여 다음을 수행할 수 있습니다.  
  
-   구독자가 처음 동기화될 때 스냅숏 생성 및 적용을 요청하도록 허용합니다.  
  
-   각 파티션에 대한 스냅숏을 미리 생성합니다.  
  
-   각 구독자에 대한 스냅숏을 수동으로 생성합니다.  
  
    > [!IMPORTANT]  
    >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
#### <a name="to-create-a-publication-that-allows-subscribers-to-initiate-snapshot-generation-and-delivery"></a>구독자가 스냅숏 생성 및 배달을 시작하도록 허용하는 게시를 만들려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)을 실행합니다. 다음 매개 변수를 지정합니다.  
  
    -   **@publication**에 대한 게시의 이름  
  
    -   **@allow_subscriber_initiated_snapshot**에 **true** 값을 지정합니다. 이렇게 하면 구독자가 스냅숏 프로세스를 시작할 수 있습니다.  
  
    -   (옵션) **@max_concurrent_dynamic_snapshots**을 참조하세요. 최대 수의 프로세스가 실행 중인 상태에서 구독자가 스냅숏 생성을 시도하면 이 프로세스는 큐에 배치됩니다. 기본적으로 동시 프로세스의 수에는 제한이 없습니다.  
  
2.  게시자에서 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)을 실행합니다. **@publication**에 1단계에서 사용된 게시 이름을, **@job_login** 및 **@password**에 [복제 스냅숏 에이전트](../../relational-databases/replication/agents/replication-snapshot-agent.md)를 실행하는 데 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 자격 증명을 지정합니다. 게시자에 연결할 때 에이전트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하면 **@publisher_security_mode** @allow_subscriber_initiated_snapshot **@publisher_security_mode** 에 1단계에 사용된 게시 이름, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 **@publisher_login** 에 **@publisher_password**을 참조하세요. 이렇게 하면 게시에 대해 스냅숏 에이전트 작업이 만들어집니다. 초기 스냅숏을 생성하고 스냅숏 에이전트에 대한 사용자 지정 일정을 정의하는 방법은 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)를 참조하세요.  
  
    > [!IMPORTANT]  
    >  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
3.  [sp_addmergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행하여 게시에 아티클을 추가합니다. 이 저장 프로시저는 게시의 각 아티클에 대해 한 번씩만 실행해야 합니다. 매개 변수가 있는 필터를 사용할 경우 **@subset_filterclause** 매개 변수를 사용하여 하나 이상의 아티클에 대해 매개 변수가 있는 행 필터를 지정해야 합니다. 자세한 내용은 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
4.  다른 아티클이 매개 변수가 있는 행 필터에 따라 필터링되면 [sp_addmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)를 실행하여 아티클 간의 조인 또는 논리 레코드 관계를 정의합니다. 이 저장 프로시저는 정의되는 각 관계에 대해 한 번씩만 실행해야 합니다. 자세한 내용은 [병합 아티클 사이에서 조인 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)을 참조하세요.  
  
5.  병합 에이전트가 구독자를 초기화하기 위해 스냅숏을 요청하면 구독의 파티션을 요청하기 위한 스냅숏이 자동으로 생성됩니다.  
  
#### <a name="to-create-a-publication-and-pre-generate-or-automatically-refresh-snapshots"></a>게시를 만들고 스냅숏을 미리 생성하거나 자동으로 새로 고치려면  
  
1.  [sp_addmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)을 실행하여 게시를 만듭니다. 자세한 내용은 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
2.  게시자에서 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)을 실행합니다. **@publication**에 1단계에서 사용된 게시 이름을, **@job_login** 및 **@password**에 스냅숏 에이전트를 실행하는 데 사용되는 Windows 자격 증명을 지정합니다. 게시자에 연결할 때 에이전트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하면 **@publisher_security_mode** @allow_subscriber_initiated_snapshot **@publisher_security_mode** 에 1단계에 사용된 게시 이름, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 **@publisher_login** 에 **@publisher_password**을 참조하세요. 이렇게 하면 게시에 대해 스냅숏 에이전트 작업이 만들어집니다. 초기 스냅숏을 생성하고 스냅숏 에이전트에 대한 사용자 지정 일정을 정의하는 방법은 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)를 참조하세요.  
  
    > [!IMPORTANT]  
    >  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
3.  [sp_addmergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행하여 게시에 아티클을 추가합니다. 이 저장 프로시저는 게시의 각 아티클에 대해 한 번씩만 실행해야 합니다. 매개 변수가 있는 필터를 사용할 경우 **@subset_filterclause** 매개 변수를 사용하여 하나 이상의 아티클에 대해 매개 변수가 있는 행 필터를 지정해야 합니다. 자세한 내용은 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
4.  다른 아티클이 매개 변수가 있는 행 필터에 따라 필터링되면 [sp_addmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)를 실행하여 아티클 간의 조인 또는 논리 레코드 관계를 정의합니다. 이 저장 프로시저는 정의되는 각 관계에 대해 한 번씩만 실행해야 합니다. 자세한 내용은 [병합 아티클 사이에서 조인 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)을 참조하세요.  
  
5.  게시 데이터베이스의 게시자에서 1단계의 **@publication** 값을 지정하여 [sp_helpmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)을 실행합니다. 결과 집합에서 **snapshot_jobid** 값을 확인합니다.  
  
6.  5단계에서 얻은 **snapshot_jobid** 의 값을 **uniqueidentifier**로 변환합니다.  
  
7.  **msdb** 데이터베이스의 게시자에서 **@job_id**에 6단계에서 얻은 변환된 값을 지정하고 [sp_start_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)을 실행합니다.  
  
8.  게시 데이터베이스의 게시자에서 [sp_addmergepartition&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)을 실행합니다. **@publication**에 1단계의 게시 이름을, **@suser_sname**([SUSER_SNAME&#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md)이 필터 절에 사용된 경우) 또는 **@host_name**([HOST_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md)이 필터 절에 사용된 경우)에 파티션을 정의하는 데 사용되는 값을 지정합니다.  
  
9. 게시 데이터베이스의 게시자에서 [sp_adddynamicsnapshot_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)을 실행합니다. **@publication**에 1단계의 게시 이름을 지정하고 8단계의 **@suser_sname** 또는 **@host_name** 값, 그리고 작업 일정을 지정합니다. 이렇게 하면 지정된 파티션에 대해 매개 변수가 있는 스냅숏을 생성하는 작업이 만들어집니다. 자세한 내용은 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요.  
  
    > [!NOTE]  
    >  이 작업은 2단계에서 정의한 초기 스냅숏 작업과 동일한 Windows 계정을 사용하여 실행됩니다. 매개 변수가 있는 스냅숏 작업과 관련 데이터 파티션을 제거하려면 [sp_dropdynamicsnapshot_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)을 실행합니다.  
  
10. 게시 데이터베이스의 게시자에서 1단계의 **@publication** 값과 8단계의 **@suser_sname** 또는 **@host_name** 값을 지정하여 [sp_helpmergepartition&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)을 실행합니다. 결과 집합에서 **dynamic_snapshot_jobid** 값을 확인합니다.  
  
11. **msdb** 데이터베이스의 배포자에서 **@job_id**에 9단계에서 얻은 값을 지정하여 [sp_start_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)을 실행합니다. 이렇게 하면 파티션에 대한 매개 변수가 있는 스냅숏 작업이 시작됩니다.  
  
12. 8-11단계를 반복하여 각 구독에 대해 분할된 스냅숏을 생성합니다.  
  
#### <a name="to-create-a-publication-and-manually-create-snapshots-for-each-partition"></a>게시를 만들고 각 파티션에 대한 스냅숏을 수동으로 만들려면  
  
1.  [sp_addmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)을 실행하여 게시를 만듭니다. 자세한 내용은 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
2.  게시자에서 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)을 실행합니다. **@publication**에 1단계에서 사용된 게시 이름을, **@job_login** 및 **@password**에 스냅숏 에이전트를 실행하는 데 사용되는 Windows 자격 증명을 지정합니다. 게시자에 연결할 때 에이전트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하면 **@publisher_security_mode** @allow_subscriber_initiated_snapshot **@publisher_security_mode** 에 1단계에 사용된 게시 이름, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 **@publisher_login** 에 **@publisher_password**을 참조하세요. 이렇게 하면 게시에 대해 스냅숏 에이전트 작업이 만들어집니다. 초기 스냅숏을 생성하고 스냅숏 에이전트에 대한 사용자 지정 일정을 정의하는 방법은 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)를 참조하세요.  
  
    > [!IMPORTANT]  
    >  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
3.  [sp_addmergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행하여 게시에 아티클을 추가합니다. 이 저장 프로시저는 게시의 각 아티클에 대해 한 번씩만 실행해야 합니다. 매개 변수가 있는 필터를 사용할 경우 **@subset_filterclause** 매개 변수를 사용하여 하나 이상의 아티클에 대해 매개 변수가 있는 행 필터를 지정해야 합니다. 자세한 내용은 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
4.  다른 아티클이 매개 변수가 있는 행 필터에 따라 필터링되면 [sp_addmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)를 실행하여 아티클 간의 조인 또는 논리 레코드 관계를 정의합니다. 이 저장 프로시저는 정의되는 각 관계에 대해 한 번씩만 실행해야 합니다. 자세한 내용은 [병합 아티클 사이에서 조인 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)을 참조하세요.  
  
5.  스냅숏 작업을 시작하거나 명령 프롬프트에서 복제 스냅숏 에이전트를 실행하여 표준 스냅숏 스키마 및 그 밖의 파일을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
6.  명령 프롬프트에서 **-DynamicSnapshotLocation** 에 분할된 스냅숏의 위치를 지정하고 파티션을 정의하는 다음 속성을 하나 또는 모두 지정하고 복제 스냅숏 에이전트를 다시 실행하여 대량 복사(.bcp) 파일을 생성합니다.  
  
    -   **-DynamicFilterHostName** - [HOST_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md)이 사용되는 경우의 값  
  
    -   **-DynamicFilterLogin** - [SUSER_SNAME&#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md)이 사용되는 경우의 값  
  
7.  6단계를 반복하여 각 구독에 대해 분할된 스냅숏을 생성합니다.  
  
8.  다음 속성을 지정하고 각 구독에 대해 병합 에이전트를 실행하여 구독자에서 초기 분할된 스냅숏을 적용합니다.  
  
    -   **-Hostname** - HOST_NAME의 실제 값이 재정의되는 경우 파티션을 정의하는 데 사용되는 값  
  
    -   **-DynamicSnapshotLocation** - 이 파티션에 대한 동적 스냅숏의 위치  
  
> [!NOTE]  
>  복제 에이전트를 프로그래밍하는 방법에 대한 자세한 내용은 [복제 에이전트 실행 파일 개념](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 매개 변수가 있는 필터를 사용하여 구독자가 스냅숏 생성 프로세스를 시작하는 병합 게시를 만듭니다. **@job_login** 및 **@job_password** 값은 스크립팅 변수를 사용하여 전달됩니다.  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_1.sql)]  
  
 이 예에서는 매개 변수가 있는 필터를 사용하여 각 구독자가 [sp_addmergepartition](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md) 을 실행하여 파티션을 정의하고 [sp_adddynamicsnapshot_job](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md) 을 실행하여 필터링된 스냅숏 작업을 만들고 분할 정보를 전달하는 게시를 만듭니다. **@job_login** 및 **@job_password** 값은 스크립팅 변수를 사용하여 전달됩니다.  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_2.sql)]  
  
 이 예에서는 매개 변수가 있는 필터를 사용하여 각 구독자가 분할 정보를 제공함으로써 데이터 파티션과 필터링된 스냅숏 작업을 만들어야 하는 게시를 만듭니다. 구독자는 복제 에이전트를 수동으로 실행할 때 구독자가 명령줄 매개 변수를 사용하여 분할 정보를 제공합니다. 이 예에서는 이 게시에 대한 구독도 만들어졌다고 가정합니다.  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPartitionManual](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_3.sql)]  
  
```  
  
REM Line breaks are added to improve readability.   
REM In a batch file, commands must be made in a single line.  
REM Run the Snapshot agent from the command line to generate the standard snapshot   
REM schema and other files.   
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub% -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  
  
PAUSE  
  
```  
  
```  
  
REM Run the Snapshot agent from the command line, this time to generate   
REM the bulk copy (.bcp) data for each Subscriber partition.    
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
MD %SnapshotDir%  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub%  -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  -DynamicFilterHostName "adventure-works\Fernando"    
-DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
```  
  
REM Run the Merge Agent for each subscription to apply the partitioned   
REM snapshot for each Subscriber.    
SET Publisher = %computername%  
SET Subscriber = %computername%  
SET PubDB = AdventureWorks2012   
SET SubDB = AdventureWorks2012Replica   
SET PubName = AdvWorksSalesPersonMerge   
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE" -Publisher  %Publisher%    
-Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB %PubDB%    
-SubscriberDB %SubDB% -Publication %PubName%  -PublisherSecurityMode 1  -OutputVerboseLevel 3    
-Output -SubscriberSecurityMode 1  -SubscriptionType 3 -DistributorSecurityMode 1    
-Hostname "adventure-works\Fernando"  -DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 다음과 같이 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 분할된 스냅숏을 만들 수 있습니다.  
  
-   구독자가 처음 동기화될 때 스냅숏 생성 및 적용을 요청하도록 허용합니다.  
  
-   각 파티션에 대한 스냅숏을 미리 생성합니다.  
  
-   스냅숏 에이전트를 실행하여 각 구독자에 대한 스냅숏을 수동으로 생성합니다.  
  
> [!NOTE]  
>  병합 아티클을 만들 때 F:Microsoft.SqlServer.Replication.PartitionOptions.NonOverlappingSingleSubscription에 P:Microsoft.SqlServer.Replication.MergeArticle.PartitionOption 값을 지정하여 아티클을 필터링함으로써 구독별로 고유한 겹치지 않는 파티션을 생성하면 병합 에이전트를 실행할 때마다 메타데이터가 정리됩니다. 따라서 분할된 스냅숏은 더 빨리 만료됩니다. 이 옵션을 사용할 경우 구독자가 스냅숏 생성을 요청하도록 허용하는 것을 고려해야 합니다. 자세한 내용은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)항목의 "적절한 필터링 옵션 사용" 섹션을 참조하세요.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [Windows .NET Framework에서 제공하는](http://go.microsoft.com/fwlink/?LinkId=34733) 암호화 서비스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 사용합니다.  
  
#### <a name="to-create-a-publication-that-allows-subscribers-to-initiate-snapshot-generation-and-delivery"></a>구독자가 스냅숏 생성 및 배달을 시작하도록 허용하는 게시를 만들려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  게시 데이터베이스에 대해 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 클래스의 인스턴스를 만들고, 1단계에서 만든 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 인스턴스에 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 속성을 설정한 다음 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출합니다. If <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 에서 **false**를 반환하면 데이터베이스가 있는지 확인합니다.  
  
3.  If <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 속성이 **false**이면 **@allow_subscriber_initiated_snapshot** 로 설정한 후 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>을 참조하세요.  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 만들고 이 개체에 대해 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에서 1단계에서 만든 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>에 대한 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>에 대한 게시의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.MergePublication.MaxConcurrentDynamicSnapshots%2A>에 대해 실행할 최대 동적 스냅숏 작업 수. 구독자가 스냅숏 요청을 언제든지 시작할 수 있으므로 이 속성은 여러 구독자가 분할된 스냅숏을 동시에 요청할 경우 동시에 실행 가능한 스냅숏 에이전트 작업 수를 제한합니다. 최대 작업 수가 실행되고 있으면 새로 추가된 분할된 스냅숏 요청은 실행 중인 작업 중 하나가 완료될 때까지 지연됩니다.  
  
    -   비트 논리 OR 연산자(Visual C#의 경우**|** , Visual Basic의 경우 **Or** )를 사용하여 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowSubscriberInitiatedSnapshot> 에 값 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>을 참조하세요.  
  
    -   스냅숏 에이전트가 실행되는 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> Windows 계정에 대한 자격 증명을 제공하는 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 의 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 필드.  
  
        > [!NOTE]  
        >  **sysadmin** 고정 서버 역할의 멤버가 게시를 만들 때는 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>를 설정하는 것이 좋습니다. 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 메서드를 호출하여 게시를 만듭니다.  
  
    > [!IMPORTANT]  
    >  원격 배포자로 게시자를 구성할 경우 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>를 포함하여 모든 속성에 제공된 값이 일반 텍스트로 배포자에게 보내집니다. <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 메서드를 호출하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
6.  <xref:Microsoft.SqlServer.Replication.MergeArticle> 속성을 사용하여 게시에 아티클을 추가합니다. 매개 변수가 있는 필터를 정의하는 하나 이상의 아티클에 대해 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 속성을 지정합니다. 필요한 경우 아티클 간 조인 필터를 정의하는 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 개체를 만듭니다. 자세한 내용은 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
7.  <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 값이 **false**이면 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A>를 호출하여 이 게시에 대한 초기 스냅숏 에이전트 작업을 만듭니다.  
  
8.  4단계에서 만든 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 개체의 <xref:Microsoft.SqlServer.Replication.MergePublication> 메서드를 호출합니다. 그러면 초기 스냅숏을 생성하는 에이전트 작업이 시작됩니다. 초기 스냅숏을 생성하고 스냅숏 에이전트에 대한 사용자 지정 일정을 정의하는 방법은 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)를 참조하세요.  
  
9. (옵션) **@allow_subscriber_initiated_snapshot** 속성이 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 값인지 확인하여 초기 스냅숏을 사용할 준비가 되었는지 확인합니다.  
  
10. 구독자가 병합 에이전트에 처음으로 연결하는 경우에는 분할된 스냅숏이 자동으로 생성됩니다.  
  
#### <a name="to-create-a-publication-and-pregenerate-or-automatically-refresh-snapshots"></a>게시를 만들고 스냅숏을 미리 생성하거나 자동으로 새로 고치려면  
  
1.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 사용하여 병합 게시를 정의합니다. 자세한 내용은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> 속성을 사용하여 게시에 아티클을 추가합니다. 매개 변수가 있는 필터를 정의하는 하나 이상의 아티클에 대해 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 속성을 지정하고 아티클 간 조인 필터를 정의하는 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 개체를 만듭니다. 자세한 내용은 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
3.  <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A>의 값이 **false**이면 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A>를 호출하여 이 게시에 대한 스냅숏 에이전트 작업을 만듭니다.  
  
4.  4단계에서 만든 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 개체의 <xref:Microsoft.SqlServer.Replication.MergePublication> 메서드를 호출합니다. 그러면 초기 스냅숏을 생성하는 에이전트 작업이 시작됩니다. 초기 스냅숏을 생성하고 스냅숏 에이전트에 대한 사용자 지정 일정을 정의하는 방법은 [초기 스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)를 참조하십시오.  
  
5.  <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 속성이 **true** 값인지 확인하여 초기 스냅숏을 사용할 준비가 되었는지 확인합니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.MergePartition> 클래스의 인스턴스를 만들고 다음 두 속성 중 하나 또는 모두를 사용하여 구독자에 대한 매개 변수가 있는 필터링 조건을 설정합니다.  
  
    -   구독자의 파티션이 [SUSER_SNAME&#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md) 결과로 정의되는 경우 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A>을 사용합니다.  
  
    -   구독자의 파티션이 [HOST_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md) 결과 또는 이 함수의 오버로드 결과로 정의되는 경우 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A>을 사용합니다.  
  
7.  <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 클래스의 인스턴스를 만들고 6단계와 동일한 속성을 설정합니다.  
  
8.  <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> 클래스를 사용하여 구독자 파티션에 대한 필터링된 스냅숏을 생성할 일정을 정의합니다.  
  
9. 1단계에서 만든 <xref:Microsoft.SqlServer.Replication.MergePublication> 의 인스턴스를 사용하여 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergePartition%2A>을 호출합니다. 6단계에서 만든 <xref:Microsoft.SqlServer.Replication.MergePartition> 개체를 전달합니다.  
  
10. 1단계에서 만든 <xref:Microsoft.SqlServer.Replication.MergePublication> 의 인스턴스를 사용하여 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergeDynamicSnapshotJob%2A> 메서드를 호출합니다. 7단계에서 만든 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 개체 및 8단계에서 만든 <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> 개체를 전달합니다.  
  
11. <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergeDynamicSnapshotJobs%2A>를 호출하고 반환된 배열의 새로 추가된 분할된 스냅숏 작업에서 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 개체를 찾습니다.  
  
12. 작업의 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob.Name%2A> 속성을 가져옵니다.  
  
13. <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
14. 13단계에서 만든 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체를 전달하여 SMO(SQL Server 관리 개체) <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스의 인스턴스를 만듭니다.  
  
15. 14단계에서 만든 <xref:Microsoft.SqlServer.Management.Smo.Agent.Job> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Server.JobServer%2A> 속성 및 12단계에서 가져온 작업 이름을 전달하여 <xref:Microsoft.SqlServer.Management.Smo.Server> 클래스의 인스턴스를 만듭니다.  
  
16. <xref:Microsoft.SqlServer.Management.Smo.Agent.Job.Start%2A> 메서드를 호출하여 분할된 스냅숏 작업을 시작합니다.  
  
17. 구독자별로 6단계에서 16단계까지 반복합니다.  
  
#### <a name="to-create-a-publication-and-manually-create-snapshots-for-each-partition"></a>게시를 만들고 각 파티션에 대한 스냅숏을 수동으로 만들려면  
  
1.  <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스의 인스턴스를 사용하여 병합 게시를 정의합니다. 자세한 내용은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> 속성을 사용하여 게시에 아티클을 추가합니다. 매개 변수가 있는 필터를 정의하는 하나 이상의 아티클에 대해 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 속성을 지정하고 아티클 간 조인 필터를 정의하는 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 개체를 만듭니다. 자세한 내용은 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
3.  초기 스냅숏을 만듭니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
4.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 클래스의 인스턴스를 만들고 다음 필수 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - 게시자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - 게시의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - 배포자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - Windows 통합 인증을 사용하는 경우 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값 또는 SQL Server 인증을 사용하는 경우 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 값  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - Windows 통합 인증을 사용하는 경우 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 값 또는 SQL Server 인증을 사용하는 경우 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 값  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> 에 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>값을 설정합니다.  
  
6.  다음 속성 중 하나 이상을 설정하여 분할 매개 변수를 정의합니다.  
  
    -   구독자의 파티션이 [SUSER_SNAME&#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md) 결과로 정의되는 경우 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterLogin%2A>을 사용합니다.  
  
    -   구독자의 파티션이 [HOST_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md) 결과 또는 이 함수의 오버로드 결과로 정의되는 경우 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterHostName%2A>을 사용합니다.  
  
7.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 메서드를 호출합니다.  
  
8.  구독자별로 4단계에서 7단계까지 반복합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예제에서는 구독자에게 스냅숏 생성 요청을 허용하는 병합 게시를 만듭니다.  
  
 [!code-cs[HowTo#rmo_CreateMergePub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
 이 예제에서는 매개 변수가 있는 행 필터를 사용하여 병합 게시에 대한 구독자 파티션 및 필터링된 스냅숏을 수동으로 만듭니다.  
  
 [!code-cs[HowTo#rmo_CreateMergePartition](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepartition)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePartition](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepartition)]  
  
 이 예제에서는 매개 변수가 있는 행 필터를 사용하여 병합 게시에 구독자에 대한 필터링된 데이터 스냅숏을 수동으로 만듭니다.  
  
 [!code-cs[HowTo#rmo_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatefilteredsnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatefilteredsnapshot)]  
  
## <a name="see-also"></a>참고 항목  
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [매개 변수가 있는 필터를 사용하는 병합 게시의 스냅숏](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
