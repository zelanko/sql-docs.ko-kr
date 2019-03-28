---
title: recovery interval 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- restoring recovery interval [SQL Server]
- checkpoints [SQL Server]
- recovery interval option [SQL Server]
- default recovery interval option
- time [SQL Server], recovery interval
- interval for recovery [SQL Server]
- maximum number of minutes per database recovery
- recovery [SQL Server], recovery interval option
ms.assetid: e4734b3b-8fbe-4b65-9c48-91b5a3dd18e1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 89449cbc31e1ec36fa37a5bb36b1f505cdd2e14d
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530915"
---
# <a name="configure-the-recovery-interval-server-configuration-option"></a>recovery interval 서버 구성 옵션 구성
  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 복구 간격 [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **복구 간격** 옵션은 데이터베이스를 복구하는 데 필요한 시간의 상한값을 정의합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서는 이 옵션에 지정된 값을 사용하여 지정된 데이터베이스에 대해 [자동 검사점](../../relational-databases/logs/database-checkpoints-sql-server.md) 을 실행하는 대략적인 빈도를 결정합니다.  
  
 기본 복구 간격 값은 0이며 이는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 복구 간격을 자동으로 구성함을 의미합니다. 일반적으로 기본 복구 간격을 사용하면 활성 데이터베이스의 경우 자동 검사점의 실행 간격은 약 1분이고 복구 시간은 1분 미만입니다. 값이 높을수록 최대 복구 시간(분)의 근사치가 더 커집니다. 예를 들어 복구 간격으로 3을 설정하면 최대 복구 시간이 약 3분이 됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 복구 간격 서버 구성 옵션을 구성합니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [Recovery interval 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   복구 간격은 기본 대상 복구 시간(0)을 사용하는 데이터베이스에만 영향을 줍니다. 데이터베이스에 대한 서버 복구 간격을 재정의하려면 데이터베이스에 기본이 아닌 대상 복구 시간을 구성합니다. 자세한 내용은 [데이터베이스의 대상 복구 시간 변경&#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)서버 구성 옵션을 구성하는 방법에 대해 설명합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자만 변경해야 합니다.  
  
-   일반적으로 성능 문제가 없는 한 복구 간격을 0으로 유지하는 것이 좋습니다. 복구 간격 설정을 늘리려는 경우에는 값을 조금씩 늘려가며 그에 따라 복구 성능에 미치는 영향을 확인하는 것이 좋습니다.  
  
-   **sp_configure** 를 사용하여 **복구 간격** 옵션 값을 60분 이상으로 변경하는 경우 RECONFIGURE WITH OVERRIDE를 지정하세요. WITH OVERRIDE를 지정하면 유효하지 않은 값 또는 권장되지 않는 값이 있는지 확인하는 구성 값 검사가 수행되지 않습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **복구 간격을 설정하려면**  
  
1.  개체 탐색기에서 서버 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **데이터베이스 설정** 노드를 클릭합니다.  
  
3.  **복구**의 **복구 간격(분)** 입력란에 0부터 32767까지 범위의 값을 입력하거나 선택하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작 시 각 데이터베이스를 복구하는 데 걸리는 최대 시간을 분으로 설정합니다. 기본값 0을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 자동으로 구성합니다. 기본값을 설정하면 실제 운영 시 1분 이하의 복구 시간이 사용되고 활성 데이터베이스의 경우 약 1분 간격으로 검사점이 실행됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-set-the-recovery-interval"></a>복구 간격을 설정하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 를 사용하여 `recovery interval` 옵션 값을 `3` 분으로 설정하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'recovery interval', 3 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 복구 간격 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스의 대상 복구 시간 변경&#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)   
 [데이터베이스 검사점&#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [show advanced options 서버 구성 옵션](show-advanced-options-server-configuration-option.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
