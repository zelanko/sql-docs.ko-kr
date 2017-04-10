---
title: "Trace File Close 이벤트 클래스 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Trace File Close 이벤트 클래스"
ms.assetid: 128b7bac-cb64-43e7-ae9b-87b7d2ebb4ef
caps.latest.revision: 31
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 31
---
# Trace File Close 이벤트 클래스
  **Trace File Close** 이벤트 클래스는 추적 파일 롤오버 중 추적 파일이 닫혔음을 나타냅니다.  
  
## Trace File Close 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**EventClass**|**int**|이벤트 유형 = 150|27|아니요|  
|**EventSequence**|**int**|이 추적에서 실행된 이 이벤트의 고유한 타임스탬프입니다. 이 번호는 실행된 각 이벤트에 따라 단순히 증가합니다.|51|아니요|  
|**FileName**|**nvarchar**|닫고 있는 추적 파일의 논리적 이름입니다.|36|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, NULL = 사용자 이 이벤트 클래스의 값은 항상 1입니다.|60|예|  
|**LoginName**|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다. 이 이벤트 클래스의 값은 항상 "sa"입니다.|11|예|  
|**ObjectID**|**int**|시스템이 할당한 추적 ID입니다.|22|예|  
|**ServerName**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
  
## 참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  