---
title: DBCC CHECKTABLE (Transact-SQL) | Microsoft Docs
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKTABLE_TSQL
- DBCC_CHECKTABLE_TSQL
- DBCC CHECKTABLE
- CHECKTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- indexed views [SQL Server], DBCC CHECKTABLE
- page integrity checks [SQL Server]
- consistency [SQL Server], tables
- consistency [SQL Server], indexed views
- DBCC CHECKTABLE statement
- integrity [SQL Server]
- low overhead checks
- table integrity checks [SQL Server]
ms.assetid: 0d6cb620-eb58-4745-8587-4133a1b16994
author: pmasl
ms.author: umajay
ms.openlocfilehash: 7352a7e2db64da959cbefaacee5c9f3d14a8a579
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809885"
---
# <a name="dbcc-checktable-transact-sql"></a>DBCC CHECKTABLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

테이블 또는 인덱싱된 뷰를 구성하는 모든 페이지 및 구조의 무결성을 검사합니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
    
## <a name="syntax"></a>구문    
    
```    
DBCC CHECKTABLE     
(    
    table_name | view_name    
    [ , { NOINDEX | index_id }    
     |, { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD }     
    ]     
)    
    [ WITH     
        { [ ALL_ERRORMSGS ]    
          [ , EXTENDED_LOGICAL_CHECKS ]     
          [ , NO_INFOMSGS ]    
          [ , TABLOCK ]     
          [ , ESTIMATEONLY ]     
          [ , { PHYSICAL_ONLY | DATA_PURITY } ]     
          [ , MAXDOP = number_of_processors ]    
        }    
    ]    
```    
    
## <a name="arguments"></a>인수    
 *table_name* | *view_name*  
 무결성 검사를 실행할 테이블 또는 인덱싱된 뷰입니다. 테이블 또는 뷰 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
    
NOINDEX  
 사용자 테이블의 비클러스터형 인덱스에 대해 집중적인 검사가 수행되지 않도록 지정합니다. 이렇게 하면 전반적인 실행 시간이 줄어듭니다. 무결성 검사는 항상 모든 시스템 테이블 인덱스에서 수행되므로 NOINDEX는 시스템 테이블에 영향을 주지 않습니다.  
    
 *index_id*  
 무결성 검사를 실행할 인덱스 ID 번호입니다. *index_id*를 지정하면 DBCC CHECKTABLE은 힙 또는 클러스터형 인덱스와 함께 해당 인덱스에 대해서만 무결성 검사를 실행합니다.  
    
REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 DBCC CHECKTABLE 실행 시 발견된 오류를 복구하도록 지정합니다. 복구 옵션을 사용하려면 데이터베이스가 단일 사용자 모드여야 합니다.  
    
REPAIR_ALLOW_DATA_LOSS  
 보고된 모든 오류를 복구합니다. 이러한 복구를 수행하면 일부 데이터가 손실될 수 있습니다.  
    
REPAIR_FAST  
 이전 버전과의 호환성을 위해서만 구문이 유지됩니다. 복구 동작은 수행되지 않습니다.  
    
REPAIR_REBUILD  
 데이터 손실 가능성이 없는 복구를 수행합니다. 여기에는 비클러스터형 인덱스의 누락 행 복구와 같은 빠른 복구 작업과 인덱스 다시 빌드과 같이 시간이 오래 걸리는 복구가 모두 포함됩니다.  
 이 인수는 FILESTREAM 데이터 관련 오류를 복구하지 않습니다.  
    
 > [!NOTE]  
 > REPAIR 옵션은 최후의 수단으로만 사용하십시오. 오류를 복구하려면 백업에서 복원하는 것이 좋습니다. 복구 작업이 수행될 경우 테이블 자체나 테이블 간에 존재할 수 있는 제약 조건이 고려되지 않습니다. 지정된 테이블이 하나 이상의 제약 조건에 관련되면 복구 작업 후에 `DBCC CHECKCONSTRAINTS`를 실행하는 것이 좋습니다.
 > REPAIR를 사용해야 하는 경우 복구 옵션 없이 `DBCC CHECKTABLE`를 실행하여 사용할 복구 수준을 확인합니다. REPAIR_ALLOW_DATA_LOSS 수준을 사용하려는 경우 이 옵션으로 `DBCC CHECKTABLE`을 실행하기 전에 데이터베이스를 백업하는 것이 좋습니다.  
    
