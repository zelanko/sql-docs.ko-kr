---
title: 유사 시 대기 운영자 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- fail-safe operator [SQL Server]
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 0f4eb513-5c0a-4523-974e-e85c1deeb57f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 73eb11034d185deb9c004d138230fff8fbf27bb6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995294"
---
# <a name="designate-a-fail-safe-operator"></a>유사 시 대기 운영자 지정
  유사 시 대기 운영자는 지정된 운영자에게 알릴 수 없을 경우 경고를 받는 사용자입니다. 이 항목 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는를 사용 하 여에서 에이전트 경고 알림을 받을 유사 시 대기 운영자를 설정 하는 방법에 대해 설명 합니다 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **유사 시 대기 운영자를 지정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   의 이후 버전에서는 에이전트에서 호출기 및 **net send** 옵션이 제거 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.  
  
-   SQL Server 에이전트는 데이터베이스 메일을 사용하여 운영자에게 전자 메일 및 호출기 알림을 보내도록 구성해야 합니다. 자세한 내용은 [경고를 운영자에게 할당](assign-alerts-to-an-operator.md)을 참조하세요.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 작업 구조를 만들고 관리할 수 있는 바람직한 방법을 제공하는데 이는 그래픽을 사용하여 쉽게 작업을 관리할 수 있는 방법입니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 **sysadmin** 고정 서버 역할의 멤버만 유사 시 대기 운영자를 지정할 수 있습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-designate-a-fail-safe-operator"></a>유사 시 대기 운영자를 지정하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 유사 시 대기로 지정할 SQL Server 에이전트 운영자가 포함된 서버를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.  

3.  **SQL Server 에이전트 속성-**_server_name_ 대화 상자의 **페이지 선택**아래에서 **경고 시스템**을 선택 합니다.  
 
4.  **유사 시 대기 운영자**에서 **유사 시 대기 운영자 설정**을 선택합니다.  
  
5.  **운영자** 목록에서 유사 시 대기 운영자로 설정할 운영자를 선택합니다.  
  
6.  **전자 메일**, **호출기**또는 **Net send**확인란 중 하나 이상을 선택하여 운영자에게 알림을 보낼 방법을 지정합니다.  
  
7.  작업을 완료한 후 **확인**을 클릭합니다.  
  
  
