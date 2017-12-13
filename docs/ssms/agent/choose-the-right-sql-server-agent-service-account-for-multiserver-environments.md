---
title: "다중 서버 환경에 적합한 SQL Server 에이전트 서비스 계정 선택 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, service accounts
- multiserver environments [SQL Server], SQL Server Agent service account behavior
ms.assetid: a07e2f38-281c-495b-965b-13fad03ba548
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 705eadb404832ca2173d453a96e1deac40a431f3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="choose-the-right-sql-server-agent-service-account-for-multiserver-environments"></a>다중 서버 환경에 적합한 SQL Server 에이전트 서비스 계정 선택
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스에 대해 선택한 Windows 계정은 다음과 같이 다중 서버 환경의 동작에 영향을 줄 수 있습니다.  
  
-   로컬 Windows Administrators 그룹의 멤버가 아닌 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 실행하는 경우 대상 서버를 마스터 서버에 참여시키면 실패할 수 있습니다. 실패 시 다음 오류 메시지가 반환됩니다.  
  
    "참여 작업이 실패했습니다."  
  
    이 문제를 해결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 다시 시작하십시오.  
  
-   로컬 시스템 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 실행하는 경우 마스터 서버와 대상 서버가 같은 컴퓨터에 있는 경우에만 마스터 서버-대상 서버 작업이 지원됩니다. 이 구성을 사용하면 대상 서버를 마스터 서버에 참여시킬 때 다음 메시지가 반환됩니다.  
  
    "*<target_server_computer_name>*의 에이전트 시작 계정에 대상 서버로 로그인할 권한이 있는지 확인하세요."  
  
    이 정보 메시지는 무시해도 됩니다. 참여 작업이 성공적으로 완료됩니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스에 대한 계정을 선택하는 방법에 대한 자세한 내용은 [SQL Server 에이전트 서비스의 계정 선택](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)을 참조하세요.  
  
