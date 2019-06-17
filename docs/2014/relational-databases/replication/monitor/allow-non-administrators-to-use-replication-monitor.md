---
title: 비관리자의 복제 모니터 사용 허용 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e8f03d12d3ac1695d4f6d000c8eab89a42004fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667391"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>비관리자의 복제 모니터 사용 허용
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 비관리자가 복제 모니터를 사용할 수 있도록 허용하는 방법에 대해 설명합니다. 복제 모니터는 다음 역할의 멤버인 사용자가 사용할 수 있습니다.  
  
-   **sysadmin** 고정 서버 역할  
  
     이러한 사용자는 복제를 모니터링할 수 있으며 에이전트 일정, 에이전트 프로필 등의 복제 속성 변경을 완벽하게 제어할 수 있습니다.  
  
-   `replmonitor` 배포 데이터베이스의 데이터베이스 역할.  
  
     이러한 사용자는 복제를 모니터링할 수만 있고 복제 속성을 변경할 수는 없습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **비관리자의 복제 모니터 사용을 허용하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 비관리자의 복제 모니터의 멤버를 사용할 수 있도록 합니다 **sysadmin** 고정된 서버 역할에서 배포 데이터베이스에 사용자를 추가 하 고 해당 사용자를 할당 해야 합니다 `replmonitor` 역할입니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>비관리자의 복제 모니터 사용을 허용하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **데이터베이스**, **시스템 데이터베이스**를 차례로 확장한 다음 배포 데이터베이스(기본적으로 이름이 **distribution** 으로 지정됨)를 확장합니다.  
  
3.  **보안**을 확장하고 **사용자**를 마우스 오른쪽 단추로 클릭한 다음 **새 사용자**를 클릭합니다.  
  
4.  해당 사용자의 사용자 이름과 로그인을 입력합니다.  
  
5.  기본 스키마를 선택 `replmonitor`합니다.  
  
6.  선택 합니다 `replmonitor` 확인란을 **데이터베이스 역할 멤버 자격** 표입니다.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>replmonitor 고정 데이터베이스 역할에 사용자를 추가하려면  
  
1.  배포 데이터베이스의 배포자에서 [sp_helpuser&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpuser-transact-sql)를 실행합니다. 사용자에 나열 되지 않은 경우 `UserName` 결과 집합에 사용자 권한을 부여 해야 사용 하 여 배포 데이터베이스를 [CREATE USER &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-user-transact-sql) 문입니다.  
  
2.  배포 데이터베이스의 배포자에서 실행 [sp_helprolemember &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)의 값을 지정 `replmonitor` 에 대 한 합니다 **@rolename** 매개 변수입니다. 사용자에 표시 된 경우 `MemberName` 결과 집합에서 사용자는 이미이 역할에 속해 있습니다.  
  
3.  사용자에 속하지 않는 경우는 `replmonitor` 역할을 실행 [sp_addrolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) 배포 데이터베이스의 배포자에서. 값을 지정 `replmonitor` 에 대 한 **@rolename** 및 데이터베이스 사용자의 이름 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에 대 한 추가 되는 Windows 로그인 **@membername** 합니다.  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>replmonitor 고정 데이터베이스 역할에서 사용자를 제거하려면  
  
1.  사용자에 속해 있는지 확인 하는 `replmonitor` 역할을 실행 [sp_helprolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql) 배포 데이터베이스의 배포자에서의 값을 지정 하 고 `replmonitor` 에대한 **@rolename** . 사용자가 결과 집합의 `MemberName`에 나열되어 있지 않으면 해당 사용자는 현재 이 역할에 속해 있지 않은 것입니다.  
  
2.  사용자에 속하지는 `replmonitor` 역할을 실행할 [sp_droprolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql) 배포 데이터베이스의 배포자에서. 값을 지정 `replmonitor` 에 대 한 **@rolename** 제거할 Windows 로그인 또는 데이터베이스 사용자의 이름과 **@membername** 합니다.  
  
  
