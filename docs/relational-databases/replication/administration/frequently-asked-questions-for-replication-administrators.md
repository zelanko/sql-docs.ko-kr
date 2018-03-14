---
title: "복제 관리자를 위한 질문과 대답 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administering replication, frequently asked questions
- replication [SQL Server], administering
ms.assetid: 5a9e4ddf-3cb1-4baf-94d6-b80acca24f64
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5324e1896067491c291d1c838ab787e4deb249f2
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="frequently-asked-questions-for-replication-administrators"></a>복제 관리자를 위한 질문과 대답
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  다음 질문과 대답은 복제 데이터베이스 관리자의 다양한 태스크에 대한 지침을 제공합니다.  
  
## <a name="configuring-replication"></a>복제 구성  
  
### <a name="does-activity-need-to-be-stopped-on-a-database-when-it-is-published"></a>작업을 게시할 때 데이터베이스에서 해당 작업을 중지해야 합니까?  
 아니요. 게시를 만드는 동안에도 데이터베이스에서 작업을 계속할 수 있습니다. 스냅숏을 생성하는 작업에는 리소스가 많이 사용될 수 있으므로 데이터베이스에 작업량이 적은 시간을 이용하여 스냅숏을 생성하는 것이 가장 좋습니다. 기본적으로 스냅숏은 새 게시 마법사를 완료하면 생성됩니다.  
  
### <a name="are-tables-locked-during-snapshot-generation"></a>스냅숏 생성 중에 테이블이 잠깁니까?  
 사용하는 복제 유형에 따라 잠금이 수행되는 기간이 달라집니다.  
  
-   병합 게시의 경우 스냅숏 에이전트는 잠금을 수행하지 않습니다.  
  
-   트랜잭션 게시의 경우 기본적으로 스냅숏 에이전트는 스냅숏 생성의 초기 단계에서만 잠금을 수행합니다.  
  
-   스냅숏 게시의 경우 스냅숏 에이전트는 전체 스냅숏 생성 프로세스 동안 잠금을 수행합니다.  
  
 잠금을 수행하면 다른 사용자가 테이블을 업데이트할 수 없기 때문에 특히 스냅숏 게시의 경우 데이터베이스에 작업량이 적을 때 스냅숏 에이전트가 실행되도록 예약해야 합니다.  
  
### <a name="when-is-a-subscription-available-when-can-the-subscription-database-be-used"></a>언제 구독을 사용할 수 있습니까? 구독 데이터베이스는 언제 사용할 수 있습니까?  
 스냅숏이 구독 데이터베이스에 적용된 다음에 구독을 사용할 수 있습니다. 그 전에도 구독 데이터베이스에 액세스할 수 있지만 스냅숏이 적용될 때까지 데이터베이스를 사용하면 안 됩니다. 다음과 같이 복제 모니터를 사용하여 스냅숏 생성 및 적용 상태를 확인합니다.  
  
-   스냅숏 에이전트에서 스냅숏을 생성한 다음 복제 모니터의 게시에 대한 **에이전트** 탭에서 스냅숏 생성 상태를 봅니다. 자세한 내용은 [게시 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)을 참조하세요.  
  
-   배포 에이전트 또는 병합 에이전트에서 스냅숏을 적용한 다음 복제 모니터의 **배포 에이전트** 또는 **병합 에이전트** 페이지에서 스냅숏 적용 상태를 봅니다. 자세한 내용은 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
### <a name="what-happens-if-the-snapshot-agent-has-not-completed-when-the-distribution-or-merge-agent-starts"></a>배포 에이전트나 병합 에이전트가 시작할 때 스냅숏 에이전트가 완료되지 않은 경우 문제가 발생합니까?  
 배포 에이전트나 병합 에이전트가 스냅숏 에이전트와 동시에 실행되면 오류가 발생하지 않습니다. 그러나 다음과 같은 사항에 유의하십시오.  
  
-   배포 에이전트나 병합 에이전트가 계속 실행되도록 구성된 경우 해당 에이전트는 스냅숏 에이전트가 완료된 다음 자동으로 스냅숏을 적용합니다.  
  
