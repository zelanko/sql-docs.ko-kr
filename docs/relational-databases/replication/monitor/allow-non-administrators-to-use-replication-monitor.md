---
title: 비관리자의 복제 모니터 사용 허용
description: 비관리자에게 SSMS(SQL Server Management Studio)의 복제 모니터 액세스 권한을 부여하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: f0451d8fcd55cc3d33616452109a5e5ff95081e0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287748"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>비관리자의 복제 모니터 사용 허용
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 비관리자가 복제 모니터를 사용할 수 있도록 허용하는 방법에 대해 설명합니다. 복제 모니터는 다음 역할의 멤버인 사용자가 사용할 수 있습니다.  
  
-   **sysadmin** 고정 서버 역할  
  
     이러한 사용자는 복제를 모니터링할 수 있으며 에이전트 일정, 에이전트 프로필 등의 복제 속성 변경을 완벽하게 제어할 수 있습니다.  
  
-   배포 데이터베이스의 **replmonitor** 데이터베이스 역할  
  
     이러한 사용자는 복제를 모니터링할 수만 있고 복제 속성을 변경할 수는 없습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **비관리자의 복제 모니터 사용을 허용하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 비관리자의 복제 모니터 사용을 허용하려면 **sysadmin** 고정 서버 역할의 멤버가 사용자를 배포 데이터베이스에 추가하고 해당 사용자를 **replmonitor** 역할에 할당해야 합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>비관리자의 복제 모니터 사용을 허용하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **데이터베이스**, **시스템 데이터베이스**를 차례로 확장한 다음 배포 데이터베이스(기본적으로 이름이 **distribution** 으로 지정됨)를 확장합니다.  
  
3.  **보안**을 확장하고 **사용자**를 마우스 오른쪽 단추로 클릭한 다음 **새 사용자**를 클릭합니다.  
  
4.  해당 사용자의 사용자 이름과 로그인을 입력합니다.  
  
5.  **replmonitor**의 기본 스키마를 선택합니다.  
  
6.  **데이터베이스 역할 멤버 자격** 표에서 **replmonitor** 확인란을 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>replmonitor 고정 데이터베이스 역할에 사용자를 추가하려면  
  
1.  배포 데이터베이스의 배포자에서 [sp_helpuser&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)를 실행합니다. 사용자가 결과 집합의 **UserName**에 나열되어 있지 않은 경우 [CREATE USER&#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md) 문을 사용하여 사용자에게 배포 데이터베이스에 대한 액세스 권한을 부여해야 합니다.  
  
2.  배포 데이터베이스의 배포자에서 [ 매개 변수에 ](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)replmonitor**값을 지정하고**sp_helprolemember&#40;Transact-SQL&#41;`@rolename`를 실행합니다. 사용자가 결과 집합의 **MemberName** 에 나열되어 있지 않으면 해당 사용자는 이미 이 역할에 속해 있는 것입니다.  
  
3.  사용자가 **replmonitor** 역할에 속해 있지 않으면 배포 데이터베이스의 배포자에서 [sp_addrolemember&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)를 실행합니다. **에** replmonitor`@rolename` 값, [!INCLUDE[msCoName](../../../includes/msconame-md.md)]에 추가할 데이터베이스 사용자 또는 `@membername` Windows 로그인의 이름을 지정합니다.  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>replmonitor 고정 데이터베이스 역할에서 사용자를 제거하려면  
  
1.  사용자가 **replmonitor** 역할에 속해 있는지 확인하려면 배포 데이터베이스의 배포자에서 [에 ](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)replmonitor**값을 지정하고**sp_helprolemember&#40;Transact-SQL&#41;`@rolename`를 실행합니다. 사용자가 결과 집합의 **MemberName** 에 나열되어 있지 않으면 해당 사용자는 현재 이 역할에 속해 있지 않은 것입니다.  
  
2.  사용자가 **replmonitor** 역할에 속해 있으면 배포 데이터베이스의 배포자에서 [sp_droprolemember&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)를 실행합니다. **에** replmonitor`@rolename` 값, `@membername`에 제거할 데이터베이스 사용자 또는 Windows 로그인의 이름을 지정합니다. 
  
  
