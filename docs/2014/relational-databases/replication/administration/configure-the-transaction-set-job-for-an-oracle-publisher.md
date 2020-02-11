---
title: Oracle 게시자에 대 한 트랜잭션 집합 작업 구성 (복제 Transact-sql 프로그래밍) | Microsoft Docs
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
ms.openlocfilehash: 48282f08df588f54b6f03a0b99c58a2f0cf039ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67793538"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>Oracle 게시자에 대한 트랜잭션 세트 작업 구성(복제 Transact-SQL 프로그래밍)
  **Xactset** 작업은 게시자에 연결 되어 있지 않을 로그 판독기 에이전트 때 트랜잭션 집합을 만들기 위해 oracle 게시자에서 실행 되는 복제를 통해 만들어지는 oracle 데이터베이스 작업입니다. 배포자에서 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 이 작업을 사용하도록 설정하고 구성할 수 있습니다. 자세한 내용은 [Oracle 게시자를 위한 성능 튜닝](../non-sql/performance-tuning-for-oracle-publishers.md)을 참조하세요.  
  
### <a name="to-enable-the-transaction-set-job"></a>트랜잭션 세트 작업을 사용하도록 설정하려면  
  
1.  Oracle 게시자에서 **job_queue_processes** 초기화 매개 변수를 Xactset 작업을 실행하기에 충분한 값으로 설정합니다. 이 매개 변수에 대한 자세한 내용은 Oracle 게시자의 데이터베이스 설명서를 참조하십시오.  
  
2.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. ** \@게시자**에 대 한 Oracle 게시자의 이름, ** \@propertyname**의 경우 값 `xactsetbatching` , ** \@propertyvalue** `enabled` 에 값을 지정 합니다.  
  
3.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. ** \@게시자**에 대 한 Oracle 게시자의 이름, ** \@propertyname**의 경우 값 `xactsetjobinterval` , ** \@propertyvalue**의 작업 간격 (분)을 지정 합니다.  
  
4.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. ** \@게시자**에 대 한 Oracle 게시자의 이름, ** \@propertyname**의 경우 값 `xactsetjob` , ** \@propertyvalue** `enabled` 에 값을 지정 합니다.  
  
### <a name="to-configure-the-transaction-set-job"></a>트랜잭션 세트 작업을 구성하려면  
  
1.  (선택 사항) 배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. ** \@게시자**에 대 한 Oracle 게시자의 이름을 지정 합니다. 이렇게 하면 게시자에서 **Xactset** 작업의 속성이 반환됩니다.  
  
2.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. ** \@게시자**에 대 한 Oracle 게시자의 이름, ** \@propertyname**에 대해 설정할 Xactset 작업 속성의 이름 및 ** \@propertyvalue**의 새 설정을 지정 합니다.  
  
3.  (옵션) 설정할 각 Xactset 작업 속성에 대해 2단계를 반복합니다. `xactsetjobinterval` 속성을 변경 하는 경우 Oracle 게시자의 작업을 다시 시작 해야 새 간격이 적용 됩니다.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>트랜잭션 세트 작업의 속성을 보려면  
  
1.  배포자에서 [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql)을 실행합니다. ** \@게시자**에 대 한 Oracle 게시자의 이름을 지정 합니다.  
  
### <a name="to-disable-the-transaction-set-job"></a>트랜잭션 세트 작업을 사용하지 않도록 설정하려면  
  
1.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)를 실행합니다. ** \@게시자**에 대 한 Oracle 게시자의 이름, ** \@propertyname**의 경우 값 `xactsetjob` , ** \@propertyvalue** `disabled` 에 값을 지정 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Xactset` 작업을 사용하도록 설정하고 실행 간격을 3분으로 설정합니다.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자를 위한 성능 튜닝](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