-   배포 에이전트나 병합 에이전트가 일정대로 또는 요청 시 실행되도록 구성된 경우 해당 에이전트가 실행될 때 사용 가능한 스냅숏이 없으면 아직 사용할 수 있는 스냅숏이 없다는 메시지와 함께 에이전트가 종료됩니다. 이 경우 스냅숏 에이전트가 완료된 다음 에이전트를 다시 실행하여 스냅숏을 적용해야 합니다. 에이전트 실행에 대한 자세한 내용은 [밀어넣기 구독 동기화](../../../relational-databases/replication/synchronize-a-push-subscription.md), [끌어오기 구독 동기화](../../../relational-databases/replication/synchronize-a-pull-subscription.md) 및 [복제 에이전트 실행 파일 개념](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
### <a name="should-i-script-my-replication-configuration"></a>복제 구성을 스크립팅해야 합니까?  
 예 복제 구성 스크립팅은 복제 토폴로지에 대한 모든 재해 복구 계획의 핵심입니다. 스크립링에 대한 자세한 내용은 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)을 참조하십시오.  
  
### <a name="what-recovery-model-is-required-on-a-replicated-database"></a>복제된 데이터베이스에는 어떤 복구 모델이 필요합니까?  
 복제는 단순 복구 모델, 대량 로그 복구 모델, 전체 복구 모델 중 어느 모델을 사용해도 제대로 작동합니다. 병합 복제는 메타데이터 테이블에 정보를 저장하여 변경 내용을 추적합니다. 트랜잭션 복제는 트랜잭션 로그를 표시하여 변경 내용을 추적하지만 이렇게 표시하는 프로세스는 복구 모델의 영향을 받지 않습니다.  
  
### <a name="why-does-replication-add-a-column-to-replicated-tables-will-it-be-removed-if-the-table-isnt-published"></a>복제 작업에서 복제된 테이블에 열을 추가하는 이유는 무엇입니까? 테이블이 게시되지 않으면 해당 열이 제거됩니까?  
 변경 내용을 추적하기 위해 병합 복제와 지연 업데이트 구독이 있는 트랜잭션 복제는 게시된 모든 테이블에 있는 모든 행을 고유하게 식별할 수 있어야 합니다. 이를 위해 다음 작업이 수행됩니다.  
  
-   테이블에 **ROWGUIDCOL** 속성이 설정된 **uniqueidentifier** 데이터 형식의 열이 없는 경우(있으면 이 열이 사용됨) 병합 복제는 모든 테이블에 **rowguid** 열을 추가합니다. 게시에서 테이블이 삭제되면 **rowguid** 열이 제거됩니다. 추적 작업에 기존 열이 사용되면 해당 열은 제거되지 않습니다.  
  
-   트랜잭션 게시가 지연 업데이트 구독을 지원하는 경우 복제가 모든 테이블에 **msrepl_tran_version** 열을 추가합니다. 게시에서 테이블을 삭제해도 **msrepl_tran_version** 열은 제거되지 않습니다.  
  
-   필터는 행 식별을 위해 복제에 사용된 **rowguidcol** 을 포함하지 않아야 합니다. 기본적으로 이 열은 병합 복제를 설정할 때 추가된 열이며 이름은 **rowguid**입니다.  
  
### <a name="how-do-i-manage-constraints-on-published-tables"></a>게시된 테이블에서 제약 조건을 어떻게 관리합니까?  
 게시된 테이블의 제약 조건에 대해 다음과 같은 사항에 유의하십시오.  
  
-   트랜잭션 복제에는 게시된 각 테이블에 대해 PRIMARY KEY 제약 조건이 필요합니다. 병합 복제에는 기본 키가 필요하지 않지만 있는 경우 복제되어야 합니다. 스냅숏 복제에는 기본 키가 필요하지 않습니다.  
  
-   기본적으로 PRIMARY KEY 제약 조건, 인덱스 및 CHECK 제약 조건은 구독자로 복제됩니다.  
  
-   FOREIGN KEY 제약 조건과 CHECK 제약 조건에 대해서는 NOT FOR REPLICATION 옵션이 기본적으로 지정됩니다. 이러한 제약 조건은 사용자 작업에는 적용되지만 에이전트 작업에는 적용되지 않습니다.  
  
 제약 조건 복제 여부를 제어하는 스키마 옵션 설정 방법은 [Specify Schema Options](../../../relational-databases/replication/publish/specify-schema-options.md)을 참조하십시오.  
  
