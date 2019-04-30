---
title: MSSQL_ENG014152 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014152 error
ms.assetid: 4215e2b1-cd30-441f-9671-9afc742adf6e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e14c0d724ba4832dfc0f67deec25308804b82f84
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191431"
---
# <a name="mssqleng014152"></a>MSSQL_ENG014152
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14152|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|복제-%s: 에이전트 %s이(가) 다시 시도하도록 예약되었습니다. %s|  
  
## <a name="explanation"></a>설명  
 지정한 복제 에이전트가 요청한 작업을 다시 시도하도록 예약되었습니다. 작업 단계에 대해 구성된 최대의 다시 시도 횟수에 도달할 때까지 프로세스는 계속해서 작업을 다시 시도합니다.  
  
 일반적으로 다시 시도는 다음 원인 중 하나로 인해 발생합니다.  
  
-   **QueryTimeout** 값이 초과되었습니다.  
  
-   **LoginTimeout** 값이 초과되었습니다.  
  
-   복제 프로세스가 교착 상태에서 처리되지 않았습니다.  
  
## <a name="user-action"></a>사용자 동작  
 사용자 동작은 다시 시도 메시지가 빈번하게 표시되는 경우에만 필요합니다.  
  
 [sp_help_jobstep](/sql/relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql) 을 사용하여, 지정한 복제 에이전트의 **에이전트 실행** 단계에서 다시 시도할 최대 횟수에 대한 현재 설정을 확인합니다. [sp_update_jobstep](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql) 저장 프로시저의 **@retry_attempts** 매개 변수를 사용하여 작업 단계에서 다시 시도하는 횟수를 조정할 수 있습니다.  
  
 다시 시도 메시지가 자주 표시되는 경우 다시 시도를 발생시키는 메시지를 기준으로 문제를 해결합니다. 다시 시도가 예약된 이유를 나타내는 메시지에 대한 에이전트 기록을 확인합니다. 경우에 따라 복제 에이전트에 대해 더 자세한 로깅을 설정해야 합니다. 복제에 대한 로깅을 구성하는 방법은 Microsoft 기술 자료 문서 [312292](https://support.microsoft.com/kb/312292)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
