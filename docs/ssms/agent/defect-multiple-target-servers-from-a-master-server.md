---
title: "마스터 서버에서 여러 대상 서버 제거 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
- multiple target server defections
ms.assetid: 61a3713b-403a-4806-bfc4-66db72ca1156
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4cadf25cf9cbf3d86662fede814c327df2f85351
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="defect-multiple-target-servers-from-a-master-server"></a>Defect Multiple Target Servers from a Master Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]를 사용하여 다중 서버 관리 구성에서 여러 대상 서버를 제거하는 방법에 대해 설명합니다. 이 절차는 마스터 서버에서 실행하십시오.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-defect-multiple-target-servers-from-a-master-server"></a>마스터 서버에서 다중 대상 서버를 제거하려면  
  
1.  **개체 탐색기**에서 마스터 서버로 구성된 서버를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭하고 **다중 서버 관리**를 가리킨 다음 **대상 서버 관리**를 클릭합니다.  
  
3.  **명령 게시**를 클릭하고 **명령 유형** 목록에서 **제거**를 선택합니다.  
  
4.  **받는 사람**에서 다음 중 하나를 수행합니다.  
  
    -   이 마스터 서버의 모든 대상 서버를 제거하려면 **모든 대상 서버** 를 클릭합니다. 현재 다중 서버 관리 구성을 완전히 제거하려면 이 옵션을 사용합니다.  
  
    -   이 마스터 서버의 모든 대상 서버가 아닌 일부 대상 서버를 제거하려면 **대상 서버 지정**을 클릭한 다음 해당 **선택** 상자를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
[다중 서버 환경 만들기](../../ssms/agent/create-a-multiserver-environment.md)  
[기업 내 관리 자동화](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Defect a Target Server from a Master Server](../../ssms/agent/defect-a-target-server-from-a-master-server.md)  
  
