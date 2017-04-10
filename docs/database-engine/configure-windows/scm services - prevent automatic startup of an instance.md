---
title: "SQL Server 인스턴스의 자동 시작 방지(SQL Server 구성 관리자) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "자동 SQL Server 시작"
  - "SQL Server, 중지"
  - "SQL Server, 자동 시작"
  - "자동 시작 취소"
  - "SQL Server 중지"
  - "자동 시작 방지 [SQL Server]"
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# SQL Server 인스턴스의 자동 시작 방지(SQL Server 구성 관리자)
  이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스가 자동으로 시작되지 않도록 방지하는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 일반적으로 자동으로 시작되도록 구성됩니다. 인스턴스의 시작 모드를 수동으로 설정하면 이러한 구성을 변경할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### SQL Server 인스턴스의 자동 시작을 방지하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 최신 버전의 Windows에서 응용 프로그램으로 표시되지 않습니다.  
    >   
    >  -   **Windows 10**:  
    >          [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 열려면 **시작 페이지**에 SQLServerManager13.msc([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 경우)를 입력합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 경우 13을 더 작은 수로 바꿉니다. SQLServerManager13.msc를 클릭하면 구성 관리자가 열립니다. 구성 관리자를 시작 페이지나 작업 표시줄에 고정하려면 SQLServerManager13.msc를 마우스 오른쪽 단추로 클릭한 다음 **파일 위치 열기**를 클릭합니다. Windows 파일 탐색기에서 SQLServerManager13.msc를 마우스 오른쪽 단추로 클릭하고 **시작 화면에 고정** 또는 **작업 표시줄에 고정**을 클릭합니다.  
    > -   **Windows 8**:  
    >          [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 열려면 **검색** 참의 **앱**에 **SQLServerManager\<version>.msc**(예: **SQLServerManager13.msc**)를 입력한 다음 **Enter** 키를 누릅니다.  
  
2.  SQL Server 구성 관리자에서 **서비스**를 확장한 다음 **SQL Server**를 클릭합니다.  
  
3.  세부 정보 창에서 **MSSQLServer**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **SQL Server \<***instancename***> 속성** 대화 상자에서 **속성** 상자에 있는 **시작 모드**를 **수동**으로 설정합니다.  
  
5.  **확인**을 클릭하여 **SQL Server \<***instancename***> 속성** 대화 상자를 닫은 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자도 닫습니다.  
  
## 참고 항목  
 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)  
  
  