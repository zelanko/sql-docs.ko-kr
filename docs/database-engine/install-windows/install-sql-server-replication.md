---
title: "SQL Server 복제 설치 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "구성 요소 [SQL Server 복제]"
  - "명령줄 설치 [SQL Server 복제]"
  - "복제 설치"
  - "복제 [SQL Server], 설치"
  - "명령 프롬프트 [SQL Server 복제]"
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
caps.latest.revision: 41
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 41
---
# SQL Server 복제 설치
  복제 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사 또는 명령 프롬프트를 사용하여 설치할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 설치할 때나 기존 인스턴스를 수정할 때 복제를 설치할 수 있습니다.  
  
 복제 구성 요소를 설치한 후에는 복제를 사용하기 전에 먼저 서버를 구성해야 합니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 [배포 구성](../../relational-databases/replication/configure-distribution.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 수정할 때 복제 구성 요소를 설치하는 경우 설치가 완료된 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 중지하고 다시 시작해야 합니다. 이 동작을 수행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 복제 에이전트 하위 시스템을 인식하며 작업 단계에서 복제 에이전트를 호출할 수 있습니다.  
  
## 설치 프로그램을 사용하여 복제 설치  
 **다음의 새 인스턴스를 설치할 때 복제를 설치하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   RMO(복제 관리 개체)를 비롯한 복제 구성 요소를 설치하려면 설치 마법사의 **기능 선택** 페이지에서 **SQL Server 복제**를 선택합니다.  
  
## 명령 프롬프트에서 복제 설치  
 **다음의 새 인스턴스를 설치할 때 복제를 설치하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   [명령 프롬프트에서 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.  
  
## 참고 항목  
 [SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016.md)   
 [명령 프롬프트에서 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [SQL Server 2016 버전에서 지원하는 기능](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
  