### <a name="how-do-i-manage-identity-columns"></a>ID 열을 어떻게 관리합니까?  
 복제는 구독자에서의 업데이트 내용을 포함하는 복제 토폴로지에 대한 자동 ID 범위 관리를 제공합니다. 자세한 내용은 [ID 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
### <a name="can-the-same-objects-be-published-in-different-publications"></a>동일한 개체를 다른 여러 게시에 게시할 수 있습니까?  
 예. 하지만 몇 가지 제한 사항이 있습니다. 자세한 내용은 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md) 항목에서 "둘 이상의 게시에 테이블 게시" 섹션을 참조하세요.  
  
### <a name="can-multiple-publications-use-the-same-distribution-database"></a>여러 게시에서 동일한 배포 데이터베이스를 사용할 수 있습니까?  
 예 동일한 배포 데이터베이스를 사용할 수 있는 게시의 수나 유형에 대한 제한은 없습니다. 지정된 게시자의 모든 게시는 동일한 배포자와 배포 데이터베이스를 사용해야 합니다.  
  
 여러 게시가 있는 경우 여러 배포 데이터베이스 사이를 이동하는 데이터가 단일 게시의 데이터가 되도록 배포자에서 각 배포 데이터베이스를 구성할 수 있습니다. **배포자 속성** 대화 상자나 [sp_adddistributiondb&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)를 사용하여 배포 데이터베이스를 추가합니다. 이러한 대화 상자에 액세스하는 방법은 [배포자 및 게시자 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
### <a name="how-do-i-find-information-on-the-distributor-and-publisher-such-as-which-objects-in-a-database-are-published"></a>배포자와 게시자에 대한 정보, 즉 데이터베이스에서 어떤 개체가 게시되었는지 등과 같은 정보를 어떻게 찾습니까?  
 이러한 정보는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]와 여러 복제 저장 프로시저를 통해 얻을 수 있습니다. 자세한 내용은 [Distributor and Publisher Information Script](../../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)를 참조하세요.  
  
### <a name="does-replication-encrypt-data"></a>복제 작업에서 데이터를 암호화합니까?  
 아니요. 복제 작업에서는 데이터베이스에 저장되어 있거나 네트워크를 통해 전송되는 데이터를 암호화하지 않습니다. 자세한 내용은 [보안 개요&#40;복제&#41;](../../../relational-databases/replication/security/security-overview-replication.md) 항목의 "암호화" 섹션을 참조하세요.  
  
### <a name="how-do-i-replicate-data-over-the-internet"></a>인터넷을 통해 데이터를 어떻게 복제합니까?  
 다음을 사용하여 인터넷을 통해 데이터를 복제합니다.  
  
-   VPN(가상 사설망). 자세한 내용은 [VPN을 사용하여 인터넷을 통해 데이터 게시](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md)를 참조하세요.  
  
-   병합 복제를 위한 웹 동기화 옵션. 자세한 내용은 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)를 참조하세요.  
  
 모든 유형의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 시 VPN을 통해 데이터를 복제할 수 있지만 병합 복제를 사용할 경우 웹 동기화를 고려해야 합니다.  
  
### <a name="does-replication-resume-if-a-connection-is-dropped"></a>연결이 끊어진 경우 복제를 재개할 수 있습니까?  
 예 연결이 끊어지면 중단된 시점에서부터 복제 처리가 재개됩니다. 불안정한 네트워크에서 병합 복제를 사용하는 경우 관련 변경 내용이 한 단위로 처리되는 논리적 레코드를 사용해 보십시오. 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
### <a name="does-replication-work-over-low-bandwidth-connections-does-it-use-compression"></a>느린 대역폭 연결을 통해서도 복제를 수행할 수 있습니까? 복제 작업에서 압축을 사용합니까?  
 예. 느린 대역폭 연결을 통해서도 복제를 수행할 수 있습니다. TCP/IP를 통한 연결의 경우 복제는 프로토콜에서 제공하는 압축을 사용하지만 추가 압축은 제공하지 않습니다. HTTPS를 통한 웹 동기화 연결의 경우 복제는 프로토콜에서 제공하는 압축과 변경 내용을 복제하는 데 사용되는 XML 파일의 추가 압축도 사용합니다.  
  
