---
title: "SQL Server 관리되는 인스턴스의 유틸리티 컬렉션 집합을 위한 프록시 계정 변경(SQL Server 유틸리티) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# SQL Server 관리되는 인스턴스의 유틸리티 컬렉션 집합을 위한 프록시 계정 변경(SQL Server 유틸리티)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]관리 인스턴스의 유틸리티 컬렉션 집합에 대한 프록시 계정을 변경하는 방법에 대해 설명합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### SQL Server의 관리 인스턴스에서 유틸리티 컬렉션 집합에 대한 프록시 계정을 변경하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스를 제거합니다.  
  
    -   SSMS의 **유틸리티 탐색기** 에서 **관리되는 인스턴스** 노드를 클릭합니다.  
  
    -   **유틸리티 탐색기** 목록 뷰에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 마우스 오른쪽 단추로 클릭하고 **관리되는 인스턴스 제거…**를 선택합니다. 자세한 내용은 [SQL Server 유틸리티에서 SQL Server 인스턴스 제거](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)를 참조하세요.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록합니다.  
  
    -   SSMS의 **유틸리티 탐색기**에서 **관리되는 인스턴스** 노드를 마우스 오른쪽 단추로 클릭하고 **관리되는 인스턴스 추가…**를 선택합니다.  
  
    -   표시되는 메시지에 따라 마법사를 완료하여 새 프록시 계정을 지정합니다.  
  
## 참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 유틸리티 문제 해결](../Topic/Troubleshoot%20the%20SQL%20Server%20Utility.md)  
  
  