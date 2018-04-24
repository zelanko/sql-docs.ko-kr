---
title: 트랜잭션 복제에서 저장 프로시저 실행 게시 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], stored procedures and
- transactional replication, publishing stored procedure execution
ms.assetid: f4686f6f-c224-4f07-a7cb-92f4dd483158
caps.latest.revision: 40
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 177edf15879dd63642934ca2f0ab5db9e2ac532c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="publishing-stored-procedure-execution-in-transactional-replication"></a>트랜잭션 복제에서 저장 프로시저 실행 게시
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  게시자에서 실행되고 게시된 테이블에 영향을 주는 하나 이상의 저장 프로시저가 있는 경우 이러한 저장 프로시저를 저장 프로시저 실행 아티클로 게시에 포함해 보십시오. 프로시저 정의(CREATE PROCEDURE 문)는 구독이 초기화될 때 구독자로 복제되고 게시자에서 프로시저가 실행되면 복제가 구독자에서 해당하는 프로시저를 실행합니다. 이렇게 하면 프로시저 실행만 복제하고 행별 변경 내용은 복제하지 않으므로 대용량 일괄 처리 작업이 수행되는 경우 성능을 크게 향상시킬 수 있습니다. 예를 들어 게시 데이터베이스에서 다음 저장 프로시저를 생성한다고 가정합니다.  
  
```  
CREATE PROC give_raise AS  
UPDATE EMPLOYEES SET salary = salary * 1.10  
```  
  
 이 프로시저는 회사 내의 직원 10,000명의 급여를 10% 인상합니다. 게시자에서 이 저장 프로시저를 실행하면 각 직원의 급여가 업데이트됩니다. 저장 프로시저 실행을 복제하지 않으면 업데이트가 여러 단계의 대규모 트랜잭션으로 구독자로 전송됩니다.  
  
```  
BEGIN TRAN  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 1'  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 2'  
```  
  
 10,000개의 업데이트에 대해 이 프로세스가 반복됩니다.  
  
 저장 프로시저 실행을 복제하면 복제에서는 배포 데이터베이스에 모든 업데이트를 기록한 후 네트워크를 통해 구독자로 보내지 않고 구독자에서 저장 프로시저를 실행하는 명령만 보냅니다.  
  
```  
EXEC give_raise  
```  
  
> [!IMPORTANT]  
>  저장 프로시저 복제가 모든 응용 프로그램에 적절한 것은 아닙니다. 아티클이 수평 분할되어 구독자와는 다른 행 집합이 게시자에 있게 되면 게시자와 구독자 모두에서 같은 저장 프로시저를 실행해도 다른 결과가 나타납니다. 마찬가지로 업데이트가 복제되지 않은 다른 테이블의 하위 쿼리를 기반으로 하면 게시자와 구독자 모두에서 같은 저장 프로시저를 실행해도 다른 결과가 반환됩니다.  
  
 **저장 프로시저의 실행을 게시하려면**  
  
