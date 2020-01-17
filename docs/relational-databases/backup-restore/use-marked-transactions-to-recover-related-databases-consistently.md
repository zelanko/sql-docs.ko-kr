---
title: 데이터베이스를 표시된 트랜잭션으로 복원
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction marks [SQL Server]
- marked transactions [SQL Server]
- database restores [SQL Server], inserting transaction marks for
- recovery [SQL Server], related databases
- restoring databases [SQL Server], related database recovery
- database restores [SQL Server], related databases
- marked transactions [SQL Server], creating
- BEGIN TRAN...WITH MARK statement
- two-phase commit
ms.assetid: 50a73574-1a69-448e-83dd-9abcc7cb7e1a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bc572ac7e1272274996b13dfb0886427cebc128e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247443"
---
# <a name="use-marked-transactions-to-recover-related-databases-consistently"></a>표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 전체 또는 대량 로그 복구 모델을 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다.  
  
 두 개 이상의 데이터베이스, 즉 *관련 데이터베이스*에 관련 업데이트를 수행할 경우 트랜잭션 표시를 사용하여 해당 데이터베이스를 논리적으로 일치하는 지점으로 복구할 수 있습니다. 그러나 이러한 방법으로 복구를 수행하면 복구 지점으로 사용된 표시 뒤에 커밋된 모든 트랜잭션이 손실됩니다. 트랜잭션 표시는 관련 데이터베이스를 테스트하거나 최근 커밋된 트랜잭션을 손실해도 상관없는 경우에만 적합합니다.  
  
 모든 관련 데이터베이스의 관련 트랜잭션을 정기적으로 표시하면 데이터베이스에 일련의 공통 복구 지점이 설정됩니다. 트랜잭션 표시는 트랜잭션 로그에 기록되고 로그 백업에 포함됩니다. 재해가 발생할 경우 각 데이터베이스를 동일한 트랜잭션 표시로 복원하여 해당 데이터베이스를 일치하는 지점으로 복구할 수 있습니다.  
  
> [!NOTE]  
>  서로 다른 데이터베이스의 로그 백업은 개별적으로 만들 수 있으며 동시에 만들 필요가 없습니다.  
  
 다음 시나리오에서 관련 데이터베이스를 복구하려면 모든 관련 데이터베이스의 트랜잭션에 이미 표시가 있어야 합니다.  
  
-   하나 이상의 트랜잭션 로그가 손상되었습니다. 마지막 로그 백업과 같은 상태로 데이터베이스 집합을 복원해야 합니다.  
  
-   이전 시점의 서로 일치하는 상태로 전체 데이터베이스 집합을 복원해야 합니다.  
  
> [!IMPORTANT]  
>  표시된 트랜잭션에만 관련된 데이터베이스를 복구할 수 있으며 지정 시간과는 관련이 없습니다.  
  
 표시하는 트랜잭션을 만드는 방법은 이 항목의 뒷부분에 나오는 "표시된 트랜잭션 만들기"를 참조하십시오.  
  
## <a name="typical-scenario-for-using-marked-transactions"></a>표시된 트랜잭션 사용에 대한 일반적인 시나리오  
 표시된 트랜잭션 사용에 대한 일반적인 시나리오는 다음 단계로 구성됩니다.  
  
1.  각 관련 데이터베이스의 전체 또는 차등 데이터베이스 백업 만들기  
  
2.  모든 데이터베이스에서 트랜잭션 블록 표시  
  
3.  모든 데이터베이스의 트랜잭션 로그 백업  
  
4.  WITH NORECOVERY로 데이터베이스 백업 복원  
  
5.  WITH STOPATMARK로 로그 복원  

## <a name="considerations-for-using-marked-transactions"></a>표시된 트랜잭션 사용에 대한 고려 사항  
 트랜잭션 로그에 명명된 표시를 삽입하기 전에 다음 사항을 주의하십시오.  
  
-   트랜잭션 표시는 로그 공간을 소비하므로 데이터베이스 복구 전략에서 중요한 역할을 하는 트랜잭션에 대해서만 사용해야 합니다.  
  
-   표시된 트랜잭션을 커밋한 후에 [msdb](../../relational-databases/system-tables/logmarkhistory-transact-sql.md) 의 **logmarkhistory**테이블에 행이 삽입됩니다.  
  
-   표시된 트랜잭션이 같은 데이터베이스 서버 또는 다른 서버의 다중 데이터베이스에 걸쳐 있으면 영향 받은 모든 데이터베이스의 로그에 표시가 기록됩니다.  
  
## <a name="creating-the-marked-transactions"></a>표시된 트랜잭션 만들기  
 표시된 트랜잭션을 만들려면 [BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md) 문과 WITH MARK [*description*] 절을 사용합니다. 선택 요소인 *description* 은 표시의 텍스트 설명입니다. 트랜잭션의 표시 이름이 필요합니다. 표시 이름은 다시 사용할 수 있습니다. 트랜잭션 로그에는 표시 이름, 설명, 데이터베이스, 사용자, datetime 정보, LSN(로그 시퀀스 번호) 등이 기록됩니다. datetime 정보는 표시 이름과 함께 사용되어 표시를 고유하게 식별합니다.  
  
 **데이터베이스 집합에 표시된 트랜잭션을 만들려면**  
  
