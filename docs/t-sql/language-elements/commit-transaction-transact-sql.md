---
title: "트랜잭션 커밋 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COMMIT
- COMMIT TRANSACTION
- COMMIT_TSQL
- COMMIT_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- user-defined transactions [SQL Server]
- committed transactions
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- implicit transactions
- distributed transactions [SQL Server], committed
- transactions [SQL Server], committed
- COMMIT TRANSACTION statement
- rolling back transactions, COMMIT TRANSACTION
ms.assetid: f8fe26a9-7911-497e-b348-4e69c7435dc1
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 84ca8221700d3eabd443b84d97dea4f698e9f945
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="commit-transaction-transact-sql"></a>COMMIT TRANSACTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  성공적인 암시적 트랜잭션이나 명시적 트랜잭션의 끝을 표시합니다. @ If@TRANCOUNT 1 이면 COMMIT TRANSACTION을 사용 하면 @ 감소 고 트랜잭션에서 보유 한 리소스를 해제 하는 데이터베이스의 영구적인 부분이 트랜잭션이 시작 된 이후로 수행 된 모든 데이터 수정 내용을@TRANCOUNT 0입니다. @ If@TRANCOUNT @ 1 이면 COMMIT TRANSACTION 감소 보다 크면@TRANCOUNT 1과 트랜잭션이 의해서만 활성 상태를 유지 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Applies to SQL Server (starting with 2008) and Azure SQL Database
  
