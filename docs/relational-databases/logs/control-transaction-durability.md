---
title: "트랜잭션 내구성 제어 | Microsoft 문서"
ms.custom: 
ms.date: 09/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- delayed durability
- Lazy Commit
ms.assetid: 3ac93b28-cac7-483e-a8ab-ac44e1cc1c76
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 956e9f95b95aa0ecb99477714e70ac61d29c45e0
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="control-transaction-durability"></a>트랜잭션 내구성 제어
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션 커밋은 완전 내구성( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본값)이 있거나 지연된 내구성(느린 커밋이라고도 함)이 있습니다.    
    
 완전 내구성이 있는 트랜잭션 커밋은 동기적이므로 트랜잭션에 대한 로그 레코드가 디스크에 기록된 후에만 커밋을 성공으로 보고하고 클라이언트에 컨트롤을 반환합니다. 지연된 내구성이 있는 트랜잭션 커밋은 비동기적이므로 트랜잭션에 대한 로그 레코드가 디스크에 기록되기 전에 커밋을 성공으로 보고합니다. 트랜잭션이 내구성을 가지려면 디스크에 트랜잭션 로그 항목을 기록해야 합니다. 지연된 내구성이 있는 트랜잭션은 트랜잭션 로그 항목을 디스크에 플러시한 경우에 내구성을 가집니다.    
    
 이 항목에서는 지연된 내구성이 있는 트랜잭션에 대해 자세히 설명합니다.    
    
## <a name="full-vs-delayed-transaction-durability"></a>완전 트랜잭션 내구성과 지연된 트랜잭션 내구성 비교    
 완전 트랜잭션 내구성과 지연된 트랜잭션 내구성은 모두 장단점이 있습니다. 응용 프로그램은 완전 내구성이 있는 트랜잭션과 지연된 내구성이 있는 트랜잭션을 혼합할 수 있습니다. 따라서 비즈니스 요구 사항과 각 트랜잭션이 이러한 요구 사항에 얼마나 적합한지를 신중하게 고려해야 합니다.    
    
### <a name="full-transaction-durability"></a>완전 트랜잭션 내구성    
 완전 내구성이 있는 트랜잭션은 클라이언트에 컨트롤을 반환하기 전에 디스크에 트랜잭션 로그를 기록합니다. 다음과 같은 경우 완전 내구성이 있는 트랜잭션을 사용해야 합니다.    
    
-   시스템에서 데이터 손실을 허용할 수 없는 경우     
    데이터 일부를 손실할 수 있는 경우에 대한 자세한 내용은 [데이터를 손실할 수는 경우](../../relational-databases/logs/control-transaction-durability.md#bkmk_DataLoss) 섹션을 참조하세요.    
    
-   병목 현상의 원인이 트랜잭션 로그 쓰기 대기 시간이 아닌 경우    
    
 지연된 트랜잭션 내구성은 트랜잭션 로그 레코드를 메모리에 유지하고 트랜잭션 로그에 일괄적으로 쓰기 때문에 I/O 작업이 더 적게 수행되므로 I/O 기록으로 인한 대기 시간이 줄어듭니다. 지연된 트랜잭션 내구성은 로그 I/O 경합을 줄여서 시스템의 대기 시간을 단축할 수 있습니다.    
    
 **완전 트랜잭션 내구성 보장**    
    
-   트랜잭션 커밋에 성공하면 트랜잭션에 의한 변경 사항이 시스템의 다른 트랜잭션에 표시됩니다. 트랜잭션 격리 수준에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md) 또는 [Transactions with Memory-Optimized Tables](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)(메모리 액세스에 최적화된 테이블 트랜잭션)을 참조하세요.    
    
-   내구성이 커밋에서 보장됩니다. 트랜잭션 커밋이 성공하여 클라이언트에 컨트롤을 반환하기 이전에는 해당 로그 레코드가 디스크에 지속됩니다.    
    