ALL_ERRORMSGS  
 오류를 개수에 제한 없이 모두 표시합니다. 기본적으로 모든 오류 메시지가 표시됩니다. 이 옵션을 지정하거나 생략하더라도 아무런 영향을 미치지 않습니다.  
    
EXTENDED_LOGICAL_CHECKS  
 호환성 수준이 100([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 이상인 경우 인덱싱된 뷰, XML 인덱스 및 공간 인덱스에 대해 논리적 일관성 검사가 수행됩니다.  
 자세한 내용은 이 항목의 뒤 부분에 나오는 [주의](#remarks) 섹션에서 *인덱스에 대한 논리적 일관성 검사 수행*을 참조하세요.  
    
NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
    
TABLOCK  
 DBCC CHECKTABLE이 내부 데이터베이스 스냅샷 대신 공유 테이블 잠금을 가져오도록 합니다. 테이블의 부하가 큰 상태에서 TABLOCK을 사용하면 DBCC CHECKTABLE의 실행 속도를 빠르게 할 수 있지만 DBCC CHECKTABLE이 실행되는 동안 테이블에서 사용할 수 있는 동시성은 줄어듭니다.  
    
ESTIMATEONLY  
 DBCC CHECKTABLE 실행에 필요한 tempdb 공간의 예상 크기와 지정된 다른 옵션을 모두 표시합니다.  
    
PHYSICAL_ONLY  
 무결성 검사를 페이지의 물리적 구조, B-트리의 물리적 구조 및 레코드 헤더로 제한합니다. 이 검사는 테이블에 대한 물리적 일관성 검사의 오버헤드를 줄이기 위한 목적으로 사용하며 데이터가 손상될 가능성이 있는 조각난 페이지와 일반적인 하드웨어 오류도 찾습니다. 다음과 같은 원인으로 DBCC CHECKTABLE 전체 실행에 이전 버전에서보다 현저히 더 많은 시간이 걸릴 수 있습니다.  
 -   논리적 검사가 더 포괄적입니다.  
 -   검사할 기본 구조 일부가 더 복잡해졌습니다.  
 -   새로운 기능을 포괄할 수 있도록 여러 가지 검사 작업이 새로 도입되었습니다.  
   
따라서 대형 테이블에서는 PHYSICAL_ONLY 옵션을 사용하여 DBCC CHECKTABLE 실행 시간을 훨씬 단축시킬 수 있으므로 생산 시스템에서의 잦은 검사 작업에는 이 옵션을 사용하는 것이 좋습니다. 하지만 정기적으로 DBCC CHECKTABLE 전체 실행을 수행하는 것이 좋습니다. 이러한 실행 빈도는 개별 비즈니스 및 프로덕션 환경과 관련된 여러 가지 요소에 따라 달라집니다. PHYSICAL_ONLY는 항상 NO_INFOMSGS를 의미하며 복구 옵션과는 함께 사용할 수 없습니다.  
    
 > [!NOTE]  
 > PHYSICAL_ONLY를 지정하면 DBCC CHECKTABLE이 FILESTREAM 데이터에 대한 모든 검사를 건너뜁니다.  
    
DATA_PURITY  
 DBCC CHECKTABLE이 테이블에서 올바르지 않거나 범위를 벗어난 열 값을 검사하도록 합니다. 예를 들어 DBCC CHECKTABLE은 **datetime** 데이터 형식으로 허용 가능한 범위보다 크거나 작은 날짜 및 시간 값을 가진 열을 검색하거나, 올바르지 않은 소수 자릿수 또는 전체 자릿수 값을 가진 **소수** 또는 근사값 데이터 형식의 열을 검색할 수 있습니다.  
 기본적으로 열 값 무결성 검사가 사용되며 DATA_PURITY 옵션은 필요하지 않습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드한 데이터베이스의 경우에는 DBCC CHECKTABLE WITH DATA_PURITY를 사용하여 특정 테이블의 오류를 찾고 수정할 수 있지만 DBCC CHECKDB WITH DATA_PURITY가 데이터베이스에서 오류 없이 실행되기 전까지는 테이블의 열 값 검사를 기본적으로 사용하지 않습니다. 이 옵션이 성공적으로 실행되면 DBCC CHECKDB 및 DBCC CHECKTABLE은 기본적으로 열 값 무결성을 검사합니다.  
 이 옵션에서 보고된 유효성 검사 오류는 DBCC 복구 옵션을 사용하여 수정할 수 없습니다. 이러한 오류를 수동으로 수정하는 방법은 기술 자료 문서 923247: [SQL Server 2005 및 이후 버전에서 DBCC 오류 2570 문제 해결](https://support.microsoft.com/kb/923247).  
 PHYSICAL_ONLY를 지정하면 열 무결성 검사는 수행되지 않습니다.  
    
MAXDOP  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]부터 시작)  
 
 명령문에 대한 **sp_configure**의 **최대 병렬 처리 수준** 구성 옵션을 재정의합니다. MAXDOP은 sp_configure로 구성한 값을 초과할 수 있습니다. MAXDOP가 Resource Governor로 구성한 값을 초과하면, 데이터베이스 엔진에서 ALTER WORKLOAD GROUP(Transact-SQL)에서 설명한 Resource Governor MAXDOP 값을 사용합니다. max degree of parallelism 구성 옵션에 사용된 모든 의미 체계 규칙을 MAXDOP 쿼리 힌트 사용 시 적용할 수 있습니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.  
    
 > [!NOTE]  
 > MAXDOP가 0으로 설정되면 서버는 최대 병렬 처리 수준을 선택합니다.  
    
## <a name="remarks"></a>Remarks    
    
> [!NOTE]    
> 데이터베이스의 모든 테이블에서 DBCC CHECKTABLE을 수행하려면 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)를 사용합니다.    
    
DBCC CHECKTABLE은 지정한 테이블에 대해 다음 사항을 검사합니다.
-   인덱스, 행 내부, LOB 및 행 오버플로 데이터 페이지가 올바로 연결되어 있습니다.    
-   인덱스 정렬 순서가 올바로 되어 있습니다.    
-   포인터가 일관성이 있습니다.    
-   각 페이지의 데이터가 적절하며 계산 열을 포함합니다.    
-   페이지 오프셋이 적절합니다.    
-   기본 테이블의 모든 행에는 각 비클러스터형 인덱스에 일치하는 행이 있으며 반대의 경우도 마찬가지입니다.    
-   분할된 테이블 또는 인덱스의 모든 행이 올바른 파티션에 있습니다.    
-   FILESTREAM을 사용하여 파일 시스템에 **varbinary(max)** 데이터를 저장할 때 파일 시스템과 테이블 사이에 연결 수준 일관성이 존재합니다.    
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>인덱스에 대한 논리적 일관성 검사 수행    
인덱스의 논리적 일관성 검사는 다음과 같이 데이터베이스의 호환성 수준에 따라 달라집니다.
-   호환성 수준이 100([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 이상인 경우:    
    -   DBCC CHECKTABLE은 NOINDEX가 지정되지 않으면 단일 테이블 및 해당하는 모든 비클러스터형 인덱스에 대해 물리적 및 논리적 일관성 검사를 모두 수행합니다. 그러나 XML 인덱스, 공간 인덱스 및 인덱싱된 뷰에 대해서는 기본적으로 물리적 일관성 검사만 수행됩니다.    
    -   WITH EXTENDED_LOGICAL_CHECKS를 지정하면 인덱싱된 뷰, XML 인덱스 및 공간 인덱스에 대해 논리적 검사가 수행됩니다. 기본적으로 물리적 일관성 검사는 논리적 일관성 검사 전에 수행됩니다. NOINDEX도 지정할 경우 논리적 검사만 수행됩니다.    
         이러한 논리적 일관성 검사는 인덱스 개체의 내부 인덱스 테이블과 이러한 테이블이 참조하는 사용자 테이블을 교차 검사합니다. 범위 외의 행을 찾기 위해 내부 쿼리가 생성되어 내부 및 사용자 테이블의 전체 교차를 수행합니다. 이 쿼리는 실행할 경우 성능에 큰 영향을 줄 수 있으며 진행 상태를 추적할 수 없습니다. 따라서 물리적 손상과 관계없는 인덱스 문제가 의심되는 경우, 또는 페이지 수준 체크섬이 해제되어 있고 열 수준 하드웨어 손상이 의심되는 경우에만 WITH EXTENDED_LOGICAL_CHECKS를 지정하는 것이 좋습니다.    
    -   인덱스가 필터링된 인덱스인 경우 DBCC CHECKDB는 일관성 검사를 수행하여 인덱스 항목이 필터 조건자를 만족하는지 확인합니다.   
      
- [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 과다한 수식 평가를 방지하기 위해 지속되는 계산된 열, UDT 열, 필터링된 인덱스에 대한 추가 검사가 기본적으로 실행되지 않습니다. 이렇게 변경하면 이 개체가 포함된 데이터베이스에 대한 CHECKDB 시간이 크게 단축됩니다. 그러나 이러한 개체의 물리적 일관성 검사는 항상 완료됩니다. EXTENDED_LOGICAL_CHECKS 옵션을 지정하는 경우에만 EXTENDED_LOGICAL_CHECKS 옵션의 일부로 기존의 논리적 검사(인덱싱된 뷰, XML 인덱스, 공간 인덱스)와 함께 식 평가가 수행됩니다.
-  호환성 수준이 90([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]) 이하인 경우 DBCC CHECKTABLE은 NOINDEX가 지정되지 않으면 단일 테이블 또는 인덱싱된 뷰와 해당하는 모든 비클러스터형 및 XML 인덱스에서 물리적 및 논리적 일관성 검사를 모두 수행합니다. 공간 인덱스는 지원되지 않습니다.
    
 **데이터베이스의 호환성 수준에 대한 자세한 내용**    
[데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>내부 데이터베이스 스냅샷    
DBCC CHECKTABLE은 이러한 검사를 수행하기 위해 확보해야 하는 트랜잭션 일관성을 제공하기 위해 내부 데이터베이스 스냅샷을 사용합니다. 자세한 내용은 [데이터베이스 스냅샷의 스파스 파일의 크기 보기&amp;#40;Transact-SQL&amp;#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) 및 [DBCC&amp;#40;Transact-SQL&amp;#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)의 "DBCC 내부 데이터베이스 스냅샷 사용법" 섹션을 참조하세요.
스냅샷을 만들 수 없거나 TABLOCK이 지정된 경우 DBCC CHECKTABLE은 공유 테이블 잠금을 획득하여 필요한 일관성을 확보합니다.
    
> [!NOTE]    
> DBCC CHECKTABLE이 tempdb에 대해 실행되는 경우 공유 테이블 잠금을 반드시 획득해야 합니다. 이것은 성능상의 이유로 tempdb의 데이터베이스 스냅샷을 사용할 수 없기 때문입니다. 즉, 필요한 트랜잭션 일관성을 얻을 수 없음을 의미합니다.    
    
## <a name="checking-and-repairing-filestream-data"></a>FILESTREAM 데이터 검사 및 복구    
데이터베이스 및 테이블에 대해 FILESTREAM을 사용하는 경우 선택적으로 파일 시스템에 **varbinary(max)** BLOB(Binary Large Object)를 저장할 수 있습니다. 파일 시스템에 BLOB을 저장하는 테이블에 대해 DBCC CHECKTABLE을 사용하면 DBCC는 파일 시스템과 데이터베이스 사이의 연결 수준 일관성을 검사합니다.
예를 들어 테이블에 FILESTREAM 특성을 사용하는 **varbinary(max)** 열이 있는 경우 DBCC CHECKTABLE은 파일 시스템 디렉터리, 파일과 테이블 행, 열, 열 값 사이에 일 대 일 매핑이 존재하는지 확인합니다. REPAIR_ALLOW_DATA_LOSS 옵션을 지정하면 DBCC CHECKTABLE이 손상을 복구할 수 있습니다. FILESTREAM 손상을 복구하기 위해 DBCC는 파일 시스템 데이터가 누락된 모든 테이블 행을 삭제하고 테이블 행, 열 또는 열 값에 매핑되지 않는 모든 디렉터리와 파일을 삭제합니다.
    
## <a name="checking-objects-in-parallel"></a>병렬로 개체 검사    
기본적으로 DBCC CHECKTABLE은 개체의 병렬 검사를 수행합니다. 병렬 처리 수준은 쿼리 프로세서에 의해 자동으로 결정됩니다. 최대 병렬 처리 수준은 최대 병렬 쿼리 수준과 동일한 방식으로 구성됩니다. DBCC 검사에 사용할 수 있는 최대 프로세서 수를 제한하려면 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용합니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.
추적 플래그 2528을 사용하면 병렬 검사를 비활성화할 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.
    
> [!NOTE]    
> DBCC CHECKTABLE 작업 중에 바이트 정렬 사용자 정의 형식 열에 저장된 바이트는 사용자 정의 형식 값의 계산된 직렬화 결과와 같아야 합니다. 그렇지 않으면 DBCC CHECKTABLE 루틴에서 일관성 오류를 보고합니다.    
    
## <a name="understanding-dbcc-error-messages"></a>DBCC 오류 메시지 이해    
DBCC CHECKTABLE 명령이 완료된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 메시지가 기록됩니다. DBCC 명령이 성공적으로 실행되면 메시지에 실행 완료 및 명령이 실행된 소요 시간이 표시됩니다. 오류로 인해 DBCC 명령이 검사를 완료하기 전에 중지되면 메시지에 명령 종료, 상태 값 및 명령이 실행된 소요 시간이 표시됩니다. 다음 표에서는 메시지에 포함될 수 있는 상태 값을 나열하고 설명합니다.
    
|State|설명|    
|-----------|-----------------|    
|0|오류 번호 8930이 발생했습니다. 메타데이터가 손상되어 DBCC 명령이 종료되었음을 나타냅니다.|    
|1|오류 번호 8967이 발생했습니다. 내부 DBCC 오류가 있습니다.|    
|2|응급 모드 데이터베이스 복구 중에 오류가 발생했습니다.|    
|3|메타데이터가 손상되어 DBCC 명령이 종료되었음을 나타냅니다.|    
|4|어설션 또는 액세스 위반이 감지되었습니다.|    
|5|알 수 없는 오류가 발생하여 DBCC 명령이 종료되었습니다.|    
    
## <a name="error-reporting"></a>오류 보고    
DBCC CHECKTABLE이 손상 오류를 발견할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] LOG 디렉터리에 미니덤프 파일(`SQLDUMP*nnnn*.txt`)이 생성됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 *기능 사용* 데이터 수집 및 *오류 보고* 기능을 설정하면 이 파일이 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에 자동으로 전달됩니다. 수집된 데이터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 향상시킬 수 있습니다.
덤프 파일에는 DBCC CHECKTABLE 명령의 결과 및 추가 진단 출력이 포함됩니다. 이 파일에는 제한된 DACL(임의 액세스 제어 목록)이 있습니다. 액세스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 및 sysadmin 역할의 멤버로 제한됩니다. 기본적으로 sysadmin 역할에는 Windows BUILTIN\Administrators 그룹 및 로컬 관리자 그룹의 모든 멤버가 포함됩니다. 데이터 수집 프로세스가 실패해도 DBCC 명령은 실패하지 않습니다.
    
## <a name="resolving-errors"></a>오류 해결    
 DBCC CHECKTABLE에서 오류를 보고하는 경우 REPAIR 옵션 중 하나를 사용하여 REPAIR를 실행하는 대신 데이터베이스 백업에서 데이터베이스를 복원하는 것이 좋습니다. 백업이 없는 경우 REPAIR를 실행하여 보고된 오류를 수정할 수 있습니다. 사용할 REPAIR 옵션은 보고된 오류 목록의 끝에 지정됩니다. 하지만 REPAIR_ALLOW_DATA_LOSS 옵션을 사용하여 오류를 수정하는 데 필요한 일부 페이지 및 데이터는 삭제되었을 수 있습니다.    
복구 작업은 사용자가 변경된 사항을 롤백할 수 있도록 사용자 트랜잭션 내에서 수행됩니다. 복구가 롤백되어도 데이터베이스에는 오류가 그대로 포함되어 있으므로 백업에서 데이터베이스를 복원해야 합니다. 복구를 모두 완료한 다음 데이터베이스를 백업하십시오.
    
## <a name="result-sets"></a>결과 집합    
DBCC CHECKTABLE은 다음 결과 집합을 반환합니다. 테이블 이름만 지정하거나 아무 옵션도 지정하지 않은 경우 동일한 결과 집합이 반환됩니다.
    
```
DBCC results for 'HumanResources.Employee'.    
There are 288 rows in 13 pages for object 'Employee'.    
DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```    
    
ESTIMATEONLY 옵션이 지정된 경우 DBCC CHECKTABLE은 다음 결과 집합을 반환합니다.
    
```
Estimated TEMPDB space needed for CHECKTABLES (KB)     
--------------------------------------------------     
21    
(1 row(s) affected)    
DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```    
    
## <a name="permissions"></a>사용 권한    
사용자는 테이블을 소유하거나 sysadmin 고정 서버 역할, db_owner 고정 데이터베이스 역할 또는 db_ddladmin 고정 데이터베이스 역할의 멤버여야 합니다.    
    
## <a name="examples"></a>예    
    
### <a name="a-checking-a-specific-table"></a>1\. 특정 테이블 검사    
다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `HumanResources.Employee`테이블에 대한 데이터 페이지 무결성을 검사합니다.
    
```sql    
DBCC CHECKTABLE ('HumanResources.Employee');    
GO    
```    
    
### <a name="b-performing-a-low-overhead-check-of-the-table"></a>2\. 테이블에 오버헤드가 적은 검사 수행    
 다음 예에서는 `Employee` 데이터베이스의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 테이블에 오버헤드가 적은 검사를 수행합니다.    
    
```sql    
DBCC CHECKTABLE ('HumanResources.Employee') WITH PHYSICAL_ONLY;    
GO    
```    
    
### <a name="c-checking-a-specific-index"></a>C. 특정 인덱스 검사    
 다음 예에서는 `sys.indexes`에 액세스하여 얻은 특정 인덱스를 검사합니다.    
    
```sql    
DECLARE @indid int;    
SET @indid = (SELECT index_id     
              FROM sys.indexes    
              WHERE object_id = OBJECT_ID('Production.Product')    
                    AND name = 'AK_Product_Name');    
DBCC CHECKTABLE ('Production.Product',@indid);    
```    
    
## <a name="see-also"></a>참고 항목    
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)     
[DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)    
    
  
