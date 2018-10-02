---
title: 배포 에이전트 보안(피어 투 피어 복제) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.p2pwizard.DA.f1
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9ef946d202acb3400c4f60e964aa4aaf691f78f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687141"
---
# <a name="distribution-agent-security-peer-to-peer-replication"></a>배포 에이전트 보안(피어 투 피어 복제)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **배포 에이전트 보안** 페이지를 사용하여 배포 에이전트를 실행하고 피어 투 피어 토폴로지의 컴퓨터에 연결하는 계정을 지정할 수 있습니다. 에이전트에 필요한 사용 권한 및 복제 보안을 위한 최선의 구현 방법은 [Replication Agent Security Model(복제 에이전트 보안 모델)](../../relational-databases/replication/security/replication-agent-security-model.md) 및 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)(복제 보안 모범 사례)를 참조하세요.  
  
> [!NOTE]  
>  이전에 이 마법사를 실행하여 구독에 대한 배포 에이전트를 구성한 경우에는 해당 배포 에이전트에서 사용하는 자격 증명을 변경할 수 없습니다. 새 자격 증명을 지정하면 이 자격 증명은 무시됩니다. 자격 증명을 변경하려면 **구독 속성** 대화 상자를 사용하십시오. 자세한 내용은 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)을(를) 참조하세요.  
  
## <a name="options"></a>Options  
 각 구독자에 대한 행에서 속성 단추 (**...**)를 클릭하여 **배포 에이전트 보안** 대화 상자에 액세스합니다. 에이전트가 사용하는 계정에 필요한 사용 권한에 대한 자세한 내용을 보려면 시작한 **배포 에이전트 보안** 대화 상자에서 **도움말** 을 클릭합니다.  
  
 대화 상자에서 설정을 입력하면 구독자에 대한 연결 정보가 표에 표시됩니다.  
  
 **구독자 에이전트**  
 각 피어의 이름입니다.  
  
 **피어 데이터베이스**  
 게시 데이터베이스와 구독 데이터베이스 역할을 모두 수행하는 피어의 데이터베이스입니다.  
  
 **배포자에 대한 연결**  
 배포자에 대한 연결이 설정되는 컨텍스트입니다. 로컬 연결은 항상 에이전트를 실행하는 Windows 계정의 컨텍스트를 사용하여 설정됩니다. 이 마법사는 밀어넣기 구독을 생성하므로(로컬 연결은 배포자에 대한 연결임) 이 필드는 항상 **Impersonate '\<Domain>\\<Login\>'** 또는 **Impersonate '\<Computer>\\<Login\>'** 을 표시합니다.  
  
 **구독자에 대한 연결**  
 구독자에 대한 연결이 설정되는 컨텍스트입니다. 에이전트를 실행하는 Windows 계정의 컨텍스트 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 컨텍스트에서 연결을 설정할 수 있습니다. 이 필드는 **Use login '\<Login>'**, **Impersonate '\<Domain>\\<Login\>'** 또는 **Impersonate '\<Computer>\\<Login\>'** 중 하나를 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 Windows 계정의 컨텍스트를 사용하여 모든 연결을 설정할 것을 권장합니다.  
  
## <a name="see-also"></a>참고 항목  
 [피어 투 피어 토폴로지 관리&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [@loopback_detection](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
