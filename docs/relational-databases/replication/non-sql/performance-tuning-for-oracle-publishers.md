---
title: "Oracle 게시자를 위한 성능 튜닝 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], performance tuning
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 43042f93e80be4f9bf7c5044cc11791c614d85f0
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="performance-tuning-for-oracle-publishers"></a>Oracle 게시자를 위한 성능 튜닝
  Oracle 게시 아키텍처는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시 아키텍처와 유사하므로 성능을 개선하기 위한 Oracle 복제 튜닝의 첫 단계는 [Enhance General Replication Performance](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)의 일반 튜닝 권장 사항을 따르는 것입니다.  
  
 또한 Oracle 게시자 성능과 관련된 다음 두 가지 방법을 사용할 수 있습니다.  
  
-   Oracle 또는 Oracle Gateway 중에서 적절한 게시 옵션 지정  
  
-   적절한 간격으로 게시자의 변경 내용을 처리하도록 트랜잭션 세트 작업 구성  
  
## <a name="specifying-the-appropriate-publishing-option"></a>적절한 게시 옵션 지정  
 Oracle Gateway 옵션은 Oracle Complete 옵션을 사용할 때보다 더 나은 성능을 제공하지만 여러 트랜잭션 게시에서 동일한 테이블을 게시할 때는 사용할 수 없습니다. 트랜잭션 게시의 경우 특정 테이블이 한 번만 나타날 수 있지만 스냅숏 게시의 경우에는 이러한 제한이 없습니다. 여러 트랜잭션 게시에서 동일한 테이블을 게시해야 할 경우에는 Oracle Complete 옵션을 선택하십시오. 이 옵션은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 Oracle 게시자를 식별할 때 지정할 수 있습니다. 자세한 내용은 [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)을(를) 참조하세요.  
  
## <a name="configuring-the-transaction-set-job"></a>트랜잭션 세트 작업 구성  
 게시된 Oracle 테이블에 대한 변경 내용은 트랜잭션 세트라는 그룹으로 처리됩니다. 트랜잭션 일관성을 유지하려면 각 트랜잭션 세트를 배포 데이터베이스에 단일 트랜잭션으로 커밋해야 합니다. 트랜잭션 세트가 너무 클 경우 단일 트랜잭션으로는 효율적으로 처리할 수 없습니다.  
  
 기본적으로 트랜잭션 세트는 로그 판독기 에이전트에서만 생성됩니다. 변경 작업이 많이 수행되는 기간 동안 로그 판독기 에이전트가 실행되지 않거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 Oracle 게시자로 연결할 수 없는 경우 트랜잭션 세트가 관리할 수 없을 정도로 커질 수 있습니다. 이러한 문제를 방지하려면 로그 판독기 에이전트가 실행되지 않거나 Oracle 게시자에 연결할 수 없는 경우에도 트랜잭션 세트를 정기적으로 만들어야 합니다.  
  
 트랜잭션 세트는 로그 판독기 에이전트가 세트를 만들 때 사용하는 메커니즘과 동일한 메커니즘을 사용하는 Xactset 작업(복제 시 설치되는 Oracle 데이터베이스 작업)을 사용하여 만들 수 있습니다. 작업이 실행될 때마다 새 트랜잭션 세트가 생성됩니다. 다음에 로그 판독기 에이전트가 실행되면 해당 에이전트는 생성된 모든 세트를 처리합니다. 기존의 트랜잭션 세트가 모두 처리된 다음에도 보류 중인 변경 내용이 남아 있는 경우 로그 판독기 에이전트에서 하나 이상의 트랜잭션 세트를 추가로 만들어서 처리합니다.  
  
 트랜잭션 집합 작업을 구성하려면 [Oracle 게시자에 대한 트랜잭션 집합 작업 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
