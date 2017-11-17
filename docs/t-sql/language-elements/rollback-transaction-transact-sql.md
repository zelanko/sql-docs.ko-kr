---
title: ROLLBACK TRANSACTION (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROLLBACK TRANSACTION
- ROLLBACK
- ROLLBACK_TSQL
- ROLLBACK_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- ROLLBACK TRANSACTION statement
- erasing data modifications [SQL Server]
- rolling back transactions, ROLLBACK TRANSACTION
- roll back transactions [SQL Server]
- savepoints [SQL Server]
ms.assetid: 6882c5bc-ff74-476a-984b-164aeb036c66
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 6e754198cf82a7ba0752fe8f20c3780a8ac551d7
ms.openlocfilehash: 7a7cf37490b1dab17a061104ab14b5d11d26632d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/14/2017

---
# <a name="rollback-transaction-transact-sql"></a>ROLLBACK TRANSACTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  명시적 또는 암시적인 트랜잭션을 트랜잭션의 처음이나 트랜잭션 내의 저장점으로 롤백합니다. ROLLBACK TRANSACTION을 사용하여 트랜잭션의 시작 이후 또는 저장점까지의 모든 데이터 수정 사항을 지울 수 있습니다. 또한 트랜잭션에서 보유한 리소스도 해제합니다.  
  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ROLLBACK { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable  
     | savepoint_name | @savepoint_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *transaction_name*  
 BEGIN TRANSACTION에서 트랜잭션에 할당된 이름입니다. *transaction_name* 식별자에 대 한 규칙을 따라야 하지만 트랜잭션 이름의 처음 32 자만 사용 됩니다. 트랜잭션을 중첩할 경우 *transaction_name* 가장 바깥쪽 BEGIN TRANSACTION 문에서 이름 이어야 합니다. *transaction_name* 는 항상 대/소문자 구분, 경우에 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구분 하지 않습니다.  
  
 **@***tran_name_variable*  
 유효한 트랜잭션 이름이 포함된 사용자 정의 변수의 이름입니다. 변수를 사용 하 여 선언 해야 합니다는 **char**, **varchar**, **nchar**, 또는 **nvarchar** 데이터 형식입니다.  
  
 *savepoint_name*  
 *savepoint_name* SAVE TRANSACTION 문의 합니다. *savepoint_name* 식별자에 대 한 규칙을 따라야 합니다. 사용 하 여 *savepoint_name* 조건부 롤백이 트랜잭션의 일부에만 영향을 경우.  
  
 **@***savepoint_variable*  
 유효한 저장점 이름이 포함된 사용자 정의 변수의 이름입니다. 변수를 사용 하 여 선언 해야 합니다는 **char**, **varchar**, **nchar**, 또는 **nvarchar** 데이터 형식입니다.  
  
## <a name="error-handling"></a>오류 처리  
 ROLLBACK TRANSACTION 문에서는 사용자에게 메시지를 제공하지 않습니다. 저장 프로시저나 트리거에 경고가 필요한 경우 RAISERROR 또는 PRINT 문을 사용하세요. 오류를 표시하는 데는 RAISERROR 문을 사용하는 것이 좋습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 없는 ROLLBACK TRANSACTION을 *savepoint_name* 또는 *transaction_name* 트랜잭션의 시작 부분으로 롤백합니다. 트랜잭션을 중첩할 경우 이 문에서는 모든 내부 트랜잭션을 가장 바깥쪽 BEGIN TRANSACTION 문으로 롤백합니다. 두 경우 모두 ROLLBACK TRANSACTION 감소는 @@TRANCOUNT 시스템 함수를 0으로 합니다. ROLLBACK TRANSACTION *savepoint_name* @ 감소 시 키 지 않는@TRANCOUNT합니다.  
  
 ROLLBACK TRANSACTION을 참조할 수 없습니다는 *savepoint_name* BEGIN DISTRIBUTED TRANSACTION으로 명시적으로 하거나 분산된 트랜잭션을 시작 하거나 로컬 트랜잭션에서 에스컬레이션 합니다.  
  
 COMMIT TRANSACTION 문이 실행된 후에는 트랜잭션을 롤백할 수 없습니다. 단, COMMIT TRANSACTION이 롤백되는 트랜잭션 내에 포함된 중첩된 트랜잭션과 연결되어 있는 경우는 제외됩니다. 이 인스턴스에서 중첩된 트랜잭션 하는 롤백되거나에 대 한 COMMIT TRANSACTION을 실행 한 경우에 합니다.  
  
 트랜잭션에서 중복되는 저장점 이름이 허용되지만 중복되는 저장점 이름을 사용하는 ROLLBACK TRANSACTION은 해당 저장점 이름을 사용하여 가장 최근의 SAVE TRANSACTION으로만 롤백합니다.  
  
## <a name="interoperability"></a>상호 운용성  
 저장 프로시저에 없는 ROLLBACK TRANSACTION 문은 한 *savepoint_name* 또는 *transaction_name* 모든 문을 가장 바깥쪽 BEGIN TRANSACTION으로 롤백합니다. @ 발생 하는 저장된 프로시저의 ROLLBACK TRANSACTION 문@TRANCOUNT 보다 저장된 프로시저가 완료 될 때 다른 값을 포함 하는 @@TRANCOUNT 정보 메시지를 생성 하는 저장된 프로시저를 호출할 때 값입니다. 이 메시지는 후속 처리에 영향을 미치지 않습니다.  
  
 트리거에서 ROLLBACK TRANSACTION이 발생한 경우  
  
-   현재 트랜잭션의 해당 지점까지 이루어진 모든 데이터 수정 사항은 트리거의 수정 사항을 포함하여 롤백합니다.  
  
-   트리거에서는 ROLLBACK 문 다음에 남아있는 모든 문을 계속 실행합니다. 이 문 중에서 데이터를 수정한 경우 수정 사항은 롤백되지 않습니다. 남아있는 이 문을 실행하여 중첩 트리거가 발생하지 않습니다.  
  
-   트리거를 발생시키는 문 다음의 일괄 처리에 있는 문은 실행되지 않습니다.  
  
@@TRANCOUNT 는 자동 커밋 모드에도 트리거를 입력 하면 1 씩 증가 합니다. 시스템은 트리거를 암시적인 중첩 트랜잭션으로 처리합니다.  
  
저장 프로시저의 ROLLBACK TRANSACTION 문은 해당 프로시저를 호출하는 일괄 처리의 다음 문에 영향을 미치지 않습니다. 일괄 처리의 다음 문이 실행됩니다. 트리거의 ROLLBACK TRANSACTION 문은 트리거를 발생시킨 문이 포함된 일괄 처리를 종료합니다. 일괄 처리의 다음 문은 실행되지 않습니다.  
  
커서에 대한 ROLLBACK의 결과는 다음 3가지 규칙으로 정의합니다.  
  
1.  CURSOR_CLOSE_ON_COMMIT을 ON으로 설정하면 ROLLBACK에서는 모든 열려있는 커서의 할당을 취소하지 않습니다.  
  
2.  CURSOR_CLOSE_ON_COMMIT을 OFF로 설정하면 ROLLBACK에서는 완전히 채운 열려있는 모든 동기 STATIC이나 INSENSITIVE 커서 또는 비동기 STATIC 커서에 영향을 미치지 않습니다. 다른 유형의 열려있는 커서는 닫히지만 할당이 취소되지는 않습니다.  
  
3.  일괄 처리를 종료하고 내부 롤백을 생성하는 오류는 오류 문이 포함된 일괄 처리에서 선언한 모든 커서의 할당을 취소합니다. 모든 커서는 유형이나 CURSOR_CLOSE_ON_COMMIT 설정에 상관없이 할당이 취소됩니다. 여기에는 오류 일괄 처리에서 호출한 저장 프로시저에서 선언한 커서가 포함됩니다. 오류 일괄 처리 전에 일괄 처리에서 선언한 커서는 규칙 1 과 2를 따릅니다. 교착 상태 오류가 이런 유형의 오류 예입니다. 트리거에서 발생한 ROLLBACK 문도 자동으로 이런 유형의 오류를 만듭니다.  
  
## <a name="locking-behavior"></a>잠금 동작  
 지정 하는 ROLLBACK TRANSACTION 문은 한 *savepoint_name* 에스컬레이션과 변환을 제외 하 고 저장 점을 초과 획득 한 모든 잠금을 해제 합니다. 이러한 잠금은 해제되지 않으며 이전 잠금 모드로 다시 변환되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 명명된 트랜잭션을 롤백한 결과를 보여 줍니다. 테이블을 만든 후에 다음 문은 명명 된 트랜잭션을 시작, 두 개의 행을 삽입 하 고 변수에 명명 된 트랜잭션을 롤백 후 @TransactionName합니다. 명명 된 트랜잭션 외부에서 다른 문을 두 개의 행을 삽입 합니다. 쿼리는 이전 문의 결과 반환합니다.   
  
```sql    
USE tempdb;  
GO  
CREATE TABLE ValueTable ([value] int);  
GO  
  
DECLARE @TransactionName varchar(20) = 'Transaction1';  
  
BEGIN TRAN @TransactionName  
       INSERT INTO ValueTable VALUES(1), (2);  
ROLLBACK TRAN @TransactionName;  
  
INSERT INTO ValueTable VALUES(3),(4);  
  
SELECT [value] FROM ValueTable;  
  
DROP TABLE ValueTable;  
```  
[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]  
```  
value  
-----   
3    
4  
```  
  
  
## <a name="see-also"></a>관련 항목:  
 [BEGIN DISTRIBUTED TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [커밋 작업 &#40; Transact SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK WORK &#40; Transact SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  