## <a name="logins-and-object-ownership"></a>로그인 및 개체 소유권  
  
### <a name="are-logins-and-passwords-replicated"></a>로그인과 암호도 복제됩니까?  
 아니요. DTS 패키지를 만들어 한 게시자에서 하나 이상의 구독자로 로그인과 암호를 전송할 수 있습니다.  
  
### <a name="what-are-schemas-and-how-are-they-replicated"></a>스키마란 무엇이며 어떻게 복제됩니까?  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], *스키마* 는 다음 두 가지 의미를 갖습니다.  
  
-   CREATE TABLE 문과 같은 개체의 정의입니다. 기본적으로 복제는 복제된 모든 개체의 정의를 구독자로 복사합니다.  
  
-   개체가 만들어진 네임스페이스 \<Database>.\<Schema>.\<Object>입니다. 스키마는 CREATE SCHEMA 문을 사용하여 정의됩니다.  
  
-   복제는 새 게시 마법사에서 스키마 및 개체 소유권에 대해 기본적으로 다음과 같이 작동합니다.  
  
-   호환성 수준이 90 이상인 병합 게시, 스냅숏 게시, 트랜잭션 게시의 아티클에 대해 기본적으로 구독자의 개체 소유자는 게시자에 있는 해당 개체의 소유자와 동일합니다. 개체를 소유한 스키마가 구독자에 없으면 자동으로 생성됩니다.  
  
-   호환성 수준이 90 이하인 병합 게시의 아티클에 대해 기본적으로 소유자는 빈 상태였다가 구독자에서 개체를 생성하는 중에 **dbo** 로 지정됩니다.  
  
-   Oracle 게시의 아티클에 대해 기본적으로 소유자는 **dbo**로 지정됩니다.  
  
-   문자 모드 스냅숏([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자 및 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 구독자에 사용됨)을 사용하는 게시의 아티클에 대해 기본적으로 소유자는 빈 상태입니다. 소유자는 기본적으로 배포 에이전트 또는 병합 에이전트를 구독자에 연결하는 데 사용하는 계정과 연결된 소유자입니다.  
  
 개체 소유자는 **아티클 속성 - \<***Article***>** 대화 상자와 **sp_addarticle**, **sp_addmergearticle**, **sp_changearticle** 및 **sp_changemergearticle** 저장 프로시저를 통해 변경할 수 있습니다. 자세한 내용은 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), [아티클 정의](../../../relational-databases/replication/publish/define-an-article.md) 및 [아티클 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)을 참조하세요.  
  
### <a name="how-can-grants-on-the-subscription-database-be-configured-to-match-grants-on-the-publication-database"></a>구독 데이터베이스에 부여된 권한을 게시 데이터베이스에 부여된 권한과 일치시키려면 어떻게 해야 합니까?  
 기본적으로 복제는 구독 데이터베이스에서 GRANT 문을 실행하지 않습니다. 구독 데이터베이스에 대한 사용 권한을 게시 데이터베이스의 사용 권한과 일치시키려면 다음 방법 중 하나를 사용하십시오.  
  
-   구독 데이터베이스에서 직접 GRANT 문을 실행합니다.  
  
-   포스트 스냅숏 스크립트를 사용하여 해당 문을 실행합니다. 자세한 내용은 [스냅숏 적용 전후에 스크립트 실행](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)을 참조하세요.  
  
-   [sp_addscriptexec](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md) 저장 프로시저를 사용하여 해당 문을 실행합니다.  
  
### <a name="what-happens-to-permissions-granted-in-a-subscription-database-if-a-subscription-is-reinitialized"></a>구독을 다시 초기화하면 구독 데이터베이스에 부여된 사용 권한은 어떻게 됩니까?  
 기본적으로 구독이 다시 초기화되면 구독자의 개체가 삭제되고 다시 생성되므로 해당 개체에 부여된 모든 사용 권한도 삭제됩니다. 이러한 문제는 다음과 같이 처리할 수 있습니다.  
  
