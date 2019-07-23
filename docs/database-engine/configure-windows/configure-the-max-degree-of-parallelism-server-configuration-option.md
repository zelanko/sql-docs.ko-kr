---
title: max degree of parallelism 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parallel queries [SQL Server]
- processors [SQL Server], parallel queries
- number of processors for parallel queries
- max degree of parallelism option
- MaxDop
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 83e56acbf6a45afda0b7ab19f83894bbca41ff33
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012595"
---
# <a name="configure-the-max-degree-of-parallelism-server-configuration-option"></a>max degree of parallelism 서버 구성 옵션 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] MAXDOP(max degree of parallelism) [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 마이크로프로세서나 CPU가 둘 이상인 컴퓨터에서 실행될 경우 최적 병렬 처리 수준, 즉 각 병렬 계획 실행에 대해 단일 문을 실행하는 데 사용된 프로세서 수를 검색합니다. **max degree of parallelism** 옵션을 사용하여 병렬 계획 실행에 사용할 프로세서 수를 제한할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 쿼리에 대한 병렬 실행 계획, 인덱스 DDL(데이터 정의 언어) 작업, 병렬 삽입, 온라인 열 변경, 병렬 통계 수집 및 정적 커서와 키 집합 커서 채우기를 고려합니다.

##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   affinity mask 옵션을 기본값으로 설정하지 않으면 SMP(대칭적 다중 처리) 시스템에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 사용 가능한 프로세서 수가 제한될 수도 있습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전문가만이 변경해야 합니다.  
  
-   서버에서 최대 병렬 처리 수준을 결정할 수 있도록 하려면 이 옵션을 기본값인 0으로 설정합니다. 최대 병렬 처리 수준을 0으로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 최대 64개의 프로세서까지 모두 사용할 수 있습니다. 병렬 계획이 생성되지 않게 하려면 **max degree of parallelism** 을 1로 설정합니다. 단일 쿼리 실행에서 사용할 수 있는 프로세서 코어의 최대 개수를 지정하려면 값을 1부터 32,767까지의 값 중 하나를 설정합니다. 사용 가능한 프로세서 수보다 더 큰 수를 지정하면 사용 가능한 실제 프로세서 수가 사용됩니다. 컴퓨터에 프로세서가 하나밖에 없으면 **max degree of parallelism** 값이 무시됩니다.  
  
-   쿼리 문에 MAXDOP 쿼리 힌트를 지정하면 쿼리의 max degree of parallelism 값을 재정의할 수 있습니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
-   인덱스를 만들거나 다시 작성하는 인덱스 작업 또는 클러스터형 인덱스를 삭제하는 인덱스 작업은 리소스가 많이 소모됩니다. 인덱스 문에 MAXDOP 인덱스 옵션을 지정하면 인덱스 작업의 max degree of parallelism 값을 재정의할 수 있습니다. MAXDOP 값은 실행 시 문에 적용되며 인덱스 메타데이터에 저장되지 않습니다. 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
-   쿼리 및 인덱스 작업과 함께 이 옵션은 DBCC CHECKTABLE, DBCC CHECKDB 및 DBCC CHECKFILEGROUP의 병렬 처리도 제어합니다. 추적 플래그 2528을 사용하여 이러한 문의 병렬 실행 계획을 비활성화할 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.

###  <a name="Guidelines"></a> 지침  
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 서비스 시작 중에 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]가 NUMA 노드 또는 소켓당 8개 초과의 실제 코어를 감지하면 soft-NUMA 노드가 기본적으로 자동 생성됩니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 논리 프로세서를 동일한 실제 코어에서 서로 다른 soft-NUMA 노드에 배치합니다. 아래 표의 권장 사항은 동일한 소프트 NUMA 노드 내에서 병렬 쿼리의 모든 작업자 스레드를 유지하는 것을 목표로 합니다. 이렇게 하면 쿼리의 성능이 향상되고 워크로드에 대한 NUMA 노드에서 작업자 스레드 배포가 향상됩니다. 자세한 내용은 [Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md)를 참조하세요.

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 **최대 병렬 처리 수준** 서버 구성 값을 구성할 때 다음 지침을 사용하세요.

||||
|----------------|-----------------|-----------------|
|단일 NUMA 노드가 있는 서버|8개 이하의 논리 프로세서|MAXDOP을 #개 이하 논리 프로세서로 유지|
|단일 NUMA 노드가 있는 서버|논리 프로세서 8개 초과|MAXDOP을 8개로 유지|
|여러 NUMA 노드가 있는 서버|NUMA 노드당 16개 이하의 논리 프로세서|MAXDOP을 NUMA 노드당 #개 이하 논리 프로세서로 유지|
|여러 NUMA 노드가 있는 서버|NUMA 노드당 논리 프로세서 16개 초과|MAXDOP를 MAX 값이 16인 NUMA 노드당 논리 프로세스 수의 절반으로 유지|
  
> [!NOTE]
> 위 표의 NUMA 노드는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 버전에서 자동으로 생성되는 소프트 NUMA 노드 또는 소프트 NUMA가 사용되지 않는 경우 하드웨어 기반 NUMA 노드를 가리킵니다.   
>  Resource Governor 작업 그룹에 대해 최대 병렬 처리 수준 옵션을 설정할 때도 동일한 지침을 사용합니다. 자세한 내용은 [작업 그룹 만들기(Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)를 참조하세요.
  
**최대 병렬 처리 수준** 서버 구성 값을 구성할 때 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]~[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 다음 지침을 사용합니다.

||||
|----------------|-----------------|-----------------|
|단일 NUMA 노드가 있는 서버|8개 이하의 논리 프로세서|MAXDOP을 #개 이하 논리 프로세서로 유지|
|단일 NUMA 노드가 있는 서버|논리 프로세서 8개 초과|MAXDOP을 8개로 유지|
|여러 NUMA 노드가 있는 서버|NUMA 노드당 8개 이하의 논리 프로세서|MAXDOP을 NUMA 노드당 #개 이하 논리 프로세서로 유지|
|여러 NUMA 노드가 있는 서버|NUMA 노드당 논리 프로세서 8개 초과|MAXDOP을 8개로 유지|
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>최대 병렬 처리 수준 옵션을 구성하려면  
  
1.  **개체 탐색기**에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **고급** 노드를 클릭합니다.  
  
3.  **최대 병렬 처리 수준** 상자에서 병렬 계획 실행에 사용할 프로세서의 최대 개수를 선택합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>최대 병렬 처리 수준 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예제에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 사용하여 `max degree of parallelism` 옵션을 `8`으로 구성하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 16;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 최대 병렬 처리 수준 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [선호도 마스크 서버 구성 옵션](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sp_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [DBCC CHECKTABLE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKFILEGROUP&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)   
 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md) [인덱스 옵션 설정](../../relational-databases/indexes/set-index-options.md)  
 [SQL Server의 "max degree of parallelism" 구성 옵션에 대한 권장 사항 및 지침(영문)](https://support.microsoft.com/help/2806535)
  
  
