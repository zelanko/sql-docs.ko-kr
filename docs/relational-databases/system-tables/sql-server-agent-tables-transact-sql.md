---
title: SQL Server 에이전트 테이블 (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Agent, system tables
- system tables [SQL Server], SQL Server Agent
ms.assetid: 6cb39bfd-079e-4be4-9c42-2fa234c65ce1
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f45847235f549eb80404236633111f5678f53825
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33263531"
---
# <a name="sql-server-agent-tables-transact-sql"></a>SQL Server 에이전트 테이블(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 섹션의 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 사용하는 정보를 저장하는 시스템 테이블에 대해 설명합니다. 모든 테이블은 msdb 데이터베이스의 dbo 스키마.  
  
## <a name="in-this-section"></a>섹션 내용  
 [dbo.sysalerts](../../relational-databases/system-tables/dbo-sysalerts-transact-sql.md)  
 각 경고에 대해 한 행을 포함합니다.  
  
 [dbo.syscategories](../../relational-databases/system-tables/dbo-syscategories-transact-sql.md)  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 작업, 경고 및 연산자를 구성하는 데 사용되는 범주를 포함합니다.  
  
 [dbo.sysdownloadlist](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)  
 모든 대상 서버의 다운로드 명령 대기열을 포함합니다.  
  
 [dbo.sysjobactivity](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 활동 및 상태에 대한 정보를 포함합니다.  
  
 [dbo.sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 예약된 작업 실행에 대한 정보를 포함합니다.  
  
 [dbo.sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 실행될 각 예약 작업의 정보를 저장합니다.  
  
 [dbo.sysjobschedules](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행할 작업에 대한 일정 정보를 포함합니다.  
  
 [dbo.sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)  
 특정 작업과 하나 이상의 대상 서버와의 연관 또는 관계를 저장합니다.  
  
 [dbo.sysjobsteps](../../relational-databases/system-tables/dbo-sysjobsteps-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 실행될 작업의 각 단계에 대한 정보를 포함합니다.  
  
 [dbo.sysjobstepslogs](../../relational-databases/system-tables/dbo-sysjobstepslogs-transact-sql.md)  
 작업 단계 로그에 대한 정보를 포함합니다.  
  
 [dbo.sysnotifications](../../relational-databases/system-tables/dbo-sysnotifications-transact-sql.md)  
 각 알림에 대해 한 행을 포함합니다.  
  
 [dbo.sysoperators](../../relational-databases/system-tables/dbo-sysoperators-transact-sql.md)  
 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 운영자에 대해 한 행을 포함합니다.  
  
 [dbo.sysproxies](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정에 대한 정보를 포함합니다.  
  
 [dbo.sysproxylogin](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)  
 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정과 연관된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 기록합니다.  
  
 [dbo.sysproxysubsystem](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)  
 각 프록시 계정에서 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 하위 시스템을 기록합니다.  
  
 [dbo.sysschedules](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 일정에 대한 정보를 포함합니다.  
  
 [dbo.syssessions](../../relational-databases/system-tables/dbo-syssessions-transact-sql.md)  
 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 세션에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 시작 날짜를 포함합니다. 세션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 시작될 때마다 생성됩니다.  
  
 [dbo.syssubsystems](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)  
 모든 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 하위 시스템에 대한 정보를 포함합니다.  
  
 [dbo.systargetservergroupmembers](../../relational-databases/system-tables/dbo-systargetservergroupmembers-transact-sql.md)  
 해당 다중 서버 그룹에 현재 참여하는 대상 서버를 기록합니다.  
  
 [dbo.systargetservergroups](../../relational-databases/system-tables/dbo-systargetservergroups-transact-sql.md)  
 해당 다중 서버 환경에 현재 참여하는 대상 서버 그룹을 기록합니다.  
  
 [dbo.systargetservers](../../relational-databases/system-tables/dbo-systargetservers-transact-sql.md)  
 해당 다중 서버 작업 도메인에 현재 참여하는 대상 서버를 기록합니다.  
  
 [dbo.systaskids](../../relational-databases/system-tables/dbo-systaskids-transact-sql.md)  
 현재 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업에 대해 이전 버전의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 생성된 태스크 매핑을 포함합니다.  
  
  
