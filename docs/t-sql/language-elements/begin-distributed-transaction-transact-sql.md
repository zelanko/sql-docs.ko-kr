---
title: BEGIN DISTRIBUTED TRANSACTION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2016
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DISTRIBUTED
- BEGIN_DISTRIBUTED_TRANSACTION_TSQL
- DISTRIBUTED_TSQL
- BEGIN DISTRIBUTED TRANSACTION
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN DISTRIBUTED TRANSACTION statement
- distributed transactions [SQL Server], starting
- MS DTC, transaction management
- distributed transactions [SQL Server], BEGIN DISTRIBUTED TRANSACTION statement
- servers [SQL Server], distributed transactions
- starting distributed transactions
- remote servers [SQL Server], distributed transactions
- starting transactions
ms.assetid: c3bc2716-39d3-4061-8c6a-8734899231ac
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9ffa8e41ef713891227994a79c1179e16992f9d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33065690"
---
# <a name="begin-distributed-transaction-transact-sql"></a>BEGIN DISTRIBUTED TRANSACTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] Distributed Transaction Coordinator(MS DTC)에서 관리되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 분산 트랜잭션을 시작하도록 지정합니다.  
    
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
BEGIN DISTRIBUTED { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *transaction_name*  
 MS DTC 유틸리티에서 분산 트랜잭션을 추적하는 데 사용되는 사용자 정의 트랜잭션 이름입니다. *transaction_name*은 식별자 규칙을 따라야 하며 \<=32자여야 합니다.  
  
 @*tran_name_variable*  
 MS DTC 유틸리티에서 분산 트랜잭션 추적에 사용되는 트랜잭션 이름이 포함된 사용자 정의 변수의 이름입니다. 변수는 **char**, **varchar**, **nchar** 또는 **nvarchar** 데이터 형식으로 선언해야 합니다.  
  
## <a name="remarks"></a>Remarks  
 BEGIN DISTRIBUTED TRANSACTION 문을 실행하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스는 트랜잭션 주관자로서 트랜잭션의 수행을 제어합니다. 이후 세션에 대해 COMMIT TRANSACTION 또는 ROLLBACK TRANSACTION 문을 실행하면 제어 인스턴스는 포함된 모든 인스턴스 간의 분산 트랜잭션 완료를 MS DTC에서 관리하도록 요청합니다.  
  
 트랜잭션 수준의 스냅숏 격리는 분산 트랜잭션을 지원하지 않습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 원격 인스턴스가 분산 트랜잭션에 참여하는 기본적인 방법은 이미 분산 트랜잭션에 참여한 세션이 연결된 서버를 참조하는 분산 쿼리를 실행할 때 참여하는 것입니다.  
  
 예를 들어 BEGIN DISTRIBUTED TRANSACTION이 서버 A에서 실행되는 경우 해당 세션은 서버 B에서 저장 프로시저를 호출하고 서버 C에서 다른 저장 프로시저를 호출합니다. 서버 C의 저장 프로시저가 서버 D에 대해 분산 쿼리를 수행하면 4개의 컴퓨터가 모두 분산 트랜잭션에 포함되게 됩니다. 서버 A의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스는 트랜잭션에 대한 원본 제어 인스턴스입니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 분산 트랜잭션에 포함된 세션은 분산 트랜잭션에 명시적으로 참여하도록 다른 세션에 전달할 수 있는 트랜잭션 개체를 얻을 수 없습니다. 원격 서버가 트랜잭션에 참여하는 유일한 방법은 원격 저장 프로시저 호출이나 분산 쿼리의 대상이 되는 것입니다.  
  
 로컬 트랜잭션에서 분산 쿼리를 실행하면 대상 OLE DB 데이터 원본이 ITransactionLocal을 지원할 경우 해당 트랜잭션이 자동으로 분산 트랜잭션으로 승격됩니다.  대상 OLE DB 데이터 원본이 ITransactionLocal을 지원하지 않을 경우 분산 쿼리에서 읽기 전용 작업만 허용됩니다.  
  
 분산 트랜잭션에 이미 참여한 세션은 원격 서버를 참조하는 원격 저장 프로시저 호출을 수행합니다.  
  
 **sp_configure remote proc trans** 옵션은 로컬 트랜잭션에서 원격 저장 프로시저를 호출하면 자동으로 로컬 트랜잭션이 MS DTC에서 관리되는 분산 트랜잭션으로 승격되도록 할지를 제어합니다. 연결 수준의 SET 옵션 REMOTE_PROC_TRANSACTIONS를 사용하여 **sp_configure remote proc trans**에서 설정한 인스턴스 기본값을 무시할 수 있습니다. 이 옵션을 on으로 설정하면 원격 저장 프로시저 호출에 의해 로컬 트랜잭션이 분산 트랜잭션으로 승격됩니다. MS DTC 트랜잭션을 만든 연결은 트랜잭션 주관자가 되며  COMMIT TRANSACTION은 MS DTC 통합 커밋을 시작합니다. **sp_configure remote proc trans** 옵션이 ON인 경우 BEGIN TRANSACTION 대신 BEGIN DISTRIBUTED TRANSACTION을 실행하도록 응용 프로그램을 다시 작성할 필요 없이 로컬 트랜잭션의 원격 저장 프로시저 호출이 분산 트랜잭션의 일부로 자동 보호됩니다.  
  
 분산 트랜잭션 환경 및 프로세스에 대한 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator 설명서를 참조하십시오.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]의 로컬 인스턴스 및 원격 서버의 인스턴스에 있는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 데이터베이스에서 후보를 삭제합니다. 로컬 및 원격 데이터베이스는 모두 트랜잭션을 커밋하거나 롤백합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 실행하는 컴퓨터에 MS DTC가 현재 설치되어 있지 않으면 이 예에서 오류 메시지가 나타납니다. MS DTC 설치 방법은 Microsoft Distributed Transaction Coordinator 설명서를 참조하십시오.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN DISTRIBUTED TRANSACTION;  
-- Delete candidate from local instance.  
DELETE AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
-- Delete candidate from remote instance.  
DELETE RemoteServer.AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
