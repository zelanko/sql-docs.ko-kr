---
title: locks 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- locks option [SQL Server]
ms.assetid: b0cf0f86-7652-4574-a9fb-908e10d03973
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2fa3483acfe078dbdd3537c0b327032765def62d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68012604"
---
# <a name="configure-the-locks-server-configuration-option"></a>locks 서버 구성 옵션 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] locks [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **locks** 옵션은 사용 가능한 최대 잠금 수를 설정하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 잠금에 사용하는 메모리 용량을 제한합니다. 기본 설정은 0이며 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 시스템 요구 사항의 변화를 기준으로 동적으로 잠금 구조를 할당하거나 할당 취소할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **잠금 옵션을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [잠금 옵션을 구성한 후](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전문가만이 변경해야 합니다.  
  
-   **locks** 를 0으로 설정한 상태로 서버를 시작하면 잠금 관리자가 초기 2,500개의 잠금 구조 풀에 사용할 충분한 메모리를 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 으로부터 확보합니다. 잠금 풀을 모두 사용하면 풀에 사용할 추가 메모리를 확보합니다.  
  
     일반적으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 메모리 풀에서 사용 가능한 잠금 풀에 메모리가 더 많이 필요하고 컴퓨터 메모리를 더 사용할 수 있는 경우 **최대 서버 메모리** 임계값에 도달하지 않았으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 잠금 요청을 만족시킬 수 있도록 동적으로 메모리가 할당됩니다. 그러나 이 메모리 할당으로 인해 운영 체제 수준에서 페이징이 발생하는 경우, 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 같은 컴퓨터에서 실행되는 다른 애플리케이션이 이 메모리를 사용하면 잠금 공간이 추가로 할당되지 않습니다. 동적 잠금 풀은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 할당된 메모리의 60% 이상은 확보하지 못합니다. 잠금 풀이 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 의해 확보된 메모리의 60%에 도달하거나 컴퓨터에 더 이상 사용 가능한 메모리가 없는 경우 잠금에 대한 요청을 추가하면 오류가 발생됩니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 잠금을 동적으로 사용하는 것이 권장 구성입니다. 그러나 **locks** 를 설정하여 잠금 리소스를 동적으로 할당하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기능을 무시할 수 있습니다. **locks** 가 0 이외의 값으로 설정되면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 **locks**에 지정된 값보다 많은 잠금을 할당할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용할 수 있는 잠금 수가 초과되었다는 메시지가 표시되면 이 값을 늘립니다. 각 잠금은 잠금 하나당 96바이트의 메모리를 사용하므로 이 값을 늘리면 서버에서 전용으로 사용하는 메모리 양을 늘려야 합니다.  
  
-   또한 **locks** 옵션은 잠금 에스컬레이션이 수행될 때 영향을 줍니다. **locks** 가 0으로 설정된 경우 현재 잠금 구조에서 사용되는 메모리가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 메모리 풀의 40%에 도달하면 잠금 에스컬레이션이 발생합니다. **locks** 가 0으로 설정되지 않은 경우 잠금 수가 **locks**에 지정된 값의 40%에 도달하면 잠금 에스컬레이션이 수행됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-locks-option"></a>잠금 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **고급** 노드를 클릭합니다.  
  
3.  **병렬 처리**아래에 원하는 **잠금** 옵션 값을 입력합니다.  
  
     **잠금** 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 잠금에 사용하는 메모리 양을 제한하는 최대 사용 가능 잠금 수를 설정할 수 있습니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-locks-option"></a>잠금 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 통해 `locks` 옵션 값을 `20000`으로 설정하여 모든 사용자가 사용할 수 있는 잠금 수를 설정하는 방법을 보여 줍니다.  
  
```sql  
Use AdventureWorks2012 ;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'locks', 20000;  
GO  
RECONFIGURE;  
GO  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="follow-up-after-you-configure-the-locks-option"></a><a name="FollowUp"></a> 후속 작업: 잠금 옵션을 구성한 후  
 설정을 적용하려면 서버를 다시 시작해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
