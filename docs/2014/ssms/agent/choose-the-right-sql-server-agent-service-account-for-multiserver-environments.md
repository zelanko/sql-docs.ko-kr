---
title: 다중 서버 환경에 대 한 올바른 SQL Server 에이전트 서비스 계정 선택 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, service accounts
- multiserver environments [SQL Server], SQL Server Agent service account behavior
ms.assetid: a07e2f38-281c-495b-965b-13fad03ba548
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3a981690efb0139d8878cab4e13794fdcf44ed7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52762956"
---
# <a name="choose-the-right-sql-server-agent-service-account-for-multiserver-environments"></a>다중 서버 환경에 적합한 SQL Server 에이전트 서비스 계정 선택
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에 대해 선택한 Windows 계정은 다음과 같이 다중 서버 환경의 동작에 영향을 줄 수 있습니다.  
  
-   로컬 Windows Administrators 그룹의 멤버가 아닌 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 실행하는 경우 대상 서버를 마스터 서버에 참여시키면 실패할 수 있습니다. 실패 시 다음 오류 메시지가 반환됩니다.  
  
     "참여 작업이 실패했습니다."  
  
     이 문제를 해결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 다시 시작하십시오.  
  
-   로컬 시스템 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 실행하는 경우 마스터 서버와 대상 서버가 같은 컴퓨터에 있는 경우에만 마스터 서버-대상 서버 작업이 지원됩니다. 이 구성을 사용하면 대상 서버를 마스터 서버에 참여시킬 때 다음 메시지가 반환됩니다.  
  
     "*<target_server_computer_name>* 의 에이전트 시작 계정에 대상 서버로 로그인할 권한이 있는지 확인하세요."  
  
     이 정보 메시지는 무시해도 됩니다. 참여 작업이 성공적으로 완료됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에 대한 계정을 선택하는 방법에 대한 자세한 내용은 [SQL Server 에이전트 서비스의 계정 선택](select-an-account-for-the-sql-server-agent-service.md)을 참조하세요.  
  
  
