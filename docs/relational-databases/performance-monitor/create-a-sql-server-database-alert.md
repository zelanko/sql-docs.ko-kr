---
title: "SQL Server 데이터베이스 경고 만들기 | Microsoft Docs"
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
  - "데이터베이스 성능 [SQL Server], 경고"
  - "경고 [SQL Server], 만들기"
  - "임계값 [SQL Server]"
  - "데이터베이스 경고 [SQL Server]"
  - "데이터베이스 튜닝 [SQL Server], 경고"
  - "성능 모니터링 [SQL Server], 경고"
  - "서버 성능 모니터링 [SQL Server], 경고"
  - "데이터베이스 모니터링 [SQL Server], 경고"
  - "서버 성능 [SQL Server], 경고"
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# SQL Server 데이터베이스 경고 만들기
  시스템 모니터를 사용하여 시스템 모니터 카운터의 임계값에 도달했을 때 발생하는 경고를 만들 수 있습니다. 시스템 모니터는 경고에 대한 응답으로 경고 조건을 처리하기 위해 쓰여진 사용자 지정 응용 프로그램과 같은 응용 프로그램을 시작합니다. 예를 들어 교착 상태 횟수가 지정한 값을 넘어설 때 발생할 경고를 만들 수 있습니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 경고를 정의할 수도 있습니다. 자세한 내용은 [경고](../../ssms/agent/alerts.md)를 참조하세요.  
  
 시스템 모니터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 경고를 설정하는 방법은 [SQL Server 데이터베이스 경고 설정&#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md)을 참조하세요.  
  
## 참고 항목  
 [sp_add_alert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo&#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  