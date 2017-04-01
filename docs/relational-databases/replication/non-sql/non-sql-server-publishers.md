---
title: "SQL Server 이외 게시자 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "다른 유형의 데이터베이스 복제, SQL Server 이외 게시자"
  - "SQL Server 이외 게시자"
  - "다른 유형의 데이터 원본, SQL Server 이외 게시자"
  - "게시자 [SQL Server 복제], Oracle"
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# SQL Server 이외 게시자
  데이터를 게시 비[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 원본에서 데이터를 통합할 수 있습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 Oracle 데이터베이스에서 게시된 스냅숏 또는 트랜잭션 데이터를 구독할 수 있습니다. Oracle에서 게시에 대 한 자세한 내용은 참조 [Oracle 게시 개요](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)합니다.  
  
 SQL Server 이외의 구독자에 대한 다른 유형의 복제는 지원되지 않습니다. Oracle 게시는 지원되지 않습니다. 데이터를 이동하려면 변경 데이터 캡처 및 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]를 사용하여 솔루션을 만듭니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 데이터베이스에서 게시 작업은 다음과 같은 시나리오에서 유용합니다.  
  
|시나리오|설명|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 응용 프로그램 배포|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] 이외 데이터베이스에서 복제한 데이터 작업 시 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Visual Studio 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용하여 개발합니다.|  
|데이터 웨어하우징 준비 서버(staging server)|유지 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 아닌 동기화 준비 데이터베이스[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|로 마이그레이션 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|원본 시스템의 변경 내용을 복제하면서 실시간으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대한 응용 프로그램을 테스트합니다. 마이그레이션에 만족하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로 전환합니다.|  
  
## 참고 항목  
 [다른 유형의 데이터베이스 복제](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  