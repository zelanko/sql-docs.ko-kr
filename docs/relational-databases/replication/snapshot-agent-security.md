---
title: "스냅숏 에이전트 보안 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.security.SSA.f1
helpviewer_keywords: Snapshot Agent Security dialog box
ms.assetid: 64e84c67-acc6-4906-98d4-3451767363fe
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e2f5d2ba5897a96ee89941eef26c7e37f73bf86
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="snapshot-agent-security"></a>스냅숏 에이전트 보안
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] **스냅숏 에이전트 보안** 대화 상자를 사용하여 다음을 지정할 수 있습니다.  
  
-   배포자에서 스냅숏 에이전트를 실행하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정. Windows 계정으로 에이전트 프로세스가 실행되기 때문에 이 계정을 *프로세스 계정*이라고도 합니다.  
  
-   스냅숏 에이전트를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 연결하는 컨텍스트. Windows 계정을 가장하거나 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정의 컨텍스트에서 연결을 설정할 수 있습니다.  
  
    > [!NOTE]  
    >  게시자 및 배포자가 동일한 컴퓨터에 있는 경우에도 스냅숏 에이전트를 게시자에 연결합니다. 또한 스냅숏 에이전트를 배포자에 연결하며 이러한 연결은 항상 에이전트를 실행하는 Windows 계정을 가장하여 설정됩니다.  
  
     Oracle 게시자의 경우 **배포자 속성** 대화 상자에서 사용할 수 있는 **게시자 속성** 대화 상자에서 스냅숏 에이전트를 게시자에 연결하는 컨텍스트를 지정합니다. 자세한 내용은 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)을(를) 참조하세요.  
  
 모든 계정이 유효해야 하며 각 계정에 대해 올바른 암호를 지정해야 합니다. 계정 및 암호의 유효성은 에이전트를 실행할 때 검사합니다.  
  
## <a name="options"></a>옵션  
 **Process account**  
 배포자에서 스냅숏 에이전트를 실행하는 Windows 계정을 입력합니다. 지정하는 Windows 계정은 다음과 같은 조건을 갖추어야 합니다.  
  
-   적어도 배포 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
-   스냅숏 공유에 대해 쓰기 권한이 있어야 합니다.  
  
 **암호** 및 **암호 확인**  
 Windows 계정의 암호를 입력합니다.  
  
 **게시자에 연결**  
 스냅숏 에이전트를 게시자에 연결할 때 **프로세스 계정** 입력란에 지정한 계정을 가장할지, 아니면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용할지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용하도록 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 암호를 입력합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용하는 것보다 Windows 계정을 가장하도록 선택하는 것이 좋습니다.  
  
 연결에 사용되는 Windows 계정이나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정은 적어도 게시 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제의 로그인 및 암호 관리](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