### <a name="delayed-transaction-durability"></a>지연된 트랜잭션 내구성    
 지연된 트랜잭션 내구성은 디스크에 대한 비동기 로그 쓰기를 사용하여 수행됩니다. 트랜잭션 로그 레코드는 버퍼에 유지되며 버퍼가 꽉 차거나 버퍼 플러시 이벤트가 발생하면 디스크에 기록됩니다. 지연된 트랜잭션 내구성은 다음과 같은 이유로 시스템에서 대기 시간과 경합을 모두 줄입니다.    
    
-   로그 IO를 완료하고 클라이언트에 컨트롤을 반환할 때까지 트랜잭션 커밋 처리가 지연되지 않습니다.    
    
-   동시 트랜잭션이 로그 IO를 경합할 가능성이 낮습니다. 대신 더 큰 청크로 구성된 디스크에 로그 버퍼를 플러시하여 경합을 줄이고 처리 속도를 높일 수 있습니다.    
    
    > [!NOTE]    
    >  동시성이 높은 경우 특히, 로그 버퍼를 플러시 속도보다 더 빠르게 채울 경우 로그 I/O 경합이 여전히 발생할 수 있습니다.    
    
 #### <a name="when-to-use-delayed-transaction-durability"></a>지연된 트랜잭션 내구성을 사용할 경우    
    
 지연된 트랜잭션 내구성을 사용하는 것이 유리한 경우는 다음과 같습니다.    
    
 **약간의 데이터 손실을 허용할 수 있는 경우**    
 약간의 데이터 손실을 허용할 수 있는 경우(예: 대부분의 데이터를 보유하여 개별 데이터가 중요하지는 않은 경우)에는 지연된 내구성을 고려하는 것이 좋습니다. 데이터 손실을 허용할 수 없는 경우에는 지연된 트랜잭션 내구성을 사용하지 마세요.    
    
 **트랜잭션 로그 쓰기 중에 병목 현상이 발생하는 경우**    
 트랜잭션 로그 쓰기의 지연으로 인해 성능 문제가 발생하는 경우 응용 프로그램에서 지연된 트랜잭션 내구성을 사용하는 것이 좋습니다.    
    
 **작업의 경합률이 높은 경우**    
 작업의 경합 수준이 높은 경우 잠금이 해제되는 동안 대기하는 데 많은 시간이 소요됩니다. 지연된 트랜잭션 내구성은 커밋 시간을 단축하여 잠금을 더 빠르게 해제하여 처리 속도를 높입니다.    
    
 ### <a name="delayed-transaction-durability-guarantees"></a>지연된 트랜잭션 내구성 보장   
    
-   트랜잭션 커밋에 성공하면 트랜잭션에 의한 변경 사항이 시스템의 다른 트랜잭션에 표시됩니다.    
    
-   트랜잭션 내구성은 디스크에 메모리 내 트랜잭션 로그를 플러시한 경우에만 보장됩니다. 메모리 내 트랜잭션 로그가 디스크에 플러시되는 경우는 다음과 같습니다.    
    
    -   동일한 데이터베이스의 완전 내구성이 있는 트랜잭션이 데이터베이스에서 변경되고 성공적으로 커밋된 경우   
    
    -   사용자가 시스템 저장 프로시저 `sp_flush_log` 를 성공적으로 실행한 경우     
    
        완전 내구성이 있는 트랜잭션 또는 sp_flush_log가 성공적으로 커밋되면, 이전에 커밋된 지연된 내구성 트랜잭션은 모두 내구성을 가집니다.
        
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 모든 트랜잭션이 지연되더라도 로그 생성 및 시간을 모두 기반으로 로그를 디스크에 플러시합니다. 일반적으로 IO 장치가 계속 실행되면 정상으로 처리된 것입니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 내구성 있는 트랜잭션 및 sp_flush_log 외의 어떠한 내구성도 보장하지 않습니다.      
    
  
    
## <a name="how-to-control-transaction-durability"></a>트랜잭션 내구성을 제어하는 방법    
    
