---
title: 게시 속성, 구독 옵션 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.subscriptionoptions.f1
ms.assetid: 31abd605-b273-419d-86df-d0ecf539a507
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e150652a335175dce388d7cd0f5c40a79e61391
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37352985"
---
# <a name="publication-properties-subscription-options"></a>게시 속성, 구독 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **게시 속성** 대화 상자의 **구독 옵션** 페이지를 사용하여 구독과 연결된 게시 수준 속성을 보고 설정할 수 있습니다. 속성은 다음 범주로 그룹화됩니다.  
  
-   모든 게시에 적용되는 속성  
  
-   스냅숏 및 트랜잭션 게시에 적용되는 속성(구독 업데이트를 허용하는 속성 포함)  
  
-   병합 게시에 적용되는 속성  
  
> [!NOTE]  
>  일부 속성은 읽기 전용입니다. 이 항목의 속성 설명에 그 이유가 설명되어 있습니다. 속성 변경 시 게시에 대한 새 스냅숏이 필요한 경우도 있고 모든 구독을 다시 초기화해야 하는 경우도 있습니다. 자세한 내용은 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
## <a name="options-for-all-publications"></a>모든 게시에 대한 옵션  
  
### <a name="creation-and-synchronization"></a>생성 및 동기화  
 **익명 구독 허용**  
 익명 끌어오기 구독을 허용할지 여부를 결정합니다. 익명 구독은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEWEd2005](../../includes/ssewed2005-md.md)], [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssMobileEd2005](../../includes/ssmobileed2005-md.md)]및 Windows CE용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 지원됩니다. 스냅숏 및 트랜잭션 게시에 대해 이 옵션을 사용하려면 **스냅숏을 항상 사용할 수 있음** 옵션을 **True**로 설정해야 합니다.  
  
 **연결할 수 있는 구독 데이터베이스**  
 구독 데이터베이스의 복사본을 연결하여 구독을 만들 수 있는지 여부를 결정합니다. 스냅숏 및 트랜잭션 게시의 경우 **스냅숏을 항상 사용할 수 있음** 옵션을 **True** 로 설정해야 합니다.  
  
> [!IMPORTANT]  
>  후속 릴리스에서는 연결할 수 있는 구독을 사용할 수 없습니다. 이 기능은 더 이상 사용되지 않습니다.  
  
 **끌어오기 구독 허용**  
 구독자가 이 게시에 대한 끌어오기 구독을 만들 수 있도록 허용할지 여부를 결정합니다. 자세한 내용은 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)을 참조하세요.  
  
### <a name="schema-replication"></a>스키마 복제  
 **스키마 변경 내용 복제**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당됩니다. 게시된 개체에 대한 스키마 변경 내용(예: 테이블에 열 추가 또는 열의 데이터 형식 변경)의 복제 여부를 결정합니다. 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
## <a name="options-for-snapshot-and-transactional-publications"></a>스냅숏 및 트랜잭션 게시에 대한 옵션  
  
