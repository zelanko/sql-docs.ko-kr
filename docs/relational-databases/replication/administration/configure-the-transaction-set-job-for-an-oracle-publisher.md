---
title: Oracle 게시자에 대한 트랜잭션 집합 작업 구성 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 98a23215063456a8379abda8384545b5c5e8e15a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812861"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher"></a>Oracle 게시자에 대한 트랜잭션 집합 작업 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Xactset** 작업은 로그 판독기 에이전트가 Oracle 게시자에 연결되어 있지 않을 때 해당 게시자에서 트랜잭션 세트를 만들기 위해 실행되는 복제를 통해 만들어지는 Oracle 데이터베이스 작업입니다. 배포자에서 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 이 작업을 사용하도록 설정하고 구성할 수 있습니다. 자세한 내용은 [Oracle 게시자를 위한 성능 튜닝](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)을 참조하세요.  
  
### <a name="to-enable-the-transaction-set-job"></a>트랜잭션 세트 작업을 사용하도록 설정하려면  
  
1.  Oracle 게시자에서 **job_queue_processes** 초기화 매개 변수를 Xactset 작업을 실행하기에 충분한 값으로 설정합니다. 이 매개 변수에 대한 자세한 내용은 Oracle 게시자의 데이터베이스 설명서를 참조하십시오.  
  
2.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)를 실행합니다. **@publisher**에 Oracle 게시자 이름을, **@propertyname**에 **xactsetbatching** 값을, **@propertyvalue**에 **enabled** 값을 지정합니다.  
  
3.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)를 실행합니다. **@publisher**에 Oracle 게시자의 이름을, **@propertyname**에 **xactsetjobinterval** 값을, **@propertyvalue**에 작업 간격(분)을 지정합니다.  
  
4.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)를 실행합니다. **@publisher**에 Oracle 게시자의 이름을, **@propertyname**에 **xactsetjob** 값을, **@propertyvalue**에 **enabled** 값을 지정합니다.  
  
### <a name="to-configure-the-transaction-set-job"></a>트랜잭션 세트 작업을 구성하려면  
  
1.  (선택 사항) 배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)를 실행합니다. **@publisher**에 Oracle 게시자의 이름을 지정합니다. 이렇게 하면 게시자에서 **Xactset** 작업의 속성이 반환됩니다.  
  
2.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)를 실행합니다. **@publisher**에 Oracle 게시자의 이름을, **@propertyname**에 설정되는 Xactset 작업 속성의 이름을, **@propertyvalue**에 새 설정을 지정합니다.  
  
3.  (옵션) 설정할 각 Xactset 작업 속성에 대해 2단계를 반복합니다. **xactsetjobinterval** 속성을 변경하는 경우 Oracle 게시자의 작업을 다시 시작해야 새 간격이 적용됩니다.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>트랜잭션 세트 작업의 속성을 보려면  
  
1.  배포자에서 [sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md)을 실행합니다. **@publisher**에 Oracle 게시자의 이름을 지정합니다.  
  
### <a name="to-disable-the-transaction-set-job"></a>트랜잭션 세트 작업을 사용하지 않도록 설정하려면  
  
1.  배포자에서 [sp_publisherproperty&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)를 실행합니다. **@publisher**에 Oracle 게시자의 이름을, **@propertyname**에 **xactsetjob** 값을, **@propertyvalue**에 **disabled** 값을 지정합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Xactset` 작업을 사용하도록 설정하고 실행 간격을 3분으로 설정합니다.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure-the-transactio_1.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자를 위한 성능 튜닝](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
