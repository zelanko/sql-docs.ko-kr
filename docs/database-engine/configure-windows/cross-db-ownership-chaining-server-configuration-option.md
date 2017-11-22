---
title: "cross db ownership chaining 서버 구성 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cross-database ownership chaining
- cross db ownership chaining option
- chaining ownership
ms.assetid: 7b2d49f2-b91c-4aee-a52b-6cc49bed03af
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 74b65323147055178856404d844e0325b3c1bf7f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="cross-db-ownership-chaining-server-configuration-option"></a>cross db ownership chaining 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **cross db ownership chaining** 옵션을 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 데이터베이스 간 소유권 체인을 구성할 수 있습니다.  
  
 이 서버 옵션을 사용하면 데이터베이스 수준에서 데이터베이스 간 소유권 체인을 제어하거나 모든 데이터베이스의 데이터베이스 간 소유권 체인을 제어할 수 있습니다.  
  
-   인스턴스에 대해 **cross db ownership chaining** 이 해제(0) 상태일 때 모든 데이터베이스에 대해 데이터베이스 간 소유권 체인이 해제됩니다.  
  
-   인스턴스에 대해 **cross db ownership chaining** 이 설정(1)되어 있으면 데이터베이스 간 소유권 체인이 모든 데이터베이스에 대해 설정됩니다.  
  
-   ALTER DATABASE 문의 SET 절을 사용하여 개별 데이터베이스에 대해 데이터베이스 간 소유권 체인을 설정할 수 있습니다. 새 데이터베이스를 만드는 경우 CREATE DATABASE 문을 사용하여 새 데이터베이스에 대해 데이터베이스 간 소유권 체인을 설정할 수 있습니다.  
  
     **인스턴스에서 호스트한 모든 데이터베이스가 데이터베이스 간 소유권 체인에 참여하지 않고 사용자가 이 설정에 따른 보안 위험을 잘 알고 있는 경우가 아니라면** cross db ownership chaining [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 1로 설정하지 않는 것이 좋습니다.  

데이터베이스 간 소유권 체인의 현재 상태를 확인하려면 다음 쿼리를 실행합니다.  
```sql
SELECT is_db_chaining_on, name FROM sys.databases;
```  
결과 1은 데이터베이스 간 소유권 체인이 사용하도록 설정되어 있음을 나타냅니다.

## <a name="controlling-cross-database-ownership-chaining"></a>데이터베이스 간 소유권 체인 제어  
 데이터베이스 간 소유권 체인을 설정하기 전에 다음 사항을 고려하십시오.  
  
-   데이터베이스 간 소유권 체인을 설정하거나 해제하려면 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
-   프로덕션 서버에서 데이터베이스 간 소유권 체인 설정을 해제하기 전에 타사 응용 프로그램을 포함한 모든 응용 프로그램을 테스트하여 설정 변경으로 인해 응용 프로그램 기능이 영향받지 않도록 하십시오.  
  
-   **sp_configure** 를 사용하여 RECONFIGURE를 지정하는 경우에는 서버를 실행하는 동안 **cross db ownership chaining**옵션을 변경할 수 있습니다.  
  
-   데이터베이스 간 소유권 체인이 필요한 데이터베이스가 있는 경우 권장되는 방법은 **sp_configure** 를 사용하여 인스턴스에 대해 **cross db ownership chaining**옵션을 해제한 다음 ALTER DATABASE 문을 사용하여 데이터베이스 간 소유권 체인이 필요한 개별 데이터베이스에 대해 데이터베이스 간 소유권 체인을 설정하는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