1.  BEGIN TRAN 문에서 트랜잭션 이름을 지정하고 WITH MARK 절을 사용합니다.  
  
     BEGIN TRAN *new_mark_name* WITH MARK 문을 기존 트랜잭션 내에 중첩할 수 있습니다. *new_mark_name* 의 값은 트랜잭션에 트랜잭션 이름이 있더라도 트랜잭션의 표시 이름이 됩니다.  
  
    > [!NOTE]  
    >  두 번째로 중첩된 BEGIN TRAN...WITH MARK를 실행하면 해당 문은 건너뛰지만 경고 메시지가 나타납니다.  
  
2.  집합의 모든 데이터베이스에 대해 업데이트를 실행합니다.  
  
     특정 트랜잭션에 대한 표시는 BEGIN TRAN...WITH MARK 문이 실행된 서버 인스턴스의 트랜잭션 로그에만 삽입됩니다. 트랜잭션 표시는 해당 서버 인스턴스에서 표시된 트랜잭션이 업데이트한 모든 데이터베이스의 트랜잭션 로그에 삽입됩니다. 데이터베이스가 서로 다른 서버 인스턴스에 있으면 각 서버 인스턴스에 동일한 표시를 만들어야 합니다.  
  
### <a name="examples"></a>예  
 다음 예에서는 트랜잭션 로그를 복원하여 `ListPriceUpdate`라는 표시된 트랜잭션에 나타냅니다.  
  
```sql  
USE AdventureWorks  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master  
GO  
  
RESTORE DATABASE AdventureWorks  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'ListPriceUpdate';  
```  
  
## <a name="forcing-a-mark-to-spread-to-other-servers"></a>다른 서버에 표시 분산  
 트랜잭션 표시 이름은 트랜잭션이 다른 서버에 분산될 때 자동으로 그 서버에 분산되지 않습니다. 표시를 다른 서버에 분산하려면 BEGIN TRAN *name* WITH MARK 문을 포함하는 저장 프로시저를 작성해야 합니다. 그런 다음 그 저장 프로시저를 원래 서버의 트랜잭션 영역에 있는 원격 서버에서 실행해야 합니다.  
  
 예를 들어 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 있는 분할된 데이터베이스를 생각해 볼 수 있습니다. 각 인스턴스에서 데이터베이스 이름은 `coyote`입니다. 먼저 모든 데이터베이스에 저장 프로시저(예: `sp_SetMark`)를 만듭니다.  
  
```sql  
CREATE PROCEDURE sp_SetMark  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION @name WITH MARK  
UPDATE coyote.dbo.Marks SET one = 1  
COMMIT TRANSACTION;  
GO  
```  
  
 그런 다음 모든 데이터베이스에 표시를 삽입하는 트랜잭션을 포함하는 `sp_MarkAll` 저장 프로시저를 만듭니다. `sp_MarkAll` 을 실행할 수 있습니다.  
  
```sql  
CREATE PROCEDURE sp_MarkAll  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION  
EXEC instance0.coyote.dbo.sp_SetMark @name  
EXEC instance1.coyote.dbo.sp_SetMark @name  
EXEC instance2.coyote.dbo.sp_SetMark @name  
COMMIT TRANSACTION;  
GO  
```  
  
### <a name="two-phase-commit"></a>2단계 커밋  
 분산된 트랜잭션 커밋은 준비 및 커밋의 2단계로 수행됩니다. 표시된 트랜잭션이 커밋되면 표시된 트랜잭션의 각 데이터베이스에 대한 커밋 로그 레코드가 모든 로그에 의심되는 트랜잭션이 없을 때 로그에 기록됩니다. 이때 한 로그에서는 커밋된 것으로 다른 로그에서는 커밋되지 않은 것으로 나타나는 트랜잭션은 분명히 없습니다.  
  
 표시된 트랜잭션을 커밋하는 동안 다음 단계를 수행하여 커밋되지 않은 트랜잭션이 나타나지 않도록 합니다.  
  
1.  표시하는 트랜잭션의 준비 단계는 모든 새 준비 및 커밋을 대기시킵니다.  
  
2.  이미 준비된 트랜잭션의 커밋만 계속할 수 있습니다.  
  
3.  그런 다음 표시하는 트랜잭션은 준비된 모든 트랜잭션이 시간이 만료되어 빠져 나가기를 기다립니다.  
  
4.  표시된 트랜잭션을 준비하고 커밋합니다.  
  
5.  새 준비 및 커밋의 대기를 제거합니다.  
  
 다중 데이터베이스에 걸쳐 표시된 트랜잭션이 생성한 대기는 서버의 트랜잭션 처리 성능을 감소시킬 수 있습니다.  
  
 표시된 트랜잭션을 동시에 실행하지 않는 것이 좋습니다. 드문 일이지만 분산 표시된 트랜잭션의 커밋이 동시에 커밋되는 다른 분산 표시된 트랜잭션과 교착 상태에 빠질 수 있습니다. 이 경우 표시하는 트랜잭션이 교착 상태에서 희생되어 롤백됩니다. 이런 경우가 발생하면 애플리케이션이 표시된 트랜잭션을 다시 시도할 수 있습니다. 여러 개의 표시된 트랜잭션이 동시에 커밋을 시도하면 교착 상태에 빠질 가능성이 더 높아집니다.  
  
## <a name="recovering-to-a-marked-transaction"></a>표시된 트랜잭션으로 복구  
 표시된 트랜잭션을 포함하는 데이터베이스를 특정 표시 또는 해당 표시 바로 앞으로 복구하는 방법은 [표시된 트랜잭션이 포함된 관련 데이터베이스 복구](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [BEGIN DISTRIBUTED TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [전체 데이터베이스 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [표시된 트랜잭션이 포함된 관련 데이터베이스 복구](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
  
