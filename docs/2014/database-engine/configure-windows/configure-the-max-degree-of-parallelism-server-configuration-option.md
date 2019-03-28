---
title: max degree of parallelism 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parallel queries [SQL Server]
- processors [SQL Server], parallel queries
- number of processors for parallel queries
- max degree of parallelism option
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 46598cf66c80d07383fb033436bbe1792b1eec64
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537273"
---
# <a name="configure-the-max-degree-of-parallelism-server-configuration-option"></a>max degree of parallelism 서버 구성 옵션 구성
  이 항목에서는 구성 하는 방법에 설명 합니다 `max degree of parallelism` 서버 구성 옵션에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용 하 여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 마이크로프로세서나 CPU가 둘 이상인 컴퓨터에서 실행될 경우 최적 병렬 처리 수준, 즉 각 병렬 계획 실행에 대해 단일 문을 실행하는 데 사용된 프로세서 수를 검색합니다. `max degree of parallelism` 옵션을 사용하여 병렬 계획 실행에 사용되도록 프로세서 수를 제한할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 쿼리에 대한 병렬 실행 계획, 인덱스 DDL(데이터 정의 언어) 작업 및 정적 커서와 키 집합 커서 채우기를 고려합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **Max degree of parallelism 구성 옵션을 사용 하 여:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [Max degree of parallelism 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   affinity mask 옵션을 기본값으로 설정하지 않으면 SMP(대칭적 다중 처리) 시스템에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 사용 가능한 프로세서 수가 제한될 수도 있습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자만 변경해야 합니다.  
  
-   서버에서 최대 병렬 처리 수준을 결정할 수 있도록 하려면 이 옵션을 기본값인 0으로 설정합니다. 최대 병렬 처리 수준을 0으로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 최대 64개의 프로세서까지 모두 사용할 수 있습니다. 병렬 계획을 생성하지 않으려면 `max degree of parallelism`을 1로 설정합니다. 단일 쿼리 실행에서 사용할 수 있는 프로세서 코어의 최대 개수를 지정하려면 값을 1부터 32,767까지의 값 중 하나를 설정합니다. 사용 가능한 프로세서 수보다 더 큰 수를 지정하면 사용 가능한 실제 프로세서 수가 사용됩니다. 컴퓨터에 프로세서가 하나만 있는 경우 `max degree of parallelism` 값이 무시됩니다.  
  
-   쿼리 문에 MAXDOP 쿼리 힌트를 지정하면 쿼리의 max degree of parallelism 값을 재정의할 수 있습니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)를 참조하세요.  
  
-   인덱스를 만들거나 다시 작성하는 인덱스 작업 또는 클러스터형 인덱스를 삭제하는 인덱스 작업은 리소스가 많이 소모됩니다. 인덱스 문에 MAXDOP 인덱스 옵션을 지정하면 인덱스 작업의 max degree of parallelism 값을 재정의할 수 있습니다. MAXDOP 값은 실행 시 문에 적용되며 인덱스 메타데이터에 저장되지 않습니다. 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
-   쿼리 및 인덱스 작업과 함께 이 옵션은 DBCC CHECKTABLE, DBCC CHECKDB 및 DBCC CHECKFILEGROUP의 병렬 처리도 제어합니다. 추적 플래그 2528을 사용하여 이러한 문의 병렬 실행 계획을 비활성화할 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
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
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예제에서는 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 를 사용하여 `max degree of parallelism` 옵션을 `8`으로 구성하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 8;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 최대 병렬 처리 수준 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [선호도 마스크 서버 구성 옵션](affinity-mask-server-configuration-option.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DBCC CHECKTABLE&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checktable-transact-sql)   
 [DBCC CHECKDB&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [DBCC CHECKFILEGROUP&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql)   
 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [쿼리 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [인덱스 옵션 설정](../../relational-databases/indexes/set-index-options.md)  
  
  
