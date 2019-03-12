---
title: DBCC CHECKDB (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKDB_TSQL
- DBCC_CHECKDB_TSQL
- DBCC CHECKDB
- CHECKDB
dev_langs:
- TSQL
helpviewer_keywords:
- CHECKDB [DBCC statement]
- database objects [SQL Server], checking
- counting pages
- per-index row counts
- per-table row counts
- DBCC CHECKDB statement
- per-table page counts
- allocation checks
- integrity [SQL Server], database objects
- per-index page counts
- counting rows
- table integrity checks [SQL Server]
- row count accuracy [SQL Server]
- negative counts
- checking database objects
- page count accuracy [SQL Server]
ms.assetid: 2c506167-0b69-49f7-9282-241e411910df
author: pmasl
ms.author: umajay
manager: craigg
ms.openlocfilehash: ec8ac971776b9b069fa9fb74bea2ee6bc9a22be3
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685730"
---
# <a name="dbcc-checkdb-transact-sql"></a>DBCC CHECKDB(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

지정한 데이터베이스에서 다음 작업을 수행하여 모든 개체의 논리적 무결성 및 물리적 무결성을 검사합니다.    
    
-   데이터베이스에 대해 [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)를 실행합니다.    
-   데이터베이스의 모든 테이블 및 뷰에 대해 [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)을 실행합니다.    
-   데이터베이스에 대해 [DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)를 실행합니다.    
-   데이터베이스에 있는 모든 인덱싱된 뷰의 내용에 대한 유효성을 검사합니다.    
-   FILESTREAM을 사용하여 파일 시스템에 **varbinary(max)** 데이터를 저장할 때 테이블 메타데이터와 파일 시스템 디렉터리 및 파일 간의 연결 수준 일관성에 대한 유효성을 검사합니다.    
-   데이터베이스에 있는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 데이터의 유효성을 검사합니다.    
    
이는 DBCC CHECKALLOC, DBCC CHECKTABLE 또는 DBCC CHECKCATALOG 명령을 DBCC CHECKDB와 별도로 실행할 필요가 없음을 의미합니다. 이러한 명령이 수행하는 검사에 대한 자세한 내용은 해당 명령의 설명을 참조하십시오.    
 
> [!NOTE]
> DBCC CHECKDB는 메모리 최적화 테이블을 포함하는 데이터베이스에서 지원되지만 유효성 검사는 디스크 기반 테이블에서만 수행됩니다. 그러나 데이터베이스 백업 및 복구의 일부로 메모리 최적화 파일 그룹의 파일에 대해 CHECKSUM 유효성 검사가 수행됩니다.    
>     
> 메모리 최적화 테이블에는 DBCC 복구 옵션을 사용할 수 없기 때문에 정기적으로 데이터베이스를 백업하고 백업을 테스트해야 합니다. 메모리 최적화 테이블에서 데이터 무결성 문제가 발생하는 경우 마지막 양호한 백업에서 복원해야 합니다.    

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>구문    
    
```    
DBCC CHECKDB     
    [ ( database_name | database_id | 0    
        [ , NOINDEX     
        | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]    
    ) ]    
    [ WITH     
        {    
            [ ALL_ERRORMSGS ]    
            [ , EXTENDED_LOGICAL_CHECKS ]     
            [ , NO_INFOMSGS ]    
            [ , TABLOCK ]    
            [ , ESTIMATEONLY ]    
            [ , { PHYSICAL_ONLY | DATA_PURITY } ]    
            [ , MAXDOP  = number_of_processors ]    
        }    
    ]    
]    
```    
    
## <a name="arguments"></a>인수    
 *database_name* | *database_id* | 0  
 무결성 검사를 실행할 데이터베이스의 이름 또는 ID입니다. 아무 값도 지정하지 않거나 0을 지정하면 현재 데이터베이스가 사용됩니다. 데이터베이스 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 준수해야 합니다.  
    
NOINDEX  
 사용자 테이블의 비클러스터형 인덱스에 대해 집중적인 검사가 수행되지 않도록 지정합니다. 이렇게 하면 전반적인 실행 시간이 줄어듭니다. 시스템 테이블 인덱스에서는 무결성 검사가 항상 수행되므로 NOINDEX는 시스템 테이블에 영향을 주지 않습니다.  
    
REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 DBCC CHECKDB 실행 시 검색된 오류를 복구하도록 지정합니다. REPAIR 옵션은 최후의 수단으로만 사용하십시오. 다음 복구 옵션 중 하나를 사용하려면 지정된 데이터베이스가 단일 사용자 모드여야 합니다.  
    
REPAIR_ALLOW_DATA_LOSS  
 보고된 모든 오류를 복구합니다. 이러한 복구를 수행하면 일부 데이터가 손실될 수 있습니다.  
    
> [!WARNING]
> REPAIR_ALLOW_DATA_LOSS 옵션은 지원되는 기능이지만, 데이터베이스를 물리적으로 일관된 상태로 전환하는 것이 항상 가장 적합한 옵션인 것은 아닙니다. 성공할 경우 REPAIR_ALLOW_DATA_LOSS 옵션 때문에 일부 데이터가 손실될 수 있습니다. 실제로 사용자가 마지막으로 알려진 성공한 백업으로부터 데이터베이스를 복원했던 것보다 더 많은 데이터가 손실될 수 있습니다. 
>
> [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서는 항상 DBCC CHECKDB에서 보고된 오류로부터 복구하는 기본 방법으로 마지막으로 알려진 성공한 백업으로부터의 사용자 복원을 권장합니다. REPAIR_ALLOW_DATA_LOSS 옵션은 알려진 성공한 백업으로부터 복원하는 방법 대신 사용할 수 없습니다. 백업으로부터 복원할 수 없는 경우에만 사용하도록 권장되는 응급 "최후의 수단"으로 사용하는 옵션입니다.    
>     
> REPAIR_ALLOW_DATA_LOSS 옵션을 사용해야 복구할 수 있는 특정 오류에는 오류를 지우기 위한 행, 페이지 또는 일련의 페이지 할당 취소가 포함됩니다. 할당 취소된 모든 데이터는 사용자가 더 이상 액세스하거나 복구할 수 없고 할당 취소된 데이터의 정확한 내용을 확인할 수 없습니다. 따라서 행이나 페이지가 할당 취소되고 나면 외래 키 제약 조건이 복구 작업 일부로 확인되거나 유지 관리되지 않으므로 참조 무결성이 정확하지 않을 수 있습니다. REPAIR_ALLOW_DATA_LOSS 옵션을 사용하고 나서 사용자는 DBCC CHECKCONSTRAINTS를 사용하여 데이터베이스의 참조 무결성을 검사해야 합니다.    
>     
> 복구를 수행하기 전에 이 데이터베이스에 속하는 파일의 물리적 복사본을 만듭니다. 여기에는 주 데이터 파일(.mdf), 보조 데이터 파일(.ndf), 모든 트랜잭션 로그 파일(.ldf) 및 전체 텍스트 카탈로그, 파일 스트림 폴더, 메모리 최적화 데이터 등을 포함하여 데이터베이스를 구성하는 기타 컨테이너가 포함됩니다.    
>     
> 복구를 수행하기 전에 데이터베이스 상태를 EMERGENCY 모드로 변경하고 중요 테이블에서 가능한 한 많은 정보를 추출하고 해당 데이터를 저장하는 것이 좋습니다.    
    
REPAIR_FAST  
 이전 버전과의 호환성을 위해서만 구문을 유지 관리합니다. 복구 동작은 수행되지 않습니다.  
    
REPAIR_REBUILD  
 데이터 손실 가능성이 없는 복구를 수행합니다. 여기에는 비클러스터형 인덱스의 누락 행 복구와 같은 빠른 복구 작업과 인덱스 다시 작성과 같이 시간이 오래 걸리는 복구가 모두 포함됩니다.  
 이 인수는 FILESTREAM 데이터 관련 오류를 복구하지 않습니다.  
    
> [!IMPORTANT] 
> REPAIR 옵션이 있는 DBCC CHECKDB는 완전히 기록되고 복구 가능하므로 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서는 항상 사용자가 작업 결과를 허용할지 확인할 수 있도록 트랜잭션 내에서 CHECKDB를 REPAIR 옵션과 함께 사용(명령을 실행하기 전에 BEGIN TRANSACTION 실행)하도록 권장합니다. 그리고 나서 사용자는 COMMIT TRANSACTION을 실행하여 복구 작업으로 수행된 모든 작업을 커밋할 수 있습니다. 작업 결과를 허용하지 않으려면 사용자는 ROLLBACK TRANSACTION을 실행하여 복구 작업의 효과를 실행 취소할 수 있습니다.    
>     
> 오류를 복구하려면 백업에서 복원하는 것이 좋습니다. 복구 작업이 수행될 경우 테이블 자체나 테이블 간에 존재할 수 있는 제약 조건이 고려되지 않습니다. 지정된 테이블이 하나 이상의 제약 조건에 관련되면 복구 작업 후에 DBCC CHECKCONSTRAINTS를 실행하는 것이 좋습니다. REPAIR를 사용해야 하는 경우 복구 옵션 없이 DBCC CHECKDB를 실행하여 사용할 복구 수준을 확인합니다. REPAIR_ALLOW_DATA_LOSS 수준을 사용하는 경우 이 옵션으로 DBCC CHECKDB를 실행하기 전에 데이터베이스를 백업하는 것이 좋습니다.    
    
ALL_ERRORMSGS  
 개체당 보고되는 모든 오류를 표시합니다. 기본적으로 모든 오류 메시지가 표시됩니다. 이 옵션을 지정하거나 생략하더라도 아무런 영향을 미치지 않습니다. [tempdb 데이터베이스](../../relational-databases/databases/tempdb-database.md)에서 생성된 메시지를 제외한 모든 오류 메시지는 개체 ID를 기준으로 정렬됩니다.     

EXTENDED_LOGICAL_CHECKS  
 호환성 수준이 100([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 이상인 경우 인덱싱된 뷰, XML 인덱스 및 공간 인덱스에 대해 논리적 일관성 검사가 수행됩니다.  
 자세한 내용은 이 항목의 뒤 부분에 나오는 [Remarks](#remarks) 섹션에서 *인덱스에 대한 논리적 일관성 검사 수행*을 참조하세요.  
    
NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
    
TABLOCK  
 내부 데이터베이스 스냅숏을 사용하는 대신 DBCC CHECKDB가 잠금을 가져오도록 합니다. 여기에는 데이터베이스에 대한 단기 배타(X) 잠금이 포함됩니다. TABLOCK을 사용하면 데이터베이스에 로드가 많은 상황에서 DBCC CHECKDB가 더 빠르게 실행됩니다. 그러나 DBCC CHECKDB가 실행되는 동안 데이터베이스의 동시 사용 가능성은 줄어듭니다.  
    
> [!IMPORTANT] 
> TABLOCK은 수행되는 검사를 제한합니다. 데이터베이스에 대해 DBCC CHECKCATALOG가 실행되지 않으며 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 데이터의 유효성이 검사되지 않습니다.
    
ESTIMATEONLY  
 지정된 다른 모든 옵션으로 DBCC CHECKDB를 실행하는 데 필요한 tempdb 공간의 예상 크기를 표시합니다. 실제 데이터베이스 검사는 수행되지 않습니다.  
    
PHYSICAL_ONLY  
 페이지 및 레코드 헤더의 물리적 구조의 무결성 및 데이터베이스 할당 일관성으로 검사를 제한합니다. 이 검사는 데이터베이스의 물리적 일관성 검사의 오버헤드를 줄이기 위한 목적으로 사용하며 사용자의 데이터를 손상시킬 가능성이 있는 조각난 페이지와 체크섬 오류, 그리고 일반적인 하드웨어 오류도 찾을 수 있습니다.  
 DBCC CHECKDB 전체 실행이 완료되는 데 걸리는 시간이 이전 버전이 비해 상당히 오래 걸릴 수 있습니다. 그 이유는 다음과 같습니다.  
 -   논리적 검사가 더 포괄적입니다.  
 -   검사할 기본 구조 일부가 더 복잡해졌습니다.  
 -   새로운 기능을 포괄할 수 있도록 여러 가지 검사 작업이 새로 도입되었습니다.  
 따라서 대형 데이터베이스에서는 PHYSICAL_ONLY 옵션을 사용하여 DBCC CHECKDB 실행 시간을 훨씬 단축시킬 수 있으므로 생산 시스템에서의 잦은 검사 작업에는 이 옵션을 사용하는 것이 좋습니다. 하지만 정기적으로 DBCC CHECKDB 전체 실행을 수행하는 것이 좋습니다. 이러한 실행 빈도는 개별 비즈니스 및 프로덕션 환경과 관련된 여러 가지 요소에 따라 달라집니다.    
이 인수는 항상 NO_INFOMSGS를 의미하며 복구 옵션과는 함께 사용할 수 없습니다.  
    
> [!WARNING] 
> PHYSICAL_ONLY를 지정하면 DBCC CHECKDB가 FILESTREAM 데이터에 대한 모든 검사를 건너뜁니다.
    
DATA_PURITY  
 DBCC CHECKDB가 데이터베이스에서 올바르지 않거나 범위를 벗어난 열 값을 검사하도록 합니다. 예를 들어 DBCC CHECKDB는 **datetime** 데이터 형식으로 허용 가능한 범위보다 크거나 작은 날짜 및 시간 값을 가진 열을 검색하거나, 올바르지 않은 소수 자릿수 또는 전체 자릿수 값을 가진 **소수** 또는 근사값 데이터 형식의 열을 검색할 수 있습니다.  
 기본적으로 열 값 무결성 검사가 사용되며 DATA_PURITY 옵션은 필요하지 않습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드한 데이터베이스의 경우에는 DBCC CHECKDB WITH DATA_PURITY가 데이터베이스에서 오류 없이 실행되기 전까지는 열 값 검사가 기본적으로 사용되지 않습니다. 이 옵션이 성공적으로 실행되면 DBCC CHECKDB는 기본적으로 열 값 무결성을 검사합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스를 업그레이드함에 따라 CHECKDB가 어떤 영향을 받는지에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 주의 섹션을 참조하십시오.  
    
> [!WARNING]
> PHYSICAL_ONLY를 지정하면 열 무결성 검사는 수행되지 않습니다.
    
 이 옵션에서 보고된 유효성 검사 오류는 DBCC 복구 옵션을 사용하여 수정할 수 없습니다. 이러한 오류를 수동으로 수정하는 방법은 기술 자료 문서 923247: [SQL Server 2005 이상 버전에서 DBCC 오류 2570 문제 해결](https://support.microsoft.com/kb/923247)을 참조하세요.  
    
 MAXDOP  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
    
 명령문에 대한 **sp_configure**의 **최대 병렬 처리 수준** 구성 옵션을 재정의합니다. MAXDOP은 sp_configure로 구성한 값을 초과할 수 있습니다. MAXDOP가 Resource Governor로 구성한 값을 초과하면 [!INCLUDE[ssDEnoversion](../../includes/ssDEnoversion_md.md)]가 [ALTER WORKLOAD GROUP](../../t-sql/statements/alter-workload-group-transact-sql.md)에서 설명한 Resource Governor MAXDOP 값을 사용합니다. max degree of parallelism 구성 옵션에 사용된 모든 의미 체계 규칙을 MAXDOP 쿼리 힌트 사용 시 적용할 수 있습니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.  
 
> [!WARNING] 
> MAXDOP가 0으로 설정되면 SQL Server는 최대 병렬 처리 수준을 사용하도록 선택합니다.    

## <a name="remarks"></a>Remarks    
DBCC CHECKDB는 비활성화된 인덱스는 검사하지 않습니다. 비활성 인덱스에 대한 자세한 내용은 [인덱스 및 제약 조건 비활성화](../../relational-databases/indexes/disable-indexes-and-constraints.md)를 참조하세요.    

사용자 정의 형식이 바이트 정렬된 것으로 표시되면 사용자 정의 형식의 직렬화가 하나만 있어야 합니다. 바이트 정렬된 사용자 정의 형식의 일관성 있는 직렬화가 없으면 DBCC CHECKDB를 실행할 때 오류 2537이 발생합니다. 자세한 내용은 [사용자 정의 형식 요구 사항](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-requirements.md)을 참조하세요.    

[리소스 데이터베이스](../../relational-databases/databases/resource-database.md)는 단일 사용자 모드에서만 수정할 수 있으므로 DBCC CHECKDB 명령은 이 데이터베이스에 대해 직접 실행할 수 없습니다. 하지만 [마스터 데이터베이스](../../relational-databases/databases/master-database.md)에 대해 DBCC CHECKDB를 실행할 때 또 다른 CHECKDB가 리소스 데이터베이스에 대해 내부적으로 실행되므로 DBCC CHECKDB가 추가적인 결과를 반환할 수 있습니다. 옵션을 설정하지 않거나 PHYSICAL_ONLY 또는 ESTIMATEONLY 옵션 중 하나를 설정하면 추가적인 결과 집합이 반환됩니다.    

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2부터 DBCC CHECKDB를 실행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 계획 캐시가 삭제되지 **않습니다**. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2 이전에서는 DBCC CHECKDB를 실행하면 계획 캐시가 삭제됩니다. 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>인덱스에 대한 논리적 일관성 검사 수행    
인덱스의 논리적 일관성 검사는 다음과 같이 데이터베이스의 호환성 수준에 따라 달라집니다.
-   호환성 수준이 100([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 이상인 경우:    
-   DBCC CHECKTABLE은 NOINDEX가 지정되지 않으면 단일 테이블 및 해당하는 모든 비클러스터형 인덱스에 대해 물리적 및 논리적 일관성 검사를 모두 수행합니다. 그러나 XML 인덱스, 공간 인덱스 및 인덱싱된 뷰에 대해서는 기본적으로 물리적 일관성 검사만 수행됩니다.
-   WITH EXTENDED_LOGICAL_CHECKS를 지정하면 인덱싱된 뷰, XML 인덱스 및 공간 인덱스에 대해 논리적 검사가 수행됩니다. 기본적으로 물리적 일관성 검사는 논리적 일관성 검사 전에 수행됩니다. NOINDEX도 지정할 경우 논리적 검사만 수행됩니다.
    
이러한 논리적 일관성 검사는 인덱스 개체의 내부 인덱스 테이블과 이러한 테이블이 참조하는 사용자 테이블을 교차 검사합니다. 범위 외의 행을 찾기 위해 내부 쿼리가 생성되어 내부 및 사용자 테이블의 전체 교차를 수행합니다. 이 쿼리는 실행할 경우 성능에 큰 영향을 줄 수 있으며 진행 상태를 추적할 수 없습니다. 따라서 물리적 손상과 관계없는 인덱스 문제가 의심되는 경우, 또는 페이지 수준 체크섬이 해제되어 있고 열 수준 하드웨어 손상이 의심되는 경우에만 WITH EXTENDED_LOGICAL_CHECKS를 지정하는 것이 좋습니다.
-   인덱스가 필터링된 인덱스인 경우 DBCC CHECKDB는 일관성 검사를 수행하여 인덱스 항목이 필터 조건자를 만족하는지 확인합니다.
-   호환성 수준이 90 이하인 경우 DBCC CHECKTABLE은 NOINDEX가 지정되지 않으면 단일 테이블 또는 인덱싱된 뷰와 해당하는 모든 비클러스터형 및 XML 인덱스에서 물리적 및 논리적 일관성 검사를 모두 수행합니다. 공간 인덱스는 지원되지 않습니다.  
- SQL Server 2016 이상에서는 과다한 수식 평가를 방지하기 위해 지속되는 계산된 열, UDT 열, 필터링된 인덱스에 대한 추가 검사가 기본적으로 실행되지 않습니다. 이렇게 변경하면 이 개체가 포함된 데이터베이스에 대한 CHECKDB 시간이 크게 단축됩니다. 그러나 이러한 개체의 물리적 일관성 검사는 항상 완료됩니다. EXTENDED_LOGICAL_CHECKS 옵션을 지정하는 경우에만 EXTENDED_LOGICAL_CHECKS 옵션의 일부로 기존의 논리적 검사(인덱싱된 뷰, XML 인덱스, 공간 인덱스)와 함께 식 평가가 수행됩니다.   
    
**데이터베이스의 호환성 수준에 대한 자세한 내용**
-   [데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>내부 데이터베이스 스냅숏    
DBCC CHECKDB는 이러한 검사를 수행하는 데 필요한 트랜잭션 일관성을 위해 내부 데이터베이스 스냅숏을 사용합니다. 이렇게 하면 이러한 명령이 실행될 때 차단 및 동시성 문제를 방지할 수 있습니다. 자세한 내용은 [데이터베이스 스냅숏의 스파스 파일의 크기 보기&#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) 및 [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)의 "DBCC 내부 데이터베이스 스냅숏 사용법" 섹션을 참조하세요. 스냅숏을 만들 수 없거나 TABLOCK이 지정되면 DBCC CHECKDB는 필요한 일관성을 확보하기 위해 잠금을 설정합니다. 이 경우 할당 검사를 위해서는 배타적 데이터베이스 잠금이 필요하며 테이블 검사를 위해서는 공유 테이블 잠금이 필요합니다.
내부 데이터베이스 스냅숏을 생성할 수 없는 경우 마스터에 대한 DBCC CHECKDB 실행은 실패합니다.
tempdb에 대해 DBCC CHECKDB를 실행할 경우 할당 또는 카탈로그 검사는 수행되지 않으며 테이블 검사를 수행하려면 공유 테이블 잠금을 설정해야 합니다. 이것은 성능상의 이유로 tempdb의 데이터베이스 스냅숏을 사용할 수 없기 때문입니다. 즉, 필요한 트랜잭션 일관성을 얻을 수 없음을 의미합니다.
Microsoft SQL Server 2012 또는 그 전의 SQL Server 버전에서는 ReFS로 포맷된 볼륨에 파일이 있는 데이터베이스에 대해 DBCC CHECKDB 명령을 실행하면 오류 메시지가 발생할 수 있습니다. 자세한 내용은 기술 자료 문서 2974455: [SQL Server 데이터베이스가 ReFS 볼륨에 있는 경우 DBCC CHECKDB 동작](https://support.microsoft.com/kb/2974455)을 참조하세요.    
    
## <a name="checking-and-repairing-filestream-data"></a>FILESTREAM 데이터 검사 및 복구    
데이터베이스 및 테이블에 대해 FILESTREAM을 사용하는 경우 선택적으로 파일 시스템에 **varbinary(max)** BLOB(Binary Large Object)를 저장할 수 있습니다. 파일 시스템에 BLOB을 저장하는 데이터베이스에 대해 DBCC CHECKDB를 사용하면 DBCC는 파일 시스템과 데이터베이스 사이의 연결 수준 일관성을 검사합니다.
예를 들어 테이블에 FILESTREAM 특성을 사용하는 **varbinary(max)** 열이 있는 경우 DBCC CHECKDB는 파일 시스템 디렉터리, 파일과 테이블 행, 열, 열 값 사이에 일 대 일 매핑이 존재하는지 확인합니다. REPAIR_ALLOW_DATA_LOSS 옵션을 지정하면 DBCC CHECKDB가 손상을 복구할 수 있습니다. FILESTREAM 손상을 복구하기 위해 DBCC에서는 파일 시스템 데이터가 없는 테이블 행을 삭제합니다.
    
## <a name="best-practices"></a>최선의 구현 방법    
프로덕션 시스템에서 자주 사용하려면 PHYSICAL_ONLY 옵션을 사용하는 것이 좋습니다. PHYSICAL_ONLY를 사용하면 큰 데이터베이스에 대한 DBCC CHECKDB 실행 시간이 훨씬 단축될 수 있습니다. 또한 옵션을 지정하지 않고 정기적으로 DBCC CHECKDB를 실행하는 것이 좋습니다. 실행 빈도는 개별 비즈니스 및 프로덕션 환경에 따라 달라집니다.
    
## <a name="checking-objects-in-parallel"></a>병렬로 개체 검사    
기본적으로 DBCC CHECKDB는 개체를 병렬로 검사합니다. 병렬 처리 수준은 쿼리 프로세서에 의해 자동으로 결정됩니다. 최대 병렬 처리 수준은 병렬 쿼리와 동일하게 구성됩니다. DBCC 검사에 사용할 수 있는 최대 프로세서 수를 제한하려면 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용합니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요. 추적 플래그 2528을 사용하면 병렬 검사를 비활성화할 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.
    
> [!NOTE]
> 이 기능은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. 자세한 내용은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)의 RDBMS 관리 효율성 섹션에 있는 병렬 일관성 검사를 참조하세요.    
    
## <a name="understanding-dbcc-error-messages"></a>DBCC 오류 메시지 이해    
DBCC CHECKDB 명령이 완료된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 메시지가 기록됩니다. DBCC 명령이 성공적으로 실행되면 메시지에 성공 및 명령이 실행된 소요 시간이 표시됩니다. 오류로 인해 DBCC 명령이 검사를 완료하기 전에 중지되면 메시지에 명령 종료, 상태 값 및 명령이 실행된 소요 시간이 표시됩니다. 다음 표에서는 메시지에 포함될 수 있는 상태 값을 나열하고 설명합니다.
    
|State|설명|    
|-----------|-----------------|    
|0|오류 번호 8930이 발생했습니다. 메타데이터가 손상되어 DBCC 명령이 종료되었음을 나타냅니다.|    
|1|오류 번호 8967이 발생했습니다. 내부 DBCC 오류가 있습니다.|    
|2|응급 모드 데이터베이스 복구 중에 오류가 발생했습니다.|    
|3|메타데이터가 손상되어 DBCC 명령이 종료되었음을 나타냅니다.|    
|4|어설션 또는 액세스 위반이 감지되었습니다.|    
|5|알 수 없는 오류가 발생하여 DBCC 명령이 종료되었습니다.|    
    
## <a name="error-reporting"></a>오류 보고    
DBCC CHECKDB가 손상 오류를 감지할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] LOG 디렉터리에 덤프 파일(`SQLDUMP*nnnn*.txt`)이 생성됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 *기능 사용* 데이터 수집 및 *오류 보고* 기능을 설정하면 이 파일이 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에 자동으로 전달됩니다. 수집된 데이터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 향상시킬 수 있습니다.
덤프 파일에는 DBCC CHECKDB 명령의 결과 및 추가 진단 출력이 포함됩니다. 액세스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 및 sysadmin 역할의 멤버로 제한됩니다. 기본적으로 sysadmin 역할에는 Windows `BUILTIN\Administrators` 그룹 및 로컬 관리자 그룹의 모든 멤버가 포함됩니다. 데이터 수집 프로세스가 실패해도 DBCC 명령은 실패하지 않습니다.
    
## <a name="resolving-errors"></a>오류 해결    
DBCC CHECKDB에 의해 오류가 보고되면 REPAIR 옵션 중 하나를 사용해 REPAIR를 실행하는 대신 데이터베이스 백업으로부터 데이터베이스를 복원하는 것이 좋습니다. 백업이 없을 경우 REPAIR를 실행하면 보고된 오류를 수정할 수 있습니다. 사용할 복구 옵션은 보고된 오류 목록 끝에 지정됩니다. 하지만 REPAIR_ALLOW_DATA_LOSS 옵션을 사용하여 오류를 수정하는 데 필요한 일부 페이지 및 데이터는 삭제되었을 수 있습니다.    

경우에 따라서는 열의 데이터 형식을 기반으로 데이터베이스에 입력된 값이 잘못되었거나 범위를 벗어날 수 있습니다. DBCC CHECKDB가 모든 열 데이터 형식에 대해 올바르지 않은 열 값을 검색할 수 있습니다. 따라서 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드된 데이터베이스에서 DATA_PURITY 옵션을 사용해 DBCC CHECKDB를 실행하면 기존의 열 값 오류가 드러날 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 오류를 자동으로 복구할 수 없기 때문에 열 값은 수동으로 업데이트해야 합니다. CHECKDB는 이러한 오류를 검색하면 경고 및 오류 번호 2570, 그리고 영향을 받은 행을 식별하고 수동으로 오류를 수정하기 위한 정보를 반환합니다.    

복구 작업은 사용자가 변경 내용을 롤백할 수 있도록 사용자 트랜잭션 내에서 수행할 수 있습니다. 복구가 롤백되어도 데이터베이스에는 오류가 그대로 포함되어 있으므로 백업에서 데이터베이스를 복원해야 합니다. 복구를 완료한 후 데이터베이스를 백업하십시오.
    
## <a name="resolving-errors-in-database-emergency-mode"></a>데이터베이스 응급 모드로 오류 해결    
[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을 사용하여 데이터베이스가 응급 모드로 설정된 경우 REPAIR_ALLOW_DATA_LOSS 옵션을 지정하면 DBCC CHECKDB는 데이터베이스에 대해 특별한 복구 작업을 수행할 수 있습니다. 이러한 복구 작업을 사용하면 일반적으로 복구 불가능한 데이터베이스가 물리적으로 일관된 상태로 다시 온라인 상태가 될 수 있습니다. 백업에서 데이터베이스를 복원할 수 없는 경우에만 최후의 수단으로 이러한 복구 작업을 사용해야 합니다. 데이터베이스를 응급 모드로 설정하면 데이터베이스가 READ_ONLY로 표시되며 로깅 설정이 해제되고 액세스가 sysadmin 고정 서버 역할의 멤버로 제한됩니다.
    
> [!NOTE]
> 사용자 트랜잭션 내부에서 응급 모드로 DBCC CHECKDB 명령을 실행하고 실행 후에 트랜잭션을 롤백할 수는 없습니다.    
    
데이터베이스가 응급 모드에 있고 REPAIR_ALLOW_DATA_LOSS 절이 있는 DBCC CHECKDB를 실행하면 다음 동작이 수행됩니다.
-   DBCC CHECKDB는 I/O 또는 체크섬 오류로 인해 액세스가 불가능하다고 표시된 페이지를 오류가 발생하지 않은 것처럼 사용합니다. 이렇게 할 경우 데이터베이스의 데이터 복구 기회가 많아집니다.    
-   DBCC CHECKDB는 일반적인 로그 기반의 복구 기술을 사용하여 데이터베이스 복구를 시도합니다.    
-   트랜잭션 로그 손상으로 인해 데이터베이스 복구가 실패하면 트랜잭션 로그가 다시 작성됩니다. 트랜잭션 로그를 다시 작성하면 트랜잭션 일관성을 유지할 수 없습니다.    
    
> [!WARNING]
> REPAIR_ALLOW_DATA_LOSS 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 지원되는 기능입니다. 그러나 데이터베이스를 물리적으로 일관된 상태로 전환하는 것이 항상 가장 적합한 옵션인 것은 아닙니다. 성공할 경우 REPAIR_ALLOW_DATA_LOSS 옵션 때문에 일부 데이터가 손실될 수 있습니다. 실제로 사용자가 마지막으로 알려진 성공한 백업으로부터 데이터베이스를 복원했던 것보다 더 많은 데이터가 손실될 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서는 항상 DBCC CHECKDB에서 보고된 오류로부터 복구하는 기본 방법으로 마지막으로 알려진 성공한 백업으로부터의 사용자 복원을 권장합니다. REPAIR_ALLOW_DATA_LOSS 옵션은 알려진 성공한 백업으로부터 복원하는 방법 대신 사용할 수 **없습니다**. 백업으로부터 복원할 수 없는 경우에만 사용하도록 권장되는 응급 "최후의 수단"으로 사용하는 옵션입니다.    
>     
>  로그를 다시 작성하고 나면 전체 ACID가 보장되지 않습니다.    
>     
>  로그를 다시 작성하고 나면 DBCC CHECKDB가 자동으로 실행되어 물리적 일관성 문서를 보고하고 수정합니다.    
>     
>  논리적 데이터 일관성 및 비즈니스 논리가 적용된 제약 조건은 수동으로 유효성 검사해야 합니다.    
>     
>  트랜잭션 로그 크기는 기본 크기로 유지되며 다시 최근 크기로 수동으로 조정해야 합니다.    
    
DBCC CHECKDB 명령이 성공하면 데이터베이스는 물리적으로 일관된 상태가 되며 데이터베이스 상태가 ONLINE으로 설정됩니다. 그러나 데이터베이스에 하나 이상의 트랜잭션 불일치가 포함되어 있을 수 있습니다. [DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)를 실행하여 비즈니스 논리 결함을 식별하고 즉시 데이터베이스를 백업하는 것이 좋습니다.
DBCC CHECKDB 명령이 실패하면 데이터베이스를 복구할 수 없습니다.
    
## <a name="running-dbcc-checkdb-with-repairallowdataloss-in-replicated-databases"></a>복제된 데이터베이스에서 REPAIR_ALLOW_DATA_LOSS 옵션으로 DBCC CHECKDB 실행    
REPAIR_ALLOW_DATA_LOSS 옵션으로 DBCC CHECKDB 명령을 실행하면 사용자 데이터베이스(게시 및 구독 데이터베이스)와 복제에 사용되는 배포 데이터베이스에 영향을 줄 수 있습니다. 게시 및 구독 데이터베이스에는 게시된 테이블과 복제 메타데이터 테이블이 포함됩니다. 이러한 데이터베이스에서 발생 가능한 다음 문제에 주의하십시오.
-   게시된 테이블. 손상된 사용자 데이터를 복구하기 위해 CHECKDB 프로세스에서 수행한 동작이 복제되지 않을 수 있습니다.    
-   병합 복제는 트리거를 사용하여 게시된 테이블의 변경 내용을 추적합니다. CHECKDB 프로세스에서 행을 삽입, 업데이트 또는 삭제하면 트리거가 발생하지 않으므로 변경 내용이 복제되지 않습니다.
-   트랜잭션 복제는 트랜잭션 로그를 사용하여 게시된 테이블의 변경 내용을 추적합니다. 그런 다음 로그 판독기 에이전트가 이러한 변경 내용을 배포 데이터베이스로 이동합니다. 일부 DBCC 복구는 기록만 되고 로그 판독기 에이전트에서 복제할 수 없습니다. 예를 들어 CHECKDB 프로세스에서 데이터 페이지를 할당 취소한 경우 로그 판독기 에이전트가 이를 DELETE 문으로 변환하지 않으므로 변경 내용이 복제되지 않습니다.
-   복제 메타데이터 테이블. 손상된 복제 메타데이터 테이블을 복구하기 위해 CHECKDB 프로세스에서 수행한 동작 때문에 복제를 제거하고 다시 구성해야 합니다.    
    
사용자 데이터베이스 또는 배포 데이터베이스에 대해 REPAIR_ALLOW_DATA_LOSS 옵션으로 DBCC CHECKDB 명령을 실행해야 하는 경우 다음 작업을 수행합니다.
1.  시스템을 정지합니다. 해당 데이터베이스와 복제 토폴로지에 있는 다른 모든 데이터베이스에서 작업을 중지하고 모든 노드를 동기화합니다. 자세한 내용은 [복제 토폴로지 정지&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)를 참조하세요.    
1.  DBCC CHECKDB를 실행합니다.    
1.  DBCC CHECKDB 보고서에 배포 데이터베이스의 테이블이나 사용자 데이터베이스의 복제 메타데이터 테이블에 대한 복구가 포함되어 있으면 복제를 제거하고 다시 구성합니다. 자세한 내용은 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)를 참조하세요.    
1.  DBCC CHECKDB 보고서에 복제된 테이블에 대한 복구가 포함되어 있으면 데이터 유효성 검사를 통해 복제 데이터베이스와 구독 데이터베이스의 데이터가 서로 다른지 확인합니다.    
    
## <a name="result-sets"></a>결과 집합    
DBCC CHECKDB는 다음 결과 집합을 반환합니다. ESTIMATEONLY, PHYSICAL_ONLY 또는 NO_INFOMSGS 옵션이 지정된 경우를 제외하고는 값이 다를 수 있습니다.
    
```
 DBCC results for 'model'.    
    
 Service Broker Msg 9675, Level 10, State 1: Message Types analyzed: 13.    
    
 Service Broker Msg 9676, Level 10, State 1: Service Contracts analyzed: 5.    
    
 Service Broker Msg 9667, Level 10, State 1: Services analyzed: 3.    
    
 Service Broker Msg 9668, Level 10, State 1: Service Queues analyzed: 3.    
    
 Service Broker Msg 9669, Level 10, State 1: Conversation Endpoints analyzed: 0.    
    
 Service Broker Msg 9674, Level 10, State 1: Conversation Groups analyzed: 0.    
    
 Service Broker Msg 9670, Level 10, State 1: Remote Service Bindings analyzed: 0.    
    
 DBCC results for 'sys.sysrowsetcolumns'.    
    
 There are 630 rows in 7 pages for object 'sys.sysrowsetcolumns'.    
    
 DBCC results for 'sys.sysrowsets'.    
    
 There are 97 rows in 1 pages for object 'sys.sysrowsets'.    
    
 DBCC results for 'sysallocunits'.    
    
 There are 195 rows in 3 pages for object 'sysallocunits'.    
    
 There are 0 rows in 0 pages for object "sys.sysasymkeys".    
    
 DBCC results for 'sys.syssqlguides'.    
    
 There are 0 rows in 0 pages for object "sys.syssqlguides".    
    
 DBCC results for 'sys.queue_messages_1977058079'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_1977058079".    
    
 DBCC results for 'sys.queue_messages_2009058193'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2009058193".    
    
 DBCC results for 'sys.queue_messages_2041058307'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2041058307".    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'model'.    
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```

DBCC CHECKDB는 NO_INFOMSGS가 지정되었을 때 다음과 같은 결과 집합(메시지)을 반환합니다.
    
```
 The command(s) completed successfully.
 ```
 
DBCC CHECKDB는 PHYSICAL_ONLY가 지정되었을 때 다음 결과 집합을 반환합니다.
    
```
 DBCC results for 'model'.    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'master'.  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
 ```
 
DBCC CHECKDB는 ESTIMATEONLY가 지정되었을 때 다음 결과 집합을 반환합니다.
    
```
 Estimated TEMPDB space needed for CHECKALLOC (KB)    
    
 -------------------------------------------------  
    
 13   
    
 (1 row(s) affected)   
    
 Estimated TEMPDB space needed for CHECKTABLES (KB)    
    
 --------------------------------------------------    
    
 57 
    
 (1 row(s) affected)  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
    
## <a name="permissions"></a>Permissions    
sysadmin 고정 서버 역할의 멤버 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다.
    
## <a name="examples"></a>예    
    
### <a name="a-checking-both-the-current-and-another-database"></a>1. 현재 데이터베이스와 다른 데이터베이스 모두 검사    
다음 예에서는 현재 데이터베이스 및 `DBCC CHECKDB` 데이터베이스에 대해 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 실행합니다.
    
```sql    
-- Check the current database.    
DBCC CHECKDB;    
GO    
-- Check the AdventureWorks2012 database without nonclustered indexes.    
DBCC CHECKDB (AdventureWorks2012, NOINDEX);    
GO    
```    
    
### <a name="b-checking-the-current-database-suppressing-informational-messages"></a>2. 현재 데이터베이스 검사 후 정보 메시지를 표시하지 않음    
다음 예에서는 현재 데이터베이스를 검사하되 모든 정보 메시지를 표시하지 않습니다.
    
```sql    
DBCC CHECKDB WITH NO_INFOMSGS;    
GO    
```    
    
## <a name="see-also"></a>참고 항목    
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[데이터베이스 스냅숏 스파스 파일의 크기 보기&#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)  
[sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)  
[시스템 테이블 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  