-   다시 초기화한 후 이전 섹션에서 설명한 기술을 사용하여 권한을 다시 적용합니다.  
  
-   구독을 다시 초기화할 때 해당 개체를 삭제하지 않도록 지정합니다. 다시 초기화하기 전에 다음 중 하나를 수행합니다.  
  
    -   [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 또는 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행할 때 **@property** 매개 변수에 'pre_creation_cmd'(**sp_changearticle**) 또는 'pre_creation_command'(**sp_changemergearticle**)를 지정하고 **@value** 매개 변수에 'none', 'delete' 또는 'truncate' 값을 지정합니다.  
  
    -   **아티클 속성 - \<Article>** 대화 상자의 **대상 개체** 섹션에서 **기존 개체를 변경하지 않고 유지**, **데이터를 삭제합니다. 아티클에 행 필터가 있으면 필터에 대응하는 데이터만 삭제합니다.** 또는 **기존 개체의 모든 데이터를 잘라냅니다.** 값을 **이름이 사용 중일 때 수행할 동작**를 참조하세요. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
## <a name="database-maintenance"></a>데이터베이스 유지 관리  
  
### <a name="why-cant-i-run-truncate-table-on-a-published-table"></a>게시된 테이블에서 TRUNCATE TABLE이 실행되지 않는 이유는 무엇입니까?  
 TRUNCATE TABLE은 트리거를 발생시키지 않는 로그되지 않은 작업입니다. 복제가 해당 작업으로 인한 변경 내용을 추적할 수 없으므로 TRUNCATE TABLE은 허용되지 않습니다. 트랜잭션 복제는 트랜잭션 로그를 통해 변경 내용을 추적하고 병합 복제는 게시된 테이블의 트리거를 통해 변경 내용을 추적합니다.  
  
### <a name="what-is-the-effect-of-running-a-bulk-insert-command-on-a-replicated-database"></a>복제된 데이터베이스에서 BULK INSERT 명령을 실행하면 어떻게 됩니까?  
 트랜잭션 복제의 경우 다른 삽입처럼 대량 삽입도 추적되어 복제됩니다. 병합 복제의 경우 변경 내용 추적 메타데이터를 적절하게 업데이트해야 합니다.  
  
### <a name="are-there-any-replication-considerations-for-backup-and-restore"></a>백업 및 복원에 대한 복제 고려 사항이 있습니까?  
 예 복제에 관련된 데이터베이스에 대해 특별히 고려해야 할 사항이 많이 있습니다. 자세한 내용은 [복제된 데이터베이스 백업 및 복원](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)을 참조하세요.  
  
### <a name="does-replication-affect-the-size-of-the-transaction-log"></a>복제가 트랜잭션 로그의 크기에 영향을 미칩니까?  
 병합 복제 및 스냅숏 복제는 트랜잭션 로그 크기에 영향을 주지 않지만 트랜잭션 복제는 영향을 줄 수 있습니다. 데이터베이스에 하나 이상의 트랜잭션 게시를 포함하는 경우 로그는 게시와 관련된 모든 트랜잭션이 배포 데이터베이스에 배달될 때까지 잘리지 않습니다. 로그 판독기 에이전트가 일정에 따라 실행되는 경우 트랜잭션 로그가 너무 방대해지면 일정 실행 간격을 좁히거나 일정이 연속 모드에서 실행되도록 설정하십시오. 연속 모드에서 실행되도록 설정(기본값)한 경우 로그 판독기 에이전트가 실행되고 있는지 확인하십시오. 로그 판독기 에이전트 상태 확인에 대한 자세한 내용은 [게시 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)을 참조하세요.  
  
 또한 게시 데이터베이스나 배포 데이터베이스에서 'sync with backup' 옵션을 설정한 경우 트랜잭션이 모두 백업될 때까지 트랜잭션 로그가 잘리지 않습니다. 이 옵션을 설정한 경우 트랜잭션 로그가 너무 방대해지면 트랜잭션 로그 백업 간격을 좁히십시오. 백업 및 트랜잭션 복제와 관련된 데이터베이스 복원에 대한 자세한 내용은 [스냅숏 및 트랜잭션 복제의 백업 및 복원을 위한 전략](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)을 참조하세요.  
  
### <a name="how-do-i-rebuild-indexes-or-tables-in-replicated-databases"></a>복제된 데이터베이스에서 인덱스나 테이블을 어떻게 다시 작성합니까?  
 인덱스를 다시 작성하는 메커니즘은 다양합니다. 이러한 메커니즘은 복제에 대한 특별한 고려 사항 없이 모두 사용 가능합니다. 한 가지 예외는 트랜잭션 게시의 테이블에는 기본 키가 필요하므로 이러한 테이블에서는 기본 키를 삭제하고 다시 만들 수 없다는 것입니다.  
  
### <a name="how-do-i-add-or-change-indexes-on-publication-and-subscription-databases"></a>게시 및 구독 데이터베이스에서 인덱스를 어떻게 추가하고 변경합니까?  
 복제에 대한 특별한 고려 사항 없이 인덱스를 게시자나 구독자에 추가할 수 있습니다. 그러나 인덱스는 성능에 영향을 미칠 수 있습니다. CREATE INDEX와 ALTER INDEX는 복제되지 않으므로 예를 들어 게시자에서 인덱스를 추가하거나 변경하는 경우 구독자에 이러한 내용을 반영하려면 구독자에서도 동일한 작업을 수행해야 합니다.  
  
### <a name="how-do-i-move-or-rename-files-for-databases-involved-in-replication"></a>복제에 관련된 데이터베이스의 파일은 어떻게 이동하며 이름은 어떻게 바꿉니까?  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서는 데이터베이스 파일을 이동하거나 이름을 바꾸려면 해당 데이터베이스를 분리하고 다시 연결해야 했습니다. 그러나 복제된 데이터베이스는 분리할 수 없으므로 먼저 이러한 데이터베이스에서 복제를 제거해야 했습니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터는 데이터베이스를 분리하거나 다시 연결하지 않고도 복제에 아무런 영향을 미치지 않으면서 파일을 이동하거나 이름을 바꿀 수 있습니다. 파일을 이동하고 이름을 바꾸는 방법은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
### <a name="how-do-i-drop-a-table-that-is-being-replicated"></a>복제 중인 테이블을 어떻게 삭제합니까?  
 먼저 [sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md), [sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) 또는 **게시 속성 - \<게시>** 대화 상자를 사용하여 게시에서 아티클을 삭제한 다음 `DROP <Object>`를 사용하여 데이터베이스에서 아티클을 삭제합니다. 구독이 추가된 후에는 스냅숏 또는 트랜잭션 게시에서 아티클을 삭제할 수 없습니다. 따라서 먼저 구독을 삭제해야 합니다. 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
### <a name="how-do-i-add-or-drop-columns-on-a-published-table"></a>게시된 테이블에서 열을 어떻게 추가하고 삭제합니까?  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 열 추가 및 삭제를 비롯하여 게시된 개체에 대한 다양한 스키마 변경을 수행할 수 있습니다. 예를 들어 게시자에서 ALTER TABLE ... DROP COLUMN을 실행하면 해당 문이 구독자로 복제된 다음 실행되어 해당 열을 삭제합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 를 실행하는 구독자는 [sp_repladdcolumn](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) 및 [sp_repldropcolumn](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md)저장 프로시저를 통해 열을 추가 및 삭제할 수 있습니다. 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
## <a name="replication-maintenance"></a>복제 유지 관리  
  
### <a name="how-do-i-determine-if-the-data-at-subscribers-is-synchronized-with-data-at-the-publisher"></a>구독자의 데이터가 게시자의 데이터와 동기화되었는지 어떻게 확인합니까?  
 유효성 검사를 사용합니다. 유효성 검사는 지정된 구독자가 게시자와 동기화되었는지 여부를 보고합니다. 자세한 내용은 [복제된 데이터의 유효성 검사](../../../relational-databases/replication/validate-replicated-data.md)를 참조하세요. 유효성 검사는 올바르게 동기화되지 않은 행이 있는 경우 해당 행에 대한 정보를 제공하지 않지만 [tablediff 유틸리티](../../../tools/tablediff-utility.md) 에서는 이러한 정보를 제공합니다.  
  
### <a name="how-do-i-add-a-table-to-an-existing-publication"></a>기존 게시에 어떻게 테이블을 추가합니까?  
 테이블이나 다른 개체를 추가하기 위해 게시 또는 구독 데이터베이스의 작업을 중지하지 않아도 됩니다. **게시 속성 - \<Publication>** 대화 상자나 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 및 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 저장 프로시저를 통해 게시에 테이블을 추가합니다. 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
### <a name="how-do-i-remove-a-table-from-a-publication"></a>게시에서 테이블을 어떻게 제거합니까?  
 먼저 [sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md), [sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) 또는 **게시 속성 - \<게시>** 대화 상자를 사용하여 게시에서 테이블을 제거합니다. 구독이 추가된 후에는 스냅숏 또는 트랜잭션 게시에서 아티클을 삭제할 수 없습니다. 따라서 먼저 구독을 삭제해야 합니다. 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
### <a name="what-actions-require-subscriptions-to-be-reinitialized"></a>구독을 다시 초기화해야 하는 동작에는 어떤 것이 있습니까?  
 일부 아티클 및 게시를 변경하면 구독을 다시 초기화해야 합니다. 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
### <a name="what-actions-cause-snapshots-to-be-invalidated"></a>스냅숏을 무효화하는 동작에는 어떤 것이 있습니까?  
 일부 아티클 및 게시를 변경하면 스냅숏이 무효화되어 새 스냅숏을 생성해야 합니다. 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
### <a name="how-do-i-remove-replication"></a>복제를 어떻게 제거합니까?  
 데이터베이스에서 복제를 제거하는 데 필요한 동작은 데이터베이스가 게시 데이터베이스 역할을 하는지 구독 데이터베이스 역할을 하는지 아니면 두 역할을 다 하는지에 따라 달라집니다.  
  
### <a name="how-do-i-determine-whether-there-are-transactions-or-rows-to-be-replicated"></a>복제할 트랜잭션이나 행이 있는지 여부를 어떻게 확인합니까?  
 트랜잭션 복제의 경우 저장 프로시저를 사용하거나 복제 모니터에서 **배포되지 않은 명령** 탭을 사용합니다. 자세한 내용은 [배포 데이터베이스의 복제된 명령 및 기타 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) 및 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
 병합 복제의 경우 **sp_showpendingchanges**저장 프로시저를 사용합니다. 자세한 내용은 [sp_showpendingchanges&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)를 참조하세요.  
  
### <a name="how-far-behind-is-the-distribution-agent-should-i-reinitialize"></a>배포 에이전트가 얼마나 오래 되었는지 어떻게 확인합니까? 다시 초기화해야 합니까?  
 **sp_replmonitorsubscriptionpendingcmds** 저장 프로시저를 사용하거나 복제 모니터에서 **배포되지 않은 명령** 탭을 사용합니다. 저장 프로시저와 탭에는 다음 내용이 표시됩니다.  
  
-   선택한 구독자에 배달되지 않은 배포 데이터베이스의 명령 수. 명령은 하나의 Transact-SQL DML(데이터 조작 언어) 문이나 하나의 DDL(데이터 정의 언어) 문으로 구성됩니다.  
  
-   명령을 구독자에 배달하는 데 걸리는 예상 시간. 이 값이 스냅숏을 생성하여 구독자에 적용하는 데 필요한 시간 값보다 더 큰 경우 구독자를 다시 초기화하십시오. 자세한 내용은 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
 자세한 내용은 [sp_replmonitorsubscriptionpendingcmds&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md) 및 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
## <a name="replication-and-other-database-features"></a>복제 및 기타 데이터베이스 기능  
  
### <a name="does-replication-work-in-conjunction-with-log-shipping-and-database-mirroring"></a>복제가 로그 전달 및 데이터베이스 미러링과 함께 작동합니까?  
 예 자세한 내용은 [로그 전달 및 복제&#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md) 및 [데이터베이스 미러링 및 복제&#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)를 참조하세요.  
  
### <a name="does-replication-work-in-conjunction-with-clustering"></a>복제가 클러스터링과 함께 작동합니까?  
 예 모든 데이터가 클러스터의 한 디스크 세트에 저장되므로 특별히 고려해야 할 사항은 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [관리&#40;복제&#41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
