---
title: user connections 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- simultaneous connections [SQL Server]
- user connections option [SQL Server]
- users [SQL Server], simultaneous connections
- maximum number of simultaneous user connections
- connections [SQL Server], simultaneous
ms.assetid: 53beee6e-59fe-4276-9abb-8f1cec2a3508
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8e06f9c776811fab5dc2a8f8f9748dde1402e0f7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-the-user-connections-server-configuration-option"></a>user connections 서버 구성 옵션 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 사용자 연결 [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 설정하는 방법에 대해 설명합니다. **사용자 연결** 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 허용되는 최대 동시 사용자 연결 수를 지정합니다. 허용되는 실제 사용자 연결 수는 사용 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전과 응용 프로그램 및 하드웨어 제한에 따라서도 달라집니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 사용자 연결을 최대 32,767개까지 허용합니다. **사용자 연결 수** 는 동적(자체 구성) 옵션이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 허용 가능한 최대값까지 필요한 만큼 자동으로 최대 사용자 연결 수를 조정합니다. 예를 들어, 10명의 사용자만 로그인했으면 10개의 사용자 연결 개체가 할당됩니다. 대부분의 경우 이 옵션의 값을 변경하지 않아도 됩니다. 기본값은 0이며 최대(32,767) 사용자 연결을 허용합니다.  
  
 시스템에 허용되는 최대 사용자 연결 수를 확인하려면 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 실행하거나 [sys.configuration](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 카탈로그 뷰를 쿼리합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **사용자 연결 옵션을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [사용자 연결 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전문가만이 변경해야 합니다.  
  
-   **사용자 연결** 옵션을 사용하면 동시 연결이 너무 많아 서버가 과부하되는 것을 방지할 수 있습니다. 시스템과 사용자 요구 사항에 따라 연결 수를 계산할 수 있습니다. 예를 들어, 사용자가 많은 시스템에서는 각 사용자가 고유하게 연결할 필요는 없습니다. 여러 사용자 간에 연결을 공유할 수 있습니다. OLE DB 응용 프로그램을 실행 중인 사용자는 각 열린 연결 개체당 하나의 연결이 필요하며 ODBC 응용 프로그램을 실행 중인 사용자는 응용 프로그램에 있는 각 활성 연결 핸들당 하나의 연결이 필요합니다. 또한 DB-Library 응용 프로그램을 실행 중인 사용자는 DB-Library **dbopen** 함수를 호출하는 시작된 각 프로세스당 하나의 연결이 필요합니다.  
  
    > [!IMPORTANT]  
    >  이 옵션을 사용해야 하는 경우 연결의 사용 여부에 관계없이 각 연결에 오버헤드가 필요하므로 값을 너무 높게 설정하지 마십시오. 최대 사용자 연결 수를 초과하면 오류 메시지가 나타나고 다른 연결을 사용할 수 있게 될 때까지 연결할 수 없습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-user-connections-option"></a>사용자 연결 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
2.  **연결** 노드를 클릭합니다.  
  
3.  **연결**의 **최대 동시 연결 수** 상자에 0부터 32767까지의 값을 입력하거나 선택하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 동시에 연결할 수 있는 최대 사용자 수를 설정합니다.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-user-connections-option"></a>사용자 연결 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예제에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 사용하여 `user connections` 옵션 값을 `325` 명의 사용자로 구성하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'user connections', 325 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 설정하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 사용자 연결 옵션을 구성한 후  
 설정을 적용하려면 서버를 다시 시작해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
