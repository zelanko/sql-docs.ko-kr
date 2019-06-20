---
title: Oracle 게시자 (복제 TRANSACT-SQL 프로그래밍)에 대 한 트랜잭션 집합 작업 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_publisherproperty
- Oracle publishing [SQL Server replication], configuring
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfa83609f4040fc9875a63217b0e86d6a3ff99bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187021"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>Oracle 게시자에 대한 트랜잭션 세트 작업 구성(복제 Transact-SQL 프로그래밍)
  **Xactset** 작업은 로그 판독기 에이전트가 Oracle 게시자에 연결되어 있지 않을 때 해당 게시자에서 트랜잭션 세트를 만들기 위해 실행되는 복제를 통해 만들어지는 Oracle 데이터베이스 작업입니다. 배포자에서 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 이 작업을 사용하도록 설정하고 구성할 수 있습니다. 자세한 내용은 [Oracle 게시자를 위한 성능 튜닝](../non-sql/performance-tuning-for-oracle-publishers.md)을 참조하세요.  
  
### <a name="to-enable-the-transaction-set-job"></a>트랜잭션 세트 작업을 사용하도록 설정하려면  
  
1.  Oracle 게시자에서 **job_queue_processes** 초기화 매개 변수를 Xactset 작업을 실행하기에 충분한 값으로 설정합니다. 이 매개 변수에 대한 자세한 내용은 Oracle 게시자의 데이터베이스 설명서를 참조하십시오.  
  
2.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. Oracle 게시자의 이름을 지정 **@publisher** 에 값 `xactsetbatching` 에 대 한 **@propertyname** 를 값 `enabled` 에 대 한 **@propertyvalue** .  
  
3.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. Oracle 게시자의 이름을 지정 **@publisher** 에 값 `xactsetjobinterval` 에 대 한 **@propertyname** , 작업 간격 (분)에 대 한 **@propertyvalue** .  
  
4.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. Oracle 게시자의 이름을 지정 **@publisher** 에 값 `xactsetjob` 에 대 한 **@propertyname** 를 값 `enabled` 에 대 한 **@propertyvalue** .  
  
### <a name="to-configure-the-transaction-set-job"></a>트랜잭션 세트 작업을 구성하려면  
  
1.  (선택 사항) 배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. **@publisher** 에 Oracle 게시자의 이름을 지정합니다. 이렇게 하면 게시자에서 **Xactset** 작업의 속성이 반환됩니다.  
  
2.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. **@publisher** 에 Oracle 게시자의 이름을, **@propertyname** 에 설정되는 Xactset 작업 속성의 이름을, **@propertyvalue** 에 새 설정을 지정합니다.  
  
3.  (옵션) 설정할 각 Xactset 작업 속성에 대해 2단계를 반복합니다. 변경 하는 경우는 `xactsetjobinterval` 속성을 적용 하려면 새 간격에 대 한 Oracle 게시자의 작업을를 다시 시작 해야 합니다.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>트랜잭션 세트 작업의 속성을 보려면  
  
1.  배포자에서 [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql)을 실행합니다. **@publisher** 에 Oracle 게시자의 이름을 지정합니다.  
  
### <a name="to-disable-the-transaction-set-job"></a>트랜잭션 세트 작업을 사용하지 않도록 설정하려면  
  
1.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. Oracle 게시자의 이름을 지정 **@publisher** 에 값 `xactsetjob` 에 대 한 **@propertyname** 를 값 `disabled` 에 대 한 **@propertyvalue** .  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Xactset` 작업을 사용하도록 설정하고 실행 간격을 3분으로 설정합니다.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>관련 항목  
 [Oracle 게시자를 위한 성능 튜닝](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
