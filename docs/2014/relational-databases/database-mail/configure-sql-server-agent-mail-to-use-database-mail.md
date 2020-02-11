---
title: 데이터베이스 메일을 사용하도록 SQL Server 에이전트 메일 구성 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], SQL Server Agent Mail
- SQL Server Agent Mail
ms.assetid: 4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d3c2f5f0be09e9a60997308efd72c360348efc60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62872330"
---
# <a name="configure-sql-server-agent-mail-to-use-database-mail"></a>데이터베이스 메일을 사용하도록 SQL Server 에이전트 메일 구성
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 데이터베이스 메일로 알림 및 경고를 보내도록 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에이전트를 구성하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  
  
-   [필수 구성 요소](#Prerequisites)  
  
-   [보안](#Security)  
  
-   [SQL Server Management Studio를 통해 데이터베이스 메일을 사용하도록 SQL Server 에이전트를 구성하려면](#SSMSProcedure)  
  
-   [후속 작업](#Follow_Up)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 필수 조건  
  
-   데이터베이스 메일을 활성화합니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정이 사용할 데이터베이스 메일 계정을 만듭니다.  
  
-   에이전트 서비스 계정에서 사용할 데이터베이스 메일 프로필을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**msdb** 데이터베이스의 **DatabaseMailUserRole** 에 사용자를 추가합니다.  
  
-   프로필을 **msdb** 데이터베이스의 기본 프로필로 설정합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 프로필 계정을 만들고 저장 프로시저를 실행하는 사용자는 sysadmin 고정 서버 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **데이터베이스 메일을 사용하도록 SQL Server 에이전트를 구성하려면**  
  
-   개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 확장합니다.  
  
-   **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
-   **경고 시스템**을 클릭합니다.  
  
-   **메일 프로필 설정**을 선택합니다.  
  
-   **메일 시스템** 목록에서 **데이터베이스 메일**을 선택합니다.  
  
-   **메일 프로필**목록에서 데이터베이스 메일에 대한 메일 프로필을 선택합니다.  
  
-   SQL Server 에이전트를 다시 시작합니다.  
  
##  <a name="Follow_Up"></a> 후속 작업  
 경고 및 알림을 보내도록 에이전트를 구성하려면 다음 태스크를 수행해야 합니다.  
  
-   [경고](../../ssms/agent/alerts.md)  
  
     경고를 구성하여 특정 데이터베이스 이벤트 또는 운영 체제 상태를 운영자에게 알릴 수 있습니다.  
  
-   [연산자](../../ssms/agent/operators.md)  
  
     운영자는 전자 알림을 받을 수 있는 사람 또는 그룹의 별칭입니다.  
  
  
