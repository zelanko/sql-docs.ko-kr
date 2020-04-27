---
title: 큐 판독기 에이전트 보안 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.QRA.f1
helpviewer_keywords:
- Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 657116e00b6905964f8cc65c28dff383c3cc9ad0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63261689"
---
# <a name="queue-reader-agent-security"></a>큐 판독기 에이전트 보안
  **큐 판독기 에이전트 보안** 대화 상자를 사용하여 큐 판독기 에이전트가 실행 중이며 배포자에 로컬 연결을 설정하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정을 지정할 수 있습니다. 에이전트는 **게시자 속성** 대화 상자( **배포자 속성** 대화 상자에서 사용 가능)에서 지정한 계정을 사용하여 게시자에 연결하고, 구독에 대한 배포 에이전트와 동일한 컨텍스트를 사용하여 구독자에 연결합니다. 자세한 내용은 [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md)을(를) 참조하세요.  
  
 계정은 올바른 암호가 지정된 유효한 것이어야 합니다. 계정 및 암호의 유효성은 에이전트를 실행할 때 검사합니다.  
  
## <a name="options"></a>옵션  
 **프로세스 계정**  
 배포자에서 큐 판독기 에이전트가 실행되는 Windows 계정을 입력합니다. 지정한 Windows 계정은 적어도 배포 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
 **암호** 및 **암호 확인**  
 Windows 계정의 암호를 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제의 로그인 및 암호 관리](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [복제 에이전트 보안 모델](security/replication-agent-security-model.md)   
 [복제 에이전트 개요](agents/replication-agents-overview.md)   
 [복제 보안을 위한 최선의 구현 방법](security/replication-security-best-practices.md)  
  
  