### <a name="creation-and-synchronization"></a>생성 및 동기화  
 **독립 배포 에이전트**  
 이 데이터베이스의 다른 게시에 대해 독립적인 에이전트의 사용 여부를 결정합니다. 이 옵션은 읽기 전용입니다. 새 게시 마법사를 사용하여 만든 게시에 대해 이 옵션은 기본적으로 **True** 로 설정되어 있으며 게시를 만든 후에는 이를 변경할 수 없습니다. 자세한 내용은 [복제 에이전트 관리](../../relational-databases/replication/agents/replication-agent-administration.md)를 참조하세요.  
  
 **스냅숏을 항상 사용할 수 있음**  
 스냅숏 에이전트를 실행할 때마다 스냅숏 파일을 만들지 여부를 결정합니다( **독립 배포 에이전트**필요). 이 옵션은 읽기 전용입니다. 새 게시 마법사의 **스냅숏 에이전트** 페이지에서 **즉시 스냅숏을 만들고 구독 초기화에 사용할 수 있도록 유지합니다** (기본값)를 선택하면 이 옵션이 **True** 로 설정됩니다. 자세한 내용은 [스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-snapshot.md)을 참조하세요.  
  
 **백업 파일로 초기화 허용**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당됩니다. 백업 파일을 사용하여 구독을 초기화할 수 있도록 허용할지 여부를 결정합니다. 자세한 내용은 [스냅숏 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다.  
  
 **SQL Server 이외 구독자 허용**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당됩니다. 게시에서[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자를 지원할지 여부를 결정합니다. 이 옵션을 **True** 로 설정하면 다른 게시 속성도[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자를 지원하도록 설정됩니다. 구독이 있으면 이 옵션은 읽기 전용입니다. **즉시 업데이트 구독 허용** , **지연 업데이트 구독 허용**또는 **피어 투 피어 구독 허용**이 **True** 로 설정된 경우에는 이 옵션을 **True**로 설정할 수 없습니다. 자세한 내용은 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)을(를) 참조하세요.  
  
### <a name="data-transformation"></a>데이터 변환  
 **데이터 변환 허용**  
 데이터를 구독자에 배포하기 전에 DTS(데이터 변환 서비스)를 사용하여 변환할지 여부를 결정합니다. 이 옵션은 읽기 전용입니다. 저장 프로시저를 사용하여 게시를 만드는 경우에만 데이터 변환을 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  후속 릴리스에서는 변환 가능한 구독을 사용할 수 없습니다. 이 기능은 더 이상 사용되지 않습니다.  
  
### <a name="peer-to-peer-replication"></a>피어 투 피어 복제  
 **True**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 적용됩니다. 게시에서 피어 투 피어 복제를 지원할지 여부를 결정합니다. 이 옵션을 **True** 로 설정하면 다른 게시 속성도 피어 투 피어 복제를 지원하도록 설정됩니다. 구독이 있으면 이 옵션을 읽기 전용입니다. **즉시 업데이트 구독 허용** , **지연 업데이트 구독 허용** 또는 **SQL Server 이외 구독자 허용**이 **True** 로 설정된 경우에는 이 옵션을 **True**로 설정할 수 없습니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 **피어 투 피어 충돌 검색 허용**  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에만 적용됩니다. 이 게시에 대해 충돌 검색을 사용할지 여부를 지정합니다. 충돌 검색을 사용하려면 모든 노드에서 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전이 실행되어야 하고 모든 노드에 대해 충돌 검색을 사용하도록 설정되어 있어야 합니다. 충돌 검색을 사용하려면 **피어 송신자 ID**값도 지정해야 합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)을(를) 참조하세요.  
  
 **피어 송신자 ID**  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에만 적용됩니다. 피어 투 피어 토폴로지에 있는 노드의 ID를 지정합니다. 이 ID는 **피어 투 피어 충돌 검색 허용** 이 **True**로 설정된 경우 충돌 검색에 사용됩니다. 토폴로지에 사용되지 않은 0이 아닌 양수 ID를 지정합니다. 이미 사용된 ID 목록을 보려면 [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 시스템 테이블을 쿼리하십시오.  
  
### <a name="updatable-subscriptions"></a>업데이트할 수 있는 구독  
 **지연 업데이트 구독 허용**  
 구독자 변경 내용을 즉시 게시자로 복제할 수 있는지 여부를 결정합니다. 이 옵션은 읽기 전용입니다. 게시를 만들 때만 구독 업데이트를 설정할 수 있습니다. 자세한 내용은 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)을(를) 참조하세요.  
  
 **피어 투 피어 구독 허용**  
 구독자 변경 내용을 지연하고 나중에 게시자로 복제할 수 있는지 여부를 결정합니다. 이 옵션은 읽기 전용입니다. 게시를 만들 때만 구독 업데이트를 설정할 수 있습니다. 자세한 내용은 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)를 참조하세요.  
  
 **한 곳에서만 충돌 보고**  
 충돌하는 데이터 변경 내용을 게시자에서만 보고할 것인지, 아니면 게시자와 구독자 모두에서 보고할 것인지 여부를 결정합니다( **지연 업데이트 구독 허용**옵션 필요). 이 옵션은 읽기 전용입니다. 새 게시 마법사를 사용하여 만든 게시에 대해 이 옵션은 기본적으로 **True** 로 설정되어 있으며 게시를 만든 후에는 이를 변경할 수 없습니다. **True** 값은 게시자에서만 충돌이 보고됨을 의미합니다. 보고된 위치에서만 충돌을 볼 수 있습니다.  
  
 **충돌 해결 정책**  
 구독자 변경 내용이 게시자 변경 내용과 충돌할 때 수행할 동작을 지정합니다( **지연 업데이트 구독 허용**옵션 필요). 자세한 내용은 [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)을(를) 참조하세요.  
  
 **큐 유형**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐 또는 MSMQ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing)를 사용하여 게시자에 적용할 수 있을 때까지 구독자에서 변경 내용을 유지할지 여부를 결정합니다( **지연 업데이트 구독 허용**옵션 필요). 이 옵션은 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에만 적용됩니다. 그 이상 버전에서는 큐 서비스에 항상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 사용합니다.  
  
