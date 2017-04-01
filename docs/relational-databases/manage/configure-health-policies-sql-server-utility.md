---
title: "상태 정책 구성(SQL Server 유틸리티) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 030aac3b-8901-4c41-91ed-aba96420276c
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# 상태 정책 구성(SQL Server 유틸리티)
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]유틸리티 대시보드를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스 및 데이터 계층 응용 프로그램의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 리소스 매개 변수를 볼 수 있습니다. 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 상태 정책 결과를 보려면 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 유틸리티 제어 지점에 연결합니다. 자세한 내용은 [유틸리티 탐색기를 사용하여 SQL Server 유틸리티 관리](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 상태 정책은 데이터 계층 응용 프로그램 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 대해 구성할 수 있습니다. 상태 정책은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 모든 데이터 계층 응용 프로그램 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 대해 전역으로 정의하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 각 데이터 계층 응용 프로그램 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 대해 개별적으로 정의할 수 있습니다.  
  
## 데이터 계층 응용 프로그램의 정책 모니터링  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 계층 응용 프로그램의 초과 사용 및 미달 사용 정책은 다음과 같습니다.  
  
-   데이터 계층 응용 프로그램 프로세서 사용률  
  
-   데이터베이스 파일을 위한 데이터 계층 응용 프로그램 파일 공간  
  
-   저장소 볼륨을 위한 데이터 계층 응용 프로그램 파일 공간  
  
-   컴퓨터 프로세서 사용률  
  
> [!NOTE]  
>  저장소 볼륨 및 프로세서 사용률은 데이터 계층 응용 프로그램의 읽기 전용 정책입니다.  
  
 데이터 계층 응용 프로그램의 전역 모니터링 정책을 보거나 변경하는 방법은 [유틸리티 관리&#40;SQL Server 유틸리티&#41;](../Topic/Utility%20Administration%20\(SQL%20Server%20Utility\).md)를 참조하세요.  
  
 개별 데이터 계층 응용 프로그램의 모니터링 정책을 보거나 변경하는 방법은 [배포된 데이터 계층 응용 프로그램 세부 정보&#40;SQL Server 유틸리티&#41;](../Topic/Deployed%20Data-tier%20Application%20Details%20\(SQL%20Server%20Utility\).md)를 참조하세요.  
  
## SQL Server의 관리되는 인스턴스의 모니터링 정책  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스의 초과 사용 및 미달 사용 정책은 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 프로세스 사용률  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 파일 공간  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 파일 공간  
  
-   컴퓨터 프로세서 사용률  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스의 전역 모니터링 정책을 보거나 변경하는 방법은 [유틸리티 관리&#40;SQL Server 유틸리티&#41;](../Topic/Utility%20Administration%20\(SQL%20Server%20Utility\).md)를 참조하세요.  
  
 개별 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스의 모니터링 정책을 보거나 변경하는 방법은 [관리되는 인스턴스 세부 정보&#40;SQL Server 유틸리티&#41;](../Topic/Managed%20Instance%20Details%20\(SQL%20Server%20Utility\).md)를 참조하세요.  
  
## 참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
  