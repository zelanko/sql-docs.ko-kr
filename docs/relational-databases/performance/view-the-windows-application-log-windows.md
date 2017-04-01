---
title: "Windows 응용 프로그램 로그 보기(Windows) | Microsoft Docs"
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
  - "로그 보기"
  - "응용 프로그램 로그 [SQL Server]"
  - "로그 [SQL Server], 응용 프로그램"
  - "Windows NT 응용 프로그램 로그 모니터링 [SQL Server]"
  - "Windows NT 응용 프로그램 로그 [SQL Server]"
  - "로그 표시"
  - "모니터링 [SQL Server], 이벤트"
  - "로그 [SQL Server], 보기"
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Windows 응용 프로그램 로그 보기(Windows)
  Windows 응용 프로그램 로그를 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 구성한 경우 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세션에서는 해당 로그에 새 이벤트를 씁니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와는 달리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 시작할 때마다 새 응용 프로그램 로그가 생성되지는 않습니다.  
  
### Windows 응용 프로그램 로그를 보려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, **관리 도구**를 차례로 가리킨 다음 **이벤트 뷰어**를 클릭합니다.  
  
2.  이벤트 뷰어에서 **응용 프로그램**을 클릭합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트는 **원본** 열에서 **MSSQLSERVER** 항목으로 식별됩니다(명명된 인스턴스는 **MSSQL$***<instance_name>*으로 식별됨). SQL Server 에이전트 이벤트는 SQLSERVERAGENT 항목으로 식별됩니다. 명명된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 이벤트는 **SQLAgent$**\<*instance_name*>으로 식별됩니다. Microsoft Search 서비스 이벤트는 **Microsoft Search**항목으로 식별됩니다.  
  
4.  다른 컴퓨터의 로그를 표시하려면 **이벤트 뷰어**를 마우스 오른쪽 단추로 클릭하고 **다른 컴퓨터에 연결**을 클릭한 다음 **컴퓨터 선택** 대화 상자에서 다른 컴퓨터를 선택합니다.  
  
5.  선택적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트만 표시하려면 **보기** 메뉴에서 **필터**를 클릭한 후 **이벤트 원본** 목록에서 **MSSQLSERVER**를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 이벤트만 표시하려면 **이벤트 원본** 목록에서 **SQLSERVERAGENT** 를 선택합니다.  
  
6.  이벤트에 대한 자세한 내용을 보려면 해당 이벤트를 두 번 클릭합니다.  
  
## 참고 항목  
 [SQL Server 오류 로그 보기&#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  