## <a name="options-for-merge-publications"></a>병합 게시에 대한 옵션  
  
### <a name="conflict-reporting"></a>충돌 보고  
 **한 곳에서만 충돌 보고**  
 충돌하는 데이터 변경 내용을 게시자에서만 보고할 것인지, 아니면 게시자와 구독자 모두에서 보고할 것인지 여부를 결정합니다. 이 옵션은 읽기 전용입니다. 새 게시 마법사를 사용하여 만든 게시에 대해 이 옵션은 기본적으로 **True** 로 설정되어 있으며 게시를 만든 후에는 이를 변경할 수 없습니다. **True** 값은 게시자에서만 충돌이 보고됨을 의미합니다. 보고된 위치에서만 충돌을 볼 수 있습니다. 자세한 내용은 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)의 "충돌 보기" 섹션을 참조하십시오.  
  
### <a name="filtering"></a>필터링  
 **매개 변수가 있는 필터 허용**  
 게시에서 매개 변수가 있는 필터를 사용하는지 여부에 따라 설정됩니다. 이 옵션은 항상 읽기 전용입니다. 자세한 내용은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)을(를) 참조하세요.  
  
 **구독자 유효성 검사**  
 구독자에 올바른 데이터 파티션이 있는지를 검사할 때 사용할 함수를 결정합니다. 값이 여러 개 있으면 쉼표로 구분합니다. 자세한 내용은 [병합 구독자의 파티션 정보 유효성 검사](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md)를 참조하세요.  
  
 **파티션 미리 계산**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당됩니다. 각 파티션에 속하는 데이터 행을 미리 계산하여 동기화를 최적화할지 여부를 결정합니다. 게시가 사전 계산 파티션 기준을 만족하면 이 설정은 기본적으로 **True** 로 지정됩니다. 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.  
  
 **동기화 최적화**  
 각 구독자에서 추가 메타데이터를 저장하여 병합 처리를 최적화할지 여부를 결정합니다. 이 최적화보다 사전 계산 파티션이 우선합니다. **동기화 최적화** 옵션은 **파티션 미리 계산** 이 **False**로 설정된 경우에만 적용됩니다. 자세한 내용은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)을(를) 참조하세요.  
  
### <a name="merge-processes"></a>병합 프로세스  
 **동시 프로세스 제한**  
 동시에 실행할 수 있는 병합 에이전트 수의 제한 여부를 결정합니다. 이 옵션은 일반적으로 게시에 동시 동기화가 가능한 밀어넣기 구독의 수가 많은 경우에 사용됩니다.  
  
 **최대 동시 프로세스 수**  
 동시에 실행될 수 있는 최대 병합 에이전트 수입니다( **동시 프로세스 제한**필요). 동기화 중인 에이전트 수가 이 최대값을 초과하면 개수가 최대값 밑으로 감소할 때까지 에이전트가 큐에 저장됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
