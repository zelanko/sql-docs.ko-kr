---
title: "비관리자의 복제 모니터 사용 허용 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "복제 모니터, 비관리자 액세스"
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 비관리자의 복제 모니터 사용 허용
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 비관리자가 복제 모니터를 사용할 수 있도록 허용하는 방법에 대해 설명합니다. 복제 모니터는 다음 역할의 멤버인 사용자가 사용할 수 있습니다.  
  
-   **sysadmin** 고정 서버 역할  
  
     이러한 사용자는 복제를 모니터링할 수 있으며 에이전트 일정, 에이전트 프로필 등의 복제 속성 변경을 완벽하게 제어할 수 있습니다.  
  
-   배포 데이터베이스의 **replmonitor** 데이터베이스 역할  
  
     이러한 사용자는 복제를 모니터링할 수만 있고 복제 속성을 변경할 수는 없습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **비관리자의 복제 모니터 사용을 허용하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 비관리자의 복제 모니터의 멤버를 사용 하도록 허용 하는 **sysadmin** 고정된 서버 역할에서 배포 데이터베이스에 사용자를 추가 하 고 해당 사용자를 할당 해야는 **replmonitor** 역할입니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### 비관리자의 복제 모니터 사용을 허용하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  확장 **데이터베이스**, 확장 **시스템 데이터베이스**, 를 확장 한 다음 배포 데이터베이스 (라는 **배포** 기본적으로).  
  
3.  확장 **보안**, 를 마우스 오른쪽 단추로 클릭 **사용자**, 를 클릭 하 고 **새 사용자**합니다.  
  
4.  해당 사용자의 사용자 이름과 로그인을 입력합니다.  
  
5.  **replmonitor**의 기본 스키마를 선택합니다.  
  
6.  **데이터베이스 역할 멤버 자격** 표에서 **replmonitor** 확인란을 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### replmonitor 고정 데이터베이스 역할에 사용자를 추가하려면  
  
1.  배포 데이터베이스의 배포자에서 실행 [sp_helpuser (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)합니다. 사용자에 나열 되지 않은 경우 **UserName** 결과 집합에 사용자 권한을 부여 해야 사용 하 여 배포 데이터베이스는 [사용자 만들기 및 #40; TRANSACT-SQL & #41;](../../../t-sql/statements/create-user-transact-sql.md) 문입니다.  
  
2.  배포 데이터베이스의 배포자에서 실행 [sp_helprolemember (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md), 값을 지정 하면 **replmonitor** 에 대 한는 **@rolename** 매개 변수입니다. 사용자가 결과 집합의 **MemberName** 에 나열되어 있지 않으면 해당 사용자는 이미 이 역할에 속해 있는 것입니다.  
  
3.  사용자에 속하지 않는 경우는 **replmonitor** 역할, 실행 [sp_addrolemember (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 배포 데이터베이스의 배포자입니다. **@rolename** 에는 **replmonitor** 값을 지정하고 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] @membername **에는 추가할 데이터베이스 사용자 또는**Windows 로그인의 이름을 지정합니다.  
  
#### replmonitor 고정 데이터베이스 역할에서 사용자를 제거하려면  
  
1.  사용자에 속해 있는지 확인 하는 **replmonitor** 역할, 실행 [sp_helprolemember (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) 배포 데이터베이스의 배포자에서 값을 지정 하 고 **replmonitor** 에 대 한 **@rolename**합니다. 사용자가 결과 집합의 **MemberName** 에 나열되어 있지 않으면 해당 사용자는 현재 이 역할에 속해 있지 않은 것입니다.  
  
2.  사용자에 속하지 않는 경우는 **replmonitor** 역할, 실행 [sp_droprolemember (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) 배포 데이터베이스의 배포자입니다. **@rolename** 에 **replmonitor** 값을 지정하고 **@membername**에는 제거할 데이터베이스 사용자 또는 Windows 로그인의 이름을 지정합니다.  
  
  