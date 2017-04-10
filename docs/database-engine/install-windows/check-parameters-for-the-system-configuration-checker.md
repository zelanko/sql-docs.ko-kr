---
title: "시스템 구성 검사기의 검사 매개 변수 | Microsoft Docs"
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
  - "SQL Server 설치, 시스템 구성 검사"
  - "시스템 구성 검사 실패 [SQL Server]"
  - "설치 전 구성 확인"
  - "SCC [SQL Server]"
  - "시스템 구성 검사"
  - "설치 전 컴퓨터 검색 [SQL Server]"
  - "설치 전 구성 검사"
  - "상태 정보 [SQL Server], 시스템 구성 검사기"
  - "매개 변수 [SQL Server], 시스템 구성 검사기"
  - "구성 검사 [SQL Server]"
  - "설치 [SQL Server], 시스템 구성 검사기"
ms.assetid: 8e712c15-6bfa-4d71-b303-9526101e5594
caps.latest.revision: 46
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 46
---
# 시스템 구성 검사기의 검사 매개 변수
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 SCC(시스템 구성 검사기)는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 컴퓨터를 검색합니다. SCC는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 성공적인 설치를 방해하는 조건이 있는지 확인합니다. 설치 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 시작하기 전에 SCC는 각 항목의 상태를 검색합니다. 그런 다음 검색 결과를 필수 조건과 비교하고 차단 문제 해결을 위한 지침을 제공합니다.  
  
 시스템 구성 검사기에서는 각 실행 규칙에 대한 간단한 설명과 실행 상태를 포함하는 보고서를 생성합니다. 시스템 구성 검사 보고서는 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.  
  
## 참고 항목  
 [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [지원되는 버전 및 에디션 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
  