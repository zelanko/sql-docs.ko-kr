---
title: "Agent XPs 서버 구성 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Agent XPs option
- extended stored procedures [SQL Server], SQL Server Agent
ms.assetid: 2e1c6c64-5ce7-4357-98c7-ac7763a9f9de
caps.latest.revision: "24"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0abd44bb6bfd0d8cf20525c6a0d6e9ee55b20bde
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="agent-xps-server-configuration-option"></a>Agent XPs 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **Agent XPs** 옵션을 사용하여 이 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 확장 저장 프로시저를 설정할 수 있습니다. 이 옵션을 해제하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 탐색기에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에이전트 노드를 사용할 수 없습니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 도구를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 시작하면 이러한 확장 저장 프로시저가 자동으로 설정됩니다. 자세한 내용은 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 상태에 관계없이 이러한 확장 저장 프로시저가 활성화되어 있지 않으면 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 노드의 콘텐츠를 표시하지 않습니다.  
  
 가능한 값은 아래와 같습니다.  
  
-   **0**은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 확장 저장 프로시저를 사용할 수 없음을 나타냅니다(기본값).  
  
-   **1**은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 확장 저장 프로시저를 사용할 수 있음을 나타냅니다.  
  
 이 설정은 서버를 중지했다가 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="example"></a>예제
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 확장 저장 프로시저를 설정합니다.  

1. Microsoft SQL Server Management Studio에서 데이터베이스 엔진에 연결합니다.

2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.

3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 
  
```sql 
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Agent XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [관리 태스크 자동화&#40;SQL Server 에이전트&#41;](http://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)   
 [SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  
  
