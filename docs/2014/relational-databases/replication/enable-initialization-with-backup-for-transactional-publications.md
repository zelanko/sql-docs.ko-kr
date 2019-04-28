---
title: 트랜잭션 게시 (SQL Server Management Studio)에 대 한 백업으로 초기화 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 046eb926391faff26bb3238dfd225619e9fec374
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721336"
---
# <a name="enable-initialization-with-a-backup-for-transactional-publications-sql-server-management-studio"></a>트랜잭션 게시에 대한 백업으로 초기화 설정(SQL Server Management Studio)
  백업에서 트랜잭션 게시에 대한 구독을 초기화하려면 백업에서 초기화할 수 있도록 게시를 설정한 다음 구독을 만들 때 백업 정보를 지정합니다.  
  
-   **게시 속성 - \<Publication>** 대화 상자의 **구독 옵션** 페이지에서 이 게시를 사용합니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
-   [sp_addsubscription&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) 저장 프로시저를 사용하여 백업 정보를 지정합니다. **sp_addsubscription**에 필요한 매개 변수에 대한 자세한 내용은 [트랜잭션 구독을 백업에서 초기화&#40;복제 Transact-SQL 프로그래밍&#41;](initialize-a-transactional-subscription-from-a-backup.md)를 참조하세요.  
  
### <a name="to-enable-initialization-with-a-backup"></a>백업으로 초기화를 설정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **구독 옵션** 페이지에서 **백업 파일에서 초기화 허용** 옵션에 대해 **True** 값을 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [스냅숏 없이 트랜잭션 구독 초기화](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
