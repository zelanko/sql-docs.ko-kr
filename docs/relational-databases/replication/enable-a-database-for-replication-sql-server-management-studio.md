---
title: 데이터베이스 복제 설정(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ac332e77226d5de33a4ef7fc77a0c34f6b234a3b
ms.sourcegitcommit: b2a29f9659f627116d0a92c03529aafc60e1b85a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59516489"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>데이터베이스 복제 설정(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
**sysadmin** 고정 서버 역할의 멤버가 새 게시 마법사로 게시를 만들면 데이터베이스가 복제를 사용할 수 있도록 암시적으로 설정됩니다. **db_owner** 고정 데이터베이스 역할의 멤버가 해당 데이터베이스에 하나 이상의 게시를 만들 수 있도록 **sysadmin** 고정 서버 역할의 멤버는 데이터베이스가 복제를 사용할 수 있도록 명시적으로 설정할 수도 있습니다. 데이터베이스를 명시적으로 사용하려면 **게시자 속성 - \<Publisher>** 대화 상자의 **게시 데이터베이스** 페이지를 사용합니다. 이 대화 상자에 액세스하는 방법은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)을 참조하십시오.  
  
## <a name="using-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 사용
  
1.  **게시자 속성 - \<Publisher>** 대화 상자의 **게시 데이터베이스** 페이지에서 복제할 각 데이터베이스에 대해 **트랜잭션** 및/또는 **병합** 확인란을 선택합니다. 데이터베이스에서 스냅샷 복제를 설정하려면 **트랜잭션** 을 선택합니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
## <a name="using-transact-sql-t-sql"></a>Transact-SQL(T-SQL) 사용
다음 Transact-SQL 코드를 사용하여 복제에 데이터베이스를 사용하도록 설정할 수 있습니다. 

```sql
USE master
EXEC sp_replicationdboption @dbname = 'AdventureWorks2017',
@optname = 'publish',
@value = 'true'
GO
```

게시를 사용하지 않으려면 @value = 'false'를 설정합니다. 
