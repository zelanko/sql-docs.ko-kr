---
title: "FT:Crawl Started 이벤트 클래스 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Crawl Started event class
ms.assetid: 2535b856-97e8-4fb2-8ba0-5d5446355fa6
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df5d03ee4b23beb694d0303cf79d479a112511d6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="ftcrawl-started-event-class"></a>FT:Crawl Started 이벤트 클래스
  **FT:Crawl Started** 이벤트 클래스는 전체 텍스트 탐색(채우기)을 시작했음을 나타냅니다. 이 이벤트 클래스를 사용하여 작업자 태스크에 의해 실제로 탐색 요청이 선택되는지 확인할 수 있습니다.  
  
## <a name="ft-crawl-started-event-class-data-columns"></a>FT: Crawl Started 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|전체 텍스트 탐색이 시작된 데이터베이스 ID입니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**EventClass**|**int**|이벤트 유형 = 155|27|아니요|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니요|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**ObjectID**|**int**|시스템이 할당한 개체의 ID입니다. 전체 텍스트 탐색은 이 개체의 전체 텍스트 인덱스에서 시작됩니다.|22|예|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 로그인이 모두 표시됩니다.|64|예|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**TextData**|**ntext**|전체 텍스트 탐색 형식입니다. 값은 전체, 증분, 수동 또는 자동이 될 수 있습니다.|1|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
