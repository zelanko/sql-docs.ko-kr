---
description: 에이전트 보안(새 게시 마법사)
title: 에이전트 보안(새 게시 마법사) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.agentsecurity.articles.f1
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 8a33a8a17aea4bddadb1c2ed99a4e5b1bcf1966b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460316"
---
# <a name="agent-security-new-publication-wizard"></a>에이전트 보안(새 게시 마법사)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **에이전트 보안** 페이지를 사용하여 다음 에이전트를 실행하고 복제 토폴로지의 컴퓨터에 연결할 때 사용되는 계정을 지정할 수 있습니다.  
  
-   모든 게시에 대한 스냅샷 에이전트입니다.  
  
-   모든 트랜잭션 게시에 대한 로그 판독기 에이전트입니다.  
  
-   업데이트할 수 있는 구독을 허용하는 트랜잭션 게시에 대한 큐 판독기 에이전트입니다. **게시 유형** 페이지에서 **업데이트할 수 있는 구독이 있는 트랜잭션 게시** 를 지정하면 사용하는 업데이트할 수 있는 구독 유형과 관계없이 이 에이전트에 대해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업이 생성됩니다. 업데이트할 수 있는 구독에 대한 자세한 내용은 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)을 참조하십시오.  
  
 에이전트에 필요한 사용 권한 및 복제 보안을 위한 최선의 구현 방법은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md) 및 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **스냅샷 에이전트**  
 모든 게시에 대해 표시됩니다. **보안 설정** 을 클릭하여 **스냅샷 에이전트 보안** 대화 상자에서 보안 설정을 지정할 수 있습니다.  
  
 스냅샷 에이전트에서 사용하는 계정에 필요한 사용 권한을 보려면 **스냅샷 에이전트 보안** 대화 상자에서 **도움말** 을 클릭합니다.  
  
 **로그 판독기 에이전트**  
 모든 트랜잭션 게시에 대해 표시됩니다. **보안 설정** 을 클릭하여 **로그 판독기 에이전트 보안** 대화 상자에서 보안 설정을 지정할 수 있습니다.  
  
 로그 판독기 에이전트에서 사용하는 계정에 필요한 사용 권한을 보려면 **로그 판독기 에이전트 보안** 대화 상자에서 **도움말** 을 클릭합니다.  
  
> [!NOTE]  
>  트랜잭션 복제를 사용하여 게시된 각 데이터베이스에 대해 하나의 로그 판독기 에이전트가 있습니다. 데이터베이스에 트랜잭션 게시가 이미 있으면 보안 설정은 읽기 전용입니다. **게시 속성** 대화 상자에서 설정을 변경할 수 있지만 이 변경 내용은 데이터베이스의 모든 트랜잭션 게시에 적용됩니다.  
  
 **큐 판독기 에이전트**  
 업데이트할 수 있는 구독을 허용하는 트랜잭션 게시에 대해 표시됩니다. **보안 설정** 을 클릭하여 **큐 판독기 에이전트 보안** 대화 상자에서 보안 설정을 지정할 수 있습니다. 이 마법사를 완료하면 큐 판독기 에이전트 작업이 생성됩니다. 지연 업데이트 구독의 생성 여부와는 관계가 없습니다. 지연 업데이트 구독을 만들지 않으려면 이 작업을 해제할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 **Jobs** 폴더에서 작업( *[\<Publisher>].\<integer>* . 형식의 이름)을 마우스 오른쪽 단추로 클릭한 다음 **사용 안 함** 을 클릭합니다.  
  
 큐 판독기 에이전트에서 사용하는 계정에 필요한 사용 권한을 보려면 **큐 판독기 에이전트 보안** 대화 상자에서 **도움말** 을 클릭합니다.  
  
> [!NOTE]  
>  각 배포 데이터베이스 및 이 데이터베이스에서 처리하는 모든 게시자에 대해 하나의 큐 판독기 에이전트가 있습니다. 지정된 배포 데이터베이스를 사용하는 게시자에 지연 업데이트 구독을 허용하는 트랜잭션 게시가 이미 있으면 보안 설정은 읽기 전용입니다. **배포자 속성** 대화 상자에서 큐 판독기 에이전트를 실행 및 연결할 때 사용되는 계정을 변경할 수 있지만 이 변경 내용은 해당 배포 데이터베이스를 사용하는 모든 게시자에서의 게시에 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [복제에 대한 ID 액세스 및 제어](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
