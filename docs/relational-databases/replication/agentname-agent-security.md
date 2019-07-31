---
title: '&lt;AgentName&gt; 에이전트 보안 | Microsoft 문서'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.agentnameagentsecurity.f1
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4eb95e374ee4fa31dca4bf6348baf543e4c9fdd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085980"
---
# <a name="ltagentnamegt-agent-security"></a>&lt;AgentName&gt; 에이전트 보안
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **\<AgentName&gt; 에이전트 보안** 페이지를 사용하여 배포 에이전트(트랜잭션 및 스냅샷 복제의 경우) 또는 병합 에이전트(병합 복제의 경우)를 실행하고 복제 토폴로지의 컴퓨터에 연결하는 계정을 지정할 수 있습니다. 에이전트에 필요한 사용 권한 및 복제 보안을 위한 최선의 구현 방법은 [Replication Agent Security Model(복제 에이전트 보안 모델)](../../relational-databases/replication/security/replication-agent-security-model.md) 및 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)(복제 보안 모범 사례)를 참조하세요.  
  
## <a name="options"></a>옵션  
 각 구독자에 대한 행의 속성 단추 ( **...** )를 클릭하여 **배포 에이전트 보안** 또는 **병합 에이전트 보안** 대화 상자에 액세스합니다. 해당 에이전트에서 사용하는 계정에 필요한 사용 권한에 대한 자세한 내용을 보려면 대화 상자에서 **도움말** 을 클릭합니다.  
  
 대화 상자에서 설정을 입력하면 구독자에 대한 연결 정보가 표에 표시됩니다.  
  
 **구독자 에이전트**  
 각 구독자의 이름입니다.  
  
 **배포자에 대한 연결**  
 트랜잭션 및 스냅샷 복제에 대해 표시됩니다. 배포자에 대한 연결이 설정되는 컨텍스트입니다. 로컬 연결은 항상 에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정의 컨텍스트를 사용하여 설정됩니다.  
  
-   밀어넣기 구독의 경우 로컬 연결은 배포자에 대한 연결이므로 이 필드는 항상 푸시 구독에 대한 **Impersonate '\<Domain>\\<Login\>'** 또는 **Impersonate '\<Computer>\\<Login\>'** 을 표시합니다.  
  
-   끌어오기 구독의 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 컨텍스트로 연결할 수도 있습니다. 이 필드는 **Use login '\<Login>'** , **Impersonate '\<Domain>\\<Login\>'** 또는 **Impersonate '\<Computer>\\<Login\>'** 중 하나를 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 Windows 계정의 컨텍스트를 사용하여 모든 연결을 설정할 것을 권장합니다.  
  
 **게시자 및 배포자에 연결**  
 병합 복제에 대해 표시됩니다. 게시자 및 배포자에 대한 연결이 설정되는 컨텍스트입니다. 로컬 연결은 항상 에이전트가 실행되는 Windows 계정의 컨텍스트를 사용하여 설정됩니다.  
  
-   밀어넣기 구독의 경우 로컬 연결은 게시자 및 배포자에 대한 연결이므로 이 필드는 항상 푸시 구독에 대한 **Impersonate '\<Domain>\\<Login\>'** 또는 **Impersonate '\<Computer>\\<Login\>'** 을 표시합니다.  
  
-   끌어오기 구독의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 컨텍스트로 연결할 수도 있습니다. 이 필드는 **Use login '\<Login>'** , **Impersonate '\<Domain>\\<Login\>'** 또는 **Impersonate '\<Computer>\\<Login\>'** 중 하나를 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 Windows 계정의 컨텍스트를 사용하여 모든 연결을 설정할 것을 권장합니다.  
  
 **구독자에 대한 연결**  
 구독자에 대한 연결이 설정되는 컨텍스트입니다. 로컬 연결은 항상 에이전트가 실행되는 Windows 계정의 컨텍스트를 사용하여 설정됩니다.  
  
-   끌어오기 구독의 경우 로컬 연결은 구독자에 대한 연결이므로 이 필드는 항상 푸시 구독에 대한 **Impersonate '\<Domain>\\<Login\>'** 또는 **Impersonate '\<Computer>\\<Login\>'** 을 표시합니다.  
  
-   밀어넣기 구독의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 컨텍스트로 연결할 수도 있습니다. 이 필드는 **Use login '\<Login>'** , **Impersonate '\<Domain>\\<Login\>'** 또는 **Impersonate '\<Computer>\\<Login\>'** 중 하나를 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 Windows 계정의 컨텍스트를 사용하여 모든 연결을 설정할 것을 권장합니다.  
  
## <a name="see-also"></a>참고 항목  
 [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [밀어넣기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [복제에 대한 ID 및 액세스 제어](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [복제 보안 설정 보기 및 수정](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
