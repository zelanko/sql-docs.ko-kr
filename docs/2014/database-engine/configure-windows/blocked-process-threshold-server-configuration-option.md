---
title: blocked process threshold 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- thresholds [SQL Server]
- blocked process threshold option
ms.assetid: 3d46d143-bc6a-4220-8b55-6baa37547c25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3901c87ebc217427e8d48f1cd299ba6831fa93b3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148693"
---
# <a name="blocked-process-threshold-server-configuration-option"></a>blocked process threshold 서버 구성 옵션
  **blocked process threshold** 옵션을 사용하여 차단된 프로세스 보고서가 생성되는 임계값을 초 단위로 지정할 수 있습니다. 0에서 86,400 사이의 임계값을 설정할 수 있습니다. 기본적으로 차단된 프로세스 보고서는 생성되지 않습니다. 시스템 태스크 또는 검색할 수 있는 교착 상태를 생성하지 않는 리소스를 기다리는 태스크의 경우 이 이벤트가 생성되지 않습니다.  
  
 이 이벤트가 생성되면 실행할 [경고](../../ssms/agent/alerts.md) 를 정의할 수 있습니다. 예를 들어 적절한 동작을 수행하여 차단 상황을 처리하도록 관리자를 페이징할 수 있습니다.  
  
 차단된 프로세스 임계값은 교착 상태 모니터 백그라운드 스레드를 사용하여 구성된 임계값보다 길거나 이 임계값의 배수인 시간 동안 대기하는 태스크 목록을 검토합니다. 차단된 각 태스크의 보고 간격마다 한 번씩 이벤트가 생성됩니다.  
  
 차단된 프로세스 보고서는 최상의 노력을 기반으로 생성됩니다. 반드시 실시간으로 보고하거나 거의 실시간으로 보고하는 것은 아닙니다.  
  
 이 설정은 서버를 중지했다가 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `blocked process threshold` 를 `20` 초로 설정하여 차단된 태스크마다 차단된 프로세스 보고서가 생성되도록 합니다.  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 20 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Blocked Process Report 이벤트 클래스](../../relational-databases/event-classes/blocked-process-report-event-class.md)  
  
  