COMMIT [ { TRAN | TRANSACTION }  [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]  
[ ; ]  
```  
 
```  
-- Applies to Azure SQL Data Warehouse and Parallel Data Warehouse Database
  
COMMIT [ TRAN | TRANSACTION ] 
[ ; ]  
``` 
 
  
## <a name="arguments"></a>인수  
 *transaction_name*  
 **적용 대상:** SQL Server 및 Azure SQL 데이터베이스
 
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 무시됩니다. *transaction_name* 은 이전의 BEGIN TRANSACTION에서 할당 된 트랜잭션 이름을 지정 합니다. *transaction_name*식별자에 대 한 규칙을 따라야 하지만 32 자를 초과할 수 없습니다. *transaction_name* 된 중첩 BEGIN TRANSACTION COMMIT TRANSACTION과 연관 되어 있는 프로그래머에 게 지정 하 여 가독성으로 사용할 수 있습니다.  
  
 *@tran_name_variable*  
 **적용 대상:** SQL Server 및 Azure SQL 데이터베이스  
 
유효한 트랜잭션 이름이 포함된 사용자 정의 변수의 이름입니다. Char, varchar, nchar 또는 nvarchar 데이터 형식의 변수 선언 되어야 합니다. 33개 이상의 문자가 변수에 전달되는 경우 32자만이 사용되고 나머지 문자는 잘립니다.  
  
 DELAYED_DURABILITY  
 **적용 대상:** SQL Server 및 Azure SQL 데이터베이스   

 이 트랜잭션이 지연된 영속성으로 커밋되도록 요청하는 옵션입니다. 데이터베이스가 `DELAYED_DURABILITY = DISABLED` 또는 `DELAYED_DURABILITY = FORCED`를 사용하여 변경된 경우 요청이 무시됩니다. 항목을 참조 [트랜잭션 내구성 제어](../../relational-databases/logs/control-transaction-durability.md) 자세한 정보에 대 한 합니다.  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그래머는 트랜잭션에서 참조되는 모든 데이터가 논리적으로 정확할 때만 COMMIT TRANSACTION을 실행해야 합니다.  
  
 커밋된 트랜잭션이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 분산 트랜잭션일 경우 COMMIT TRANSACTION은 MS DTC가 2단계 커밋 프로토콜을 사용하여 트랜잭션에 포함된 모든 서버를 커밋하도록 트리거합니다. 로컬 트랜잭션이 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 동일한 인스턴스에서 둘 이상의 데이터베이스와 관련되어 있을 경우 인스턴스는 내부적으로 2단계 커밋을 사용하여 트랜잭션에 포함된 모든 데이터베이스를 커밋할 수 있습니다.  
  
 COMMIT TRANSACTION을 중첩된 트랜잭션에서 사용할 경우 내부 트랜잭션을 커밋해도 리소스가 해제되거나 수정 내용이 영구적으로 반영되지 않습니다. 이런 경우 외부 트랜잭션을 커밋해야만 데이터 수정 내용이 영구적으로 반영되고 리소스가 해제됩니다. 각 COMMIT TRANSACTION을 발급 한 경우 @@TRANCOUNT 1 단순히 감소 @ 보다 크면@TRANCOUNT 1입니다. @ 때@TRANCOUNT 은 0으로 감소 하도록 마지막으로, 전체 외부 트랜잭션이 커밋됩니다. 때문에 *transaction_name* 에서 무시는 [!INCLUDE[ssDE](../../includes/ssde-md.md)], 해결 되지 않은 내부 트랜잭션이 @ 만큼 줄어듭니다 없는 경우 외부 트랜잭션의 이름을 참조 하는 COMMIT TRANSACTION을 실행@TRANCOUNT 1 씩 합니다.  
  
 COMMIT TRANSACTION을 실행 될 때 @@TRANCOUNT 오류가 0 결과는는 해당 BEGIN TRANSACTION이 없습니다.  
  
 COMMIT TRANSACTION 문을 실행한 후에는 데이터 수정 내용이 데이터베이스에 영구적으로 반영되므로 트랜잭션을 롤백할 수 없습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 문이 시작될 때 트랜잭션 수가 0인 경우에만 문에서 트랜잭션 수를 증가시킵니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-committing-a-transaction"></a>1. 트랜잭션 커밋  
**적용 대상:** SQL Server, Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스   

다음 예에서는 작업 후보를 삭제합니다. AdventureWorks를 사용합니다. 
  
```   
BEGIN TRANSACTION;   
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;   
COMMIT TRANSACTION;   
```  
  
### <a name="b-committing-a-nested-transaction"></a>2. 중첩된 트랜잭션 커밋  
**적용 대상:** SQL Server 및 Azure SQL 데이터베이스    

다음 예에서는 테이블을 만들고 3단계로 중첩된 트랜잭션을 생성한 다음 중첩된 트랜잭션을 커밋합니다. 하지만 각 `COMMIT TRANSACTION` 문에는 *transaction_name* 매개 변수 간에 관계가 없습니다는 `COMMIT TRANSACTION` 및 `BEGIN TRANSACTION` 문. *transaction_name* 매개 변수는 단지 프로그래머가 개수의 커밋이 감소 코딩 되었는지 확인할 수 있도록 `@@TRANCOUNT` 를 0으로 만들고 외부 트랜잭션을 커밋합니다. 
  
```   
IF OBJECT_ID(N'TestTran',N'U') IS NOT NULL  
    DROP TABLE TestTran;  
GO  
CREATE TABLE TestTran (Cola int PRIMARY KEY, Colb char(3));  
GO  
-- This statement sets @@TRANCOUNT to 1.  
BEGIN TRANSACTION OuterTran;  
  
PRINT N'Transaction count after BEGIN OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
INSERT INTO TestTran VALUES (1, 'aaa');  
 
-- This statement sets @@TRANCOUNT to 2.  
BEGIN TRANSACTION Inner1;  
 
PRINT N'Transaction count after BEGIN Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (2, 'bbb');  
  
-- This statement sets @@TRANCOUNT to 3.  
BEGIN TRANSACTION Inner2;  
  
PRINT N'Transaction count after BEGIN Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (3, 'ccc');  
  
-- This statement decrements @@TRANCOUNT to 2.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner2;  
 
PRINT N'Transaction count after COMMIT Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
-- This statement decrements @@TRANCOUNT to 1.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner1;  
 
PRINT N'Transaction count after COMMIT Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
-- This statement decrements @@TRANCOUNT to 0 and  
-- commits outer transaction OuterTran.  
COMMIT TRANSACTION OuterTran;  
  
PRINT N'Transaction count after COMMIT OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
```  
  
## <a name="see-also"></a>관련 항목:  
 [BEGIN DISTRIBUTED TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [커밋 작업 &#40; Transact SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40; Transact SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  