###  <a name="bkmk_DbControl"></a> Database level control    
 DBA는 다음 문을 사용하여 사용자가 데이터베이스에서 지연된 트랜잭션 내구성을 사용할 수 있는지 여부를 제어할 수 있습니다. ALTER DATABASE를 사용하여 지연된 내구성 설정을 지정해야 합니다.    
    
```tsql    
ALTER DATABASE … SET DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }    
```    
    
 **사용 안 함**    
 [기본값] 이 설정을 사용하면 커밋 수준 설정(DELAYED_DURABILITY=[ON | OFF])에 상관없이 데이터베이스에 커밋된 모든 트랜잭션이 완전 내구성을 가집니다. 저장 프로시저를 변경하고 다시 컴파일할 필요가 없습니다. 따라서 지연된 내구성으로 인해 데이터가 위험에 노출되지 않습니다.    
    
 **허용함**    
 이 설정을 사용하면 각 트랜잭션의 내구성이 트랜잭션 수준에서 결정됩니다. 즉, DELAYED_DURABILITY = { *OFF* | ON }에 의해 결정됩니다. 자세한 내용은 [Atomic 블록 수준 제어 – 고유하게 컴파일된 저장 프로시저](../../relational-databases/logs/control-transaction-durability.md#CompiledProcControl) 및 [COMMIT 수준 제어 – Transact-SQL](../../relational-databases/logs/control-transaction-durability.md#bkmk_T-SQLControl) 을 참조하세요.    
    
 **FORCED**    
 이 설정을 사용하면 데이터베이스에 커밋되는 모든 트랜잭션이 지연된 내구성을 가집니다. 트랜잭션이 완전 내구성(DELAYED_DURABILITY = OFF)을 지정하는지 여부에 상관없이 트랜잭션은 지연된 내구성이 있습니다. 이 설정은 지연된 트랜잭션 내구성이 데이터베이스에 유용하고 응용 프로그램 코드를 변경하지 않으려는 경우에 유용합니다.    
    
###  <a name="CompiledProcControl"></a> Atomic block level control – Natively Compiled Stored Procedures    
 다음 코드는 ATOMIC 블록 내로 이동합니다.    
    
```tsql    
DELAYED_DURABILITY = { OFF | ON }    
```    
    
 **OFF**    
 [기본값] DELAYED_DURABLITY = FORCED 데이터베이스 옵션을 적용하여 커밋이 비동기적이고 지연된 내구성을 갖는 경우를 제외하고 트랜잭션은 완전 내구성을 가집니다. 자세한 내용은 [Database level control](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) 을 참조하세요.    
    
 **ON**    
 DELAYED_DURABLITY = DISABLED 데이터베이스 옵션을 적용하여 커밋이 동기적이고 완전 내구성이 있는 경우를 제외하고 트랜잭션은 지연된 내구성을 가집니다.  자세한 내용은 [Database level control](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) 을 참조하세요.    
    
 **코드 예:**    
    
```tsql    
CREATE PROCEDURE <procedureName> …    
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER    
AS BEGIN ATOMIC WITH     
(    
    DELAYED_DURABILITY = ON,    
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,    
    LANGUAGE = N'English'    
    …    
)    
END    
```    
    
### <a name="table-1-durability-in-atomic-blocks"></a>테이블 1; ATOMIC 블록의 내구성    
    
|ATOMIC 블록 내구성 옵션|기존 트랜잭션 없음|처리 중인 트랜잭션(완전 또는 지연된 내구성이 있음)|    
|------------------------------------|-----------------------------|---------------------------------------------------------|    
|**DELAYED_DURABILITY = OFF**|ATOMIC 블록은 새로운 완전 내구성이 있는 트랜잭션을 시작합니다.|ATOMIC 블록은 기존 트랜잭션에 저장점을 만든 다음 새 트랜잭션을 시작합니다.|    
|**DELAYED_DURABILITY = ON**|ATOMIC 블록은 새로운 지연된 내구성이 있는 트랜잭션을 시작합니다.|ATOMIC 블록은 기존 트랜잭션에 저장점을 만든 다음 새 트랜잭션을 시작합니다.|    
    
###  <a name="bkmk_T-SQLControl"></a> COMMIT level control –[!INCLUDE[tsql](../../includes/tsql-md.md)]    
 지연된 트랜잭션 내구성을 강제로 적용할 수 있도록 COMMIT 구문이 확장됩니다. 데이터베이스 수준에서 If DELAYED_DURABILITY가 DISABLED 또는 FORCED인 경우(위 내용 참조) 이 COMMIT 옵션은 무시됩니다.    
    
```tsql    
COMMIT [ { TRAN | TRANSACTION } ] [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]    
    
```    
    
 **OFF**    
 [기본값] DELAYED_DURABLITY = FORCED 데이터베이스 옵션을 적용하여 COMMIT이 비동기적이고 지연된 내구성을 갖는 경우를 제외하고 COMMIT 트랜잭션은 완전 내구성을 가집니다. 자세한 내용은 [Database level control](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) 을 참조하세요.    
    
 **ON**    
 DELAYED_DURABLITY = DISABLED 데이터베이스 옵션을 적용하여 COMMIT이 동기적이고 완전 내구성이 있는 경우를 제외하고 COMMIT 트랜잭션은 지연된 내구성을 가집니다. 자세한 내용은 [Database level control](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) 을 참조하세요.    
    
### <a name="summary-of-options-and-their-interactions"></a>옵션 및 상호 작용 요약    
 이 표에서는 데이터베이스 수준 지연된 내구성 설정과 커밋 수준 설정 사이의 상호 작용을 요약합니다. 데이터베이스 수준 설정이 커밋 수준 설정보다 항상 우선합니다.    
    
|COMMIT 설정/데이터베이스 설정|DELAYED_DURABILITY = DISABLED|DELAYED_DURABILITY = ALLOWED|DELAYED_DURABILITY = FORCED|    
|--------------------------------------|-------------------------------------|------------------------------------|-----------------------------------|    
|**DELAYED_DURABILITY = OFF** 데이터베이스 수준 트랜잭션|트랜잭션이 완전 내구성을 가집니다.|트랜잭션이 완전 내구성을 가집니다.|트랜잭션이 지연된 내구성을 가집니다.|    
|**DELAYED_DURABILITY = ON** 데이터베이스 수준 트랜잭션|트랜잭션이 완전 내구성을 가집니다.|트랜잭션이 지연된 내구성을 가집니다.|트랜잭션이 지연된 내구성을 가집니다.|    
|**DELAYED_DURABILITY = OFF** 데이터베이스 간 트랜잭션 또는 분산 트랜잭션|트랜잭션이 완전 내구성을 가집니다.|트랜잭션이 완전 내구성을 가집니다.|트랜잭션이 완전 내구성을 가집니다.|    
|**DELAYED_DURABILITY = ON** 데이터베이스 간 트랜잭션 또는 분산 트랜잭션|트랜잭션이 완전 내구성을 가집니다.|트랜잭션이 완전 내구성을 가집니다.|트랜잭션이 완전 내구성을 가집니다.|    
    
## <a name="how-to-force-a-transaction-log-flush"></a>트랜잭션 로그를 강제로 플러시하는 방법    
 디스크에 트랜잭션 로그를 강제로 플러시하는 두 가지 방법이 있습니다.    
    
-   동일한 데이터베이스를 변경하는 완전 내구성이 있는 트랜잭션을 실행합니다. 이렇게 하면 모든 이전에 커밋된 지연된 내구성 트랜잭션의 로그 레코드가 디스크에 강제로 플러시됩니다.    
    
-   시스템 저장 프로시저 실행 `sp_flush_log`를 실행합니다. 이 프로시저는 모든 이전에 커밋된 지연된 내구성이 있는 트랜잭션의 로그 레코드를 디스크에 강제로 플러시합니다. 자세한 내용은 [sys.sp_flush_log&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-flush-log-transact-sql.md)를 참조하세요.    
    
##  <a name="bkmk_OtherSQLFeatures"></a> 지연된 내구성 및 기타 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능    
 **변경 추적 및 변경 데이터 캡처**    
 변경 추적을 적용한 모든 트랜잭션은 완전 내구성을 가집니다. 변경 추적을 사용하도록 설정한 테이블에 쓰기 작업을 수행하는 경우 트랜잭션은 변경 추적 속성이 있습니다. 지연된 내구성 사용은 CDC(변경 데이터 캡처)를 사용하는 데이터베이스에 지원되지 않습니다.    
    
 **충돌 복구**    
 일관성이 보장되지만 커밋된 지연된 내구성이 있는 트랜잭션에서 변경된 일부 항목이 손실될 수 있습니다.    
    
 **데이터베이스 간 및 DTC**    
 데이터베이스 또는 트랜잭션 커밋 설정에 상관없이 데이터베이스 간 트랜잭션 또는 분산 트랜잭션인 경우 트랜잭션은 완전 내구성을 가집니다.    
    
 **AlwaysOn 가용성 그룹 및 미러링**    
 지연된 내구성이 있는 트랜잭션은 기본 또는 보조 데이터베이스에서 내구성을 보장하지 않습니다. 또한 보조 데이터베이스에서 트랜잭션에 대한 정보를 보장하지 않습니다. 제어는 커밋 후 동기 보조 데이터베이스에서 승인이 수신되기 이전에 클라이언트에 반환됩니다. 기본 복제본의 디스크로 플러시될 때 보조 복제본으로 계속 복제됩니다.   
    
 **장애 조치(Failover) 클러스터링**    
 일부 지연된 내구성이 있는 트랜잭션 쓰기가 손실될 수 있습니다.    
    
 **트랜잭션 복제**    
 지연된 내구성이 있는 트랜잭션은 트랜잭션 복제에서 지원되지 않습니다.    
    
 **로그 전달**    
 내구성이 있는 트랜잭션만 발송되는 로그에 포함됩니다.    
    
 **로그 백업**    
 내구성이 있는 트랜잭션만 백업에 포함됩니다.    
    
##  <a name="bkmk_DataLoss"></a> When can I lose data?    
 테이블에 대해 지연된 내구성을 구현하는 경우 특정 상황에서 데이터를 손실할 수 있습니다. 데이터 손실을 허용할 수 없는 경우에는 지연된 트랜잭션 내구성을 사용하지 마세요.    
    
### <a name="catastrophic-events"></a>재해    
 서버 크래시와 같은 재해 발생 시 디스크에 저장되지 않은 커밋된 모든 트랜잭션의 데이터를 손실하게 됩니다. 데이터베이스의 테이블에 대해 완전 내구성이 있는 트랜잭션이 실행되거나 `sp_flush_log` 가 호출될 때마다 지연된 내구성 트랜잭션이 디스크에 저장됩니다. 지연된 내구성 트랜잭션을 사용하는 경우 데이터베이스에 정기적으로 `sp_flush_log` 를 업데이트하거나 호출할 수 있는 작은 테이블을 만들어 처리되지 않은 커밋된 모든 트랜잭션을 저장할 수 있습니다. 또한 가득 찰 때마다 트랜잭션 로그가 플러시되지만 이는 예측하기 어려워 제어하는 것이 불가능합니다.    
    
### <a name="includessnoversionincludesssnoversion-mdmd-shutdown-and-restart"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 종료 및 다시 시작    
 지연된 내구성의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 예기치 않은 종료와 예상된 종료/다시 시작 간에는 차이가 없습니다. 재해와 같은 데이터 손실을 대비하여 계획을 세워야 합니다. 예정된 종료/다시 시작에서 디스크에 기록되지 않은 일부 트랜잭션이 먼저 디스크에 저장될 수 있지만 이에 대한 계획을 세우지 않아야 합니다. 예정되었든 예정되지 않았든 종료/다시 시작 시 재해와 동일하게 데이터를 손실할 것처럼 계획을 세우세요.    
    
## <a name="see-also"></a>참고 항목    
 [메모리 액세스에 최적화된 테이블의 트랜잭션](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)    
    
  

