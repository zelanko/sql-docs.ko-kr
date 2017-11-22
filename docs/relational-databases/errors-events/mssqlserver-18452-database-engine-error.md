---
title: "MSSQLSERVER_18452 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 18456 (Database Engine error)
- 18452 (Database Engine error)
ms.assetid: 21da332c-e81d-4dee-a9d2-95598911b3be
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a1fa6d4d1a840341cd9a2bb26d330e1ed3146219
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver18452"></a>MSSQLSERVER_18452
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|18452|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LOGON_INVALID_CONNECT|  
|메시지 텍스트|사용자 '%.*ls'이(가) 로그인하지 못했습니다. SQL Server 로그인으로 Windows 인증과 함께 사용할 수 없습니다. %.\*ls|  
  
## <a name="explanation"></a>설명  
사용자가 유효성을 검사할 수 없는 자격 증명으로 로그인하려고 했습니다. 가능한 원인은 다음과 같습니다.  
  
-   로그인이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인일 수 있지만 서버에서 Windows 인증만 허용합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하려고 하고 있지만 사용된 로그인이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 없습니다.  
  
-   로그인이 Windows 인증을 사용할 수 있지만 인식할 수 없는 Windows 보안 주체입니다. 인식할 수 없는 Windows 보안 주체란 로그인을 Windows에서 확인할 수 없음을 의미합니다. 이는 Windows 로그인이 트러스트되지 않은 도메인에서 온 것이기 때문일 수 있습니다.  
  
유사한 문제가 덜 구체적인 오류 18456를 일으킬 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하려고 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 혼합 인증 모드로 구성되어 있는지 확인합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하려고 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 있는지 확인합니다.  
  
Windows 인증을 사용하여 연결하려고 하는 경우 올바른 도메인에 제대로 로그인되어 있는지 확인합니다.  
  
