---
title: 이벤트 전달 서버 (SQL Server Management Studio)를 지정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1617038a42dcef9103613e4d0164ba0f796000fa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995275"
---
# <a name="designate-an-events-forwarding-server-sql-server-management-studio"></a>Designate an Events Forwarding Server (SQL Server Management Studio)
  이 항목에서는를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여에서 이벤트를 전달 하는 서버를 지정 하는 방법에 대해 설명 합니다 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . 이벤트 전달은 서버 간에 전달되는 이벤트에만 적용되고 단일 컴퓨터에서 호스팅되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 전달되는 이벤트에는 적용되지 않습니다. 또한 전달된 이벤트를 수신하려면 경고 관리 서버가 SQL Server의 기본 인스턴스여야 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 이벤트 전달 서버를 지정합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-designate-an-events-forwarding-server"></a>이벤트 전달 서버를 지정하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 이벤트를 다른 서버로 전달하려는 서버를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.  

3.  **SQL Server 에이전트 속성 -**_server_name_ 대화 상자의 **페이지 선택** 아래에서 **고급**을 선택합니다.  

4.  **SQL Server 이벤트 전달**아래에서 **다른 서버로 이벤트 전달** 확인란을 선택합니다.  
  
5.  **서버** 목록에서 서버를 선택하고 **이벤트**에서 다음 중 하나를 수행합니다.  
  
    -   로컬 경고로 처리되지 않은 이벤트만 전달하려면 **처리되지 않은 이벤트** 를 선택합니다.  
  
    -   로컬 경고로 처리되었는지 여부에 관계 없이 모든 이벤트를 전달하려면 **모든 이벤트** 를 선택합니다.  
  
6.  **이벤트의 심각도가 다음 이상인 경우** 목록에서 선택한 서버로 이벤트가 전달되는 심각도 수준을 클릭합니다.  
  
7.  작업을 완료한 후 **확인**을 클릭합니다.  
  
  
