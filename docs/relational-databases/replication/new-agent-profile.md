---
description: 새 에이전트 프로필
title: 새 에이전트 프로필 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 5abca0ca89a446939f21b1501b22d14e4f7cef64
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469044"
---
# <a name="new-agent-profile"></a>새 에이전트 프로필
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **새 에이전트 프로필** 대화 상자를 사용하여 새 프로필을 만들 수 있습니다. 새 프로필은 항상 기존 프로필에 기반하지만 이를 애플리케이션 요구 사항에 맞게 수정할 수 있습니다. 만든 프로필은 **에이전트 프로필** 대화 상자에서 기존 및 후속 에이전트 작업에 적용할 수 있습니다. 에이전트 매개 변수 값은 \<**AgentProfileName> 속성** 대화 상자에서 편집할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **이름**  
 프로필의 이름을 입력합니다.  
  
 **설명**  
 프로필에 대한 설명을 입력합니다.  
  
 **매개 변수**  
 프로필에 포함된 에이전트 매개 변수입니다. 새 프로필의 기반으로 사용한 프로필이 반드시 각 매개 변수에 대해 값을 지정하는 것은 아닙니다. 지정한 에이전트에 유효한 모든 매개 변수를 보려면 **이 프로필에서 사용되는 매개 변수만 표시** 확인란의 선택을 취소합니다. 각 매개 변수에 대한 설명은 다음을 참조하십시오.  
  
-   [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [복제 로그 판독기 에이전트](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Replication Queue Reader Agent](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
 **기본값**  
 각 에이전트 매개 변수의 기본값입니다.  
  
 **값**  
 새 프로필의 기반으로 사용한 프로필의 매개 변수에 대해 지정한 값입니다. 변경하려는 매개 변수 값으로 이 필드를 편집합니다.  
  
 **이 프로필에서 사용되는 매개 변수만 표시**  
 지정한 에이전트에 유효한 모든 매개 변수를 표시하려면 선택을 취소합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 프로필 작업](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [복제 에이전트 프로필](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
