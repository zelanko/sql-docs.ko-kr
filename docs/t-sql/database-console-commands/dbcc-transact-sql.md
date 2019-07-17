---
title: DBCC(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC
- DBCC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactional consistency
- Database Console Command statements
- status information [SQL Server], DBCC statements
- snapshots [SQL Server database snapshots], DBCC statements
- emergency database state [SQL Server]
- TABLOCK
- internal database snapshots [SQL Server]
- reporting DBCC statement progress
- logical consistency of data [SQL Server]
- DBCC statements
- validation statements [SQL Server]
- miscellaneous statements [SQL Server]
- statements [SQL Server], DBCC statements
- DBCC commands [SQL Server]
- result sets [SQL Server], DBCC statements
- maintenance statements [SQL Server]
- physical consistency of data [SQL Server]
- current DBCC statement status
- progress reporting [DBCC statements]
- informational statements [SQL Server]
ms.assetid: c6da8c04-5b6b-459a-9f76-110c92ca8b29
author: pmasl
ms.author: umajay
manager: craigg
ms.openlocfilehash: e746569eb629eb41c96cc7738e9529949307532e
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685720"
---
# <a name="dbcc-transact-sql"></a>DBCC(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그래밍 언어는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대해 데이터베이스 콘솔 명령으로 작동하는 DBCC 문을 제공합니다.
  
데이터베이스 콘솔 명령 문은 다음과 같은 범주로 분류할 수 있습니다.
  
|명령 범주|수행하는 작업|  
|---|---|
|유지 관리|데이터베이스, 인덱스 또는 파일 그룹에 대한 유지 관리 태스크|  
|기타|추적 플래그 설정이나 메모리에서 DLL 제거 같은 기타 태스크입니다.|  
|알림|다양한 정보를 수집하고 표시하는 태스크입니다.|  
|유효성 검사|데이터베이스, 테이블, 인덱스, 카탈로그, 파일 그룹 또는 데이터베이스 페이지 할당에 대한 유효성 검사 작업입니다.|  
  
DBCC 명령은 입력 매개 변수와 반환 값을 사용합니다. 모든 DBCC 명령 매개 변수는 유니코드와 DBCS 리터럴을 모두 사용할 수 있습니다.
  
## <a name="dbcc-internal-database-snapshot-usage"></a>DBCC 내부 데이터베이스 스냅샷 사용법  
다음 DBCC 명령은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 만든 내부 읽기 전용 데이터베이스 스냅샷에서 작동합니다. 이렇게 하면 이러한 명령이 실행될 때 차단 및 동시성 문제를 방지할 수 있습니다. 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요.
- DBCC CHECKALLOC
- DBCC CHECKCATALOG
- DBCC CHECKDB
- DBCC CHECKFILEGROUP
- DBCC CHECKTABLE

이러한 DBCC 명령 중 하나를 실행할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 데이터베이스 스냅샷을 만들어 트랜잭션이 일관성 있는 상태가 되도록 합니다. 그런 다음 DBCC 명령은 이 스냅샷에 대한 검사를 실행합니다. DBCC 명령이 완료되면 이 스냅샷은 삭제됩니다.
  
내부 데이터베이스 스냅샷이 필요하지 않거나 생성되지 않는 경우도 있습니다. 이럴 경우 DBCC 명령은 실제 데이터베이스에 실행됩니다. 데이터베이스가 온라인 상태인 경우 DBCC 명령은 테이블 잠금을 사용하여 검사 중인 개체의 일관성을 유지하도록 합니다. 이 동작은 WITH TABLOCK 옵션이 지정된 경우와 동일합니다.
  
다음과 같은 경우에 DBCC 명령이 실행되면 내부 데이터베이스 스냅샷이 생성되지 않습니다.
-   **master**에 대해 실행되고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 단일 사용자 모드로 실행 중인 경우  
-   **master** 이외의 데이터베이스에 대해 실행되지만, 해당 데이터베이스가 ALTER DATABASE 문을 사용하여 단일 사용자 모드로 배치된 경우  
-   읽기 전용 데이터베이스에 대해 실행된 경우  
-   ALTER DATABASE 문을 사용하여 응급 모드로 설정된 데이터베이스에 대해 실행된 경우  
-   **tempdb**에 대해 실행된 경우. 이 경우 내부 제한 사항으로 인해 데이터베이스 스냅샷을 만들 수 없습니다.  
-   WITH TABLOCK 옵션을 사용하는 경우. 이 경우 DBCC는 데이터베이스 스냅샷을 만들지 않도록 요청하는 것으로 인식합니다.  
  
DBCC 명령이 다음에 대해 실행될 때 이 명령은 내부 데이터베이스 스냅샷 대신 테이블 잠금을 사용합니다.
-   읽기 전용 파일 그룹  
-   FAT 파일 시스템  
-   '명명된 스트림'을 지원하지 않는 볼륨  
-   '대체 스트림'을 지원하지 않는 볼륨  
  
> [!NOTE]  
>  WITH TABLOCK 옵션을 사용하여 DBCC CHECKALLOC 또는 DBCC CHECKDB의 동등한 부분을 실행하려면 데이터베이스 X 잠금이 필요합니다. 이 데이터베이스 잠금은 **tempdb** 또는 **master**에 설정할 수 없으며, 다른 모든 데이터베이스에서도 실패할 수 있습니다.  
  
> [!NOTE]  
>  내부 데이터베이스 스냅샷을 만들 수 없는 경우 DBCC CHECKDB가 **master**에 대해 실행되면 실패합니다.  
  
## <a name="progress-reporting-for-dbcc-commands"></a>DBCC 명령에 대한 진행률 보고  
**sys.dm_exec_requests** 카탈로그 뷰에는 DBCC CHECKDB, CHECKFILEGROUP 및 CHECKTABLE 명령의 현재 실행 단계와 진행률에 대한 정보가 포함되어 있습니다. **percent_complete** 열은 명령의 완료 비율을 표시하고, **command** 열은 해당 명령의 현재 실행 단계를 보고합니다.
  
진행률 단위에 대한 정의는 DBCC 명령의 현재 실행 단계에 따라 다릅니다. 때때로 진행률은 데이터베이스 페이지의 세분성에 따라 보고되며 다른 단계에서는 할당 복구 또는 단일 데이터베이스의 세분성에 따라 보고됩니다. 다음 표에서는 각 실행 단계 및 명령이 진행률을 보고하는 세분성에 대해 설명합니다.
  
|실행 단계|설명|진행률 보고 세분성|  
|---------------------|-----------------|------------------------------------|  
|DBCC TABLE CHECK|이 단계 동안 데이터베이스의 개체에 대한 논리적 일관성과 물리적 일관성을 검사합니다.|데이터베이스 페이지 수준에서 보고된 진행률입니다.<br /><br /> 진행률 보고 값은 1000개의 데이터베이스 페이지가 검사될 때마다 업데이트됩니다.|  
|DBCC TABLE REPAIR|REPAIR_FAST, REPAIR_REBUILD 또는 REPAIR_ALLOW_DATA_LOSS가 지정되어 있고 복구해야 하는 개체 오류가 있는 경우 이 단계 동안 데이터베이스 복구가 수행됩니다.|개별 복구 수준에서 보고된 진행률입니다.<br /><br /> 완료된 각 복구에 대해 카운터가 업데이트됩니다.|  
|DBCC ALLOC CHECK|이 단계 동안 데이터베이스의 할당 구조를 검사합니다.<br /><br /> 참고: DBCC CHECKALLOC은 동일한 검사를 수행합니다.|진행률이 보고되지 않습니다.|  
|DBCC ALLOC REPAIR|REPAIR_FAST, REPAIR_REBUILD 또는 REPAIR_ALLOW_DATA_LOSS가 지정되어 있고 복구해야 하는 할당 오류가 있는 경우 이 단계 동안 데이터베이스 복구가 수행됩니다.|진행률이 보고되지 않습니다.|  
|DBCC SYS CHECK|이 단계 동안 데이터베이스 시스템 테이블을 검사합니다.|데이터베이스 페이지 수준에서 보고된 진행률입니다.<br /><br /> 진행률 보고 값은 검사되는 1000개의 데이터베이스 페이지마다 업데이트됩니다.|  
|DBCC SYS REPAIR|REPAIR_FAST, REPAIR_REBUILD 또는 REPAIR_ALLOW_DATA_LOSS가 지정되어 있고 복구해야 하는 시스템 테이블 오류가 있는 경우 이 단계 동안 데이터베이스 복구가 수행됩니다.|개별 복구 수준에서 보고된 진행률입니다.<br /><br /> 완료된 각 복구에 대해 카운터가 업데이트됩니다.|  
|DBCC SSB CHECK|이 단계 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker 개체를 검사합니다.<br /><br /> 참고: DBCC CHECKTABLE이 실행될 때는 이 단계가 실행되지 않습니다.|진행률이 보고되지 않습니다.|  
|DBCC CHECKCATALOG|이 단계 동안 데이터베이스 카탈로그의 일관성을 검사합니다.<br /><br /> 참고: DBCC CHECKTABLE이 실행될 때는 이 단계가 실행되지 않습니다.|진행률이 보고되지 않습니다.|  
|DBCC IVIEW CHECK|이 단계 동안 데이터베이스에 있는 인덱싱된 뷰에 대한 논리적 일관성을 검사합니다.|검사 중인 개별 데이터베이스 뷰의 수준에서 보고된 진행률입니다.|  
  
## <a name="informational-statements"></a>알림 문  
  
|||  
|-|-|  
|[DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)|[DBCC SHOWCONTIG](../../t-sql/database-console-commands/dbcc-showcontig-transact-sql.md)|  
|[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)|[DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)|  
|[DBCC OUTPUTBUFFER](../../t-sql/database-console-commands/dbcc-outputbuffer-transact-sql.md)|[DBCC TRACESTATUS](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)|  
|[DBCC PROCCACHE](../../t-sql/database-console-commands/dbcc-proccache-transact-sql.md)|[DBCC USEROPTIONS](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)|  
|[DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)||  
  
## <a name="validation-statements"></a>유효성 검사 문  
  
|||  
|-|-|  
|[DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)|[DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)|  
|[DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)|[DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)|  
|[DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)|[DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)|  
|[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)||  
  
## <a name="maintenance-statements"></a>유지 관리 문  
  
|||  
|-|-|  
|[DBCC CLEANTABLE](../../t-sql/database-console-commands/dbcc-cleantable-transact-sql.md)|[DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)|  
|[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)|[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)|  
|[DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)|[DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)|  
|[DBCC FREEPROCCACHE](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)|[DBCC UPDATEUSAGE](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)|  
  
## <a name="miscellaneous-statements"></a>기타 문  
  
|||  
|-|-|  
|[DBCC dllname(FREE)](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)|[DBCC HELP](../../t-sql/database-console-commands/dbcc-help-transact-sql.md)|  
|[DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)|[DBCC TRACEOFF](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)|  
|[DBCC FREESESSIONCACHE](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)|[DBCC TRACEON](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)|  
|[DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)|[DBCC CLONEDATABASE](../../t-sql/database-console-commands/dbcc-clonedatabase-transact-sql.md) <br /><br /> **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2~[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
  