-   SQL Server Management Studio: [저장 프로시저 실행을 트랜잭션 게시로 게시&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
-   복제 Transact-SQL 프로그래밍: [sp_addarticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 실행하고 **@type** 매개 변수의 값을 'serializable proc exec'(권장) 또는 'proc exec'로 지정합니다. 아티클을 정의하는 방법은 [아티클 정의](../../../relational-databases/replication/publish/define-an-article.md)를 참조하세요.  
  
## <a name="modifying-the-procedure-at-the-subscriber"></a>구독자에서 프로시저 수정  
 기본적으로 게시자의 저장 프로시저 정의는 각 구독자로 전파됩니다. 그러나 구독자에서 저장 프로시저를 수정할 수도 있습니다. 이는 게시자와 구독자에서 다른 논리를 실행하려고 할 때 유용합니다. 예를 들어 구독자의 저장 프로시저 **sp_big_delete**에는 두 가지 기능이 있습니다. 복제된 테이블 **big_table1** 에서 1,000,000개의 행을 삭제하고 복제되지 않은 테이블 **big_table2**를 업데이트합니다. 네트워크 리소스에 대한 수요를 줄이려면 **sp_big_delete**를 게시하여 100만 개의 행 삭제를 저장 프로시저로 전파해야 합니다. 구독자에서 100만 개의 행만 삭제하고 **big_table2** 에 대한 후속 업데이트를 수행하지 않도록 **sp_big_delete**를 정의할 수 있습니다.  
  
> [!NOTE]  
>  기본적으로 게시자에서 ALTER PROCEDURE를 사용하여 적용한 변경 내용은 구독자로 전파됩니다. 이를 방지하려면 ALTER PROCEDURE를 실행하기 전에 스키마 변경 내용을 전파하는 설정을 해제합니다. 스키마 변경에 대한 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
## <a name="types-of-stored-procedure-execution-articles"></a>저장 프로시저 실행 아티클의 유형  
 직렬화 가능 프로시저 실행 아티클과 프로시저 실행 아티클을 사용하여 저장 프로시저의 실행을 게시할 수 있습니다.  
  
-   프로시저가 직렬화 가능 트랜잭션의 컨텍스트 내에서 실행되는 경우에만 프로시저 실행을 복제하는 직렬화 가능 옵션을 사용하는 것이 좋습니다. 저장 프로시저가 직렬화 가능 트랜잭션 외부에서 실행되면 게시된 테이블의 데이터 변경 내용이 일련의 DML 문으로 복제됩니다. 이 동작을 통해 구독자의 데이터와 게시자의 데이터의 일관성을 기할 수 있습니다. 이는 대규모 정리 작업과 같은 일괄 처리 작업에 특히 유용합니다.  
  
-   프로시저 실행 옵션을 사용하면 저장 프로시저에 있는 개별 문의 성공 여부에 상관없이 실행을 모든 구독자에 복제할 수 있습니다. 또한 여러 트랜잭션 내에서 저장 프로시저에 의해 데이터가 변경될 수 있으므로 구독자 데이터와 게시자 데이터가 일치하지 않을 수 있습니다. 이러한 문제를 해결하려면 구독자가 읽기 전용이어야 하고 커밋되지 않은 읽기보다 높은 격리 수준을 사용해야 합니다. 커밋되지 않은 읽기를 사용하면 게시된 테이블의 데이터에 대한 변경 내용이 일련의 DML 문으로 복제됩니다.  
  
 다음 예에서는 프로시저 복제를 직렬화 가능 프로시저 아티클로 설정하는 것을 권장하는 이유를 설명합니다.  
  
```  
BEGIN TRANSACTION T1  
SELECT @var = max(col1) FROM tableA  
UPDATE tableA SET col2 = <value>   
   WHERE col1 = @var   
  
BEGIN TRANSACTION T2  
INSERT tableA VALUES <values>  
COMMIT TRANSACTION T2  
```  
  
 위의 예제에서 트랜잭션 T1의 SELECT는 트랜잭션 T2의 INSERT 이전에 발생한다고 가정합니다.  
  
 프로시저가 직렬화 가능 트랜잭션(격리 수준이 SERIALIZABLE로 설정됨) 내에서 프로시저가 실행되지 않으면 트랜잭션 T2는 T1의 SELECT 문 범위 내에서 새 행을 삽입할 수 있고 T1 이전에 커밋됩니다. 이는 T2가 T1 이전에 구독자에서 적용되는 것을 의미합니다. T1이 구독자에서 적용되면, SELECT는 게시자에서와 다른 값을 반환할 수 있고 UPDATE와 다른 결과를 가져올 수 있습니다.  
  
 프로시저가 직렬화 가능 트랜잭션 내에서 실행되면, 트랜잭션 T2는 T2의 SELECT 문 범위 내에서 삽입을 할 수 없습니다. 구독자에서 같은 결과를 가져오도록 T1이 커밋될 때까지 T2는 차단됩니다.  
  
 직렬화 가능 트랜잭션 내에서 프로시저를 실행하면 잠금이 더 오래 유지되어 동시성이 줄어들 수 있습니다.  
  
## <a name="the-xactabort-setting"></a>XACT_ABORT 설정  
 저장 프로시저 실행을 복제할 때 저장 프로시저를 실행하는 세션에 대해 XACT_ABORT 설정을 ON으로 지정해야 합니다. XACT_ABORT가 OFF로 설정되면 게시자에서 프로시저 실행 중 오류가 발생하면 구독자에서도 같은 오류가 발생하여 배포 에이전트가 실패합니다. XACT_ABORT를 ON으로 지정하면 게시자에서 실행 중 발생한 모든 오류로 인해 전체 실행이 롤백되므로 배포 에이전트 실패를 막을 수 있습니다. XACT_ABORT 설정에 대한 자세한 내용은 [SET XACT_ABORT&#40;Transact-SQL&#41;](../../../t-sql/statements/set-xact-abort-transact-sql.md)를 참조하세요.  
  
 XACT_ABORT를 OFF로 설정해야 하는 경우에는 배포 에이전트에 대해 **-SkipErrors** 매개 변수를 지정합니다. 그러면 오류가 발생해도 에이전트가 구독자에서 변경 내용을 계속 적용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
