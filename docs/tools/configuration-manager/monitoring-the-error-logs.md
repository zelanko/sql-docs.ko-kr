---
title: "오류 로그 모니터링 | Microsoft Docs"
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
  - "로그 [SQL Server]"
  - "데이터베이스 성능 [SQL Server], 오류"
  - "Windows 응용 프로그램 로그 [SQL Server]"
  - "성능 모니터링 [SQL Server], 오류"
  - "서버 성능 [SQL Server], 오류"
  - "오류 및 응용 프로그램 로그 출력 비교"
  - "오류 [SQL Server], 로그"
  - "데이터베이스 튜닝 [SQL Server], 오류"
  - "데이터베이스 모니터링 [SQL Server], 오류"
  - "SQL Server 오류 로그"
  - "로그 [SQL Server], SQL Server 오류 로그"
  - "오류 로그 [SQL Server]"
  - "로그 [SQL Server], Windows 응용 프로그램 로그"
ms.assetid: e250336b-0695-44f6-a42f-23222f94e377
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 오류 로그 모니터링
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 특정 시스템 이벤트와 사용자 정의 이벤트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 응용 프로그램 로그에 기록합니다. 두 가지 로그 모두 모든 기록된 이벤트에 자동으로 타임스탬프를 남깁니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 있는 정보를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련된 문제를 해결할 수 있습니다.  
  
 Windows 응용 프로그램 로그에서 Windows 운영 체제 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 발생하는 이벤트의 전체적인 모습을 볼 수 있습니다. Windows 이벤트 뷰어를 사용하여 Windows 응용 프로그램 로그를 보고 정보를 필터링할 수 있습니다. 예를 들어 정보, 경고, 오류, 성공 감사 및 실패 감사와 같은 이벤트들을 필터링할 수 있습니다.  
  
## 오류와 응용 프로그램 로그 출력 비교  
 문제의 원인을 확인하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 Windows 응용 프로그램 로그를 모두 사용할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그를 모니터링할 때 원인을 알 수 없는 오류 메시지가 표시될 수 있습니다. 이 경우 두 로그 간의 이벤트에 대한 날짜와 시간을 비교하면 가능한 원인 목록을 좁혀 갈 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 로그 파일 뷰어를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 및 Windows 로그를 단일 목록으로 통합할 수 있어 관련된 서버 이벤트와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트를 쉽게 이해할 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서의 "로그 파일 뷰어" 항목을 참조하십시오.  
  
## 섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[SQL Server 오류 로그 보기](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 및 이 로그를 보는 방법에 대해 설명합니다.|  
|[Windows 응용 프로그램 로그 보기](../../tools/configuration-manager/viewing-the-windows-application-log.md)|Windows 응용 프로그램 로그 및 이 로그를 보는 방법에 대해 설명합니다.|  
  
  