---
title: ALTER DATABASE 호환성 수준(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/18/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COMPATIBILITY_LEVEL_TSQL
- COMPATIBILITY_LEVEL
dev_langs:
- TSQL
helpviewer_keywords:
- 80 compatibility level
- ALTER DATABASE statement, compatibility levels
- 90 compatibility level
- compatibility levels [SQL Server]
- 100 compatibility level
- db compatibility level
- db compat level
ms.assetid: ca5fd220-d5ea-4182-8950-55d4101a86f6
caps.latest.revision: 89
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3bdc0c85068e4933b0c97cb508bd819ee1cc481d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="alter-database-transact-sql-compatibility-level"></a>ALTER DATABASE(Transact-SQL) 호환성 수준
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

특정 데이터베이스 동작이 지정된 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환되도록 설정합니다. 다른 ALTER DATABASE 옵션은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER DATABASE database_name   
SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 | 90 }  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 수정할 데이터베이스의 이름입니다.  
  
 COMPATIBILITY_LEVEL { 140 | 130 | 120 | 110 | 100 | 90 | 80 }  
 데이터베이스가 호환되도록 설정할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전입니다. 다음 호환성 수준 값을 구성할 수 있습니다.  
  
|Product|데이터베이스 엔진 버전|호환성 수준 지정|지원되는 호환성 수준 값|  
|-------------|-----------------------------|-------------------------------------|------------------------------------------|  
|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|14|140|140, 130, 120, 110, 100|
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|140, 130, 120, 110, 100|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130, 120, 110, 100|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120, 110, 100|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110, 100, 90|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100, 90, 80|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100, 90, 80|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|9|90|90, 80|  
|SQL Server 2000|8|80|80|  
  
> [!NOTE]  
> **2018년 1월** 기준으로 SQL Database에서 새로 만들어진 데이터베이스에 대한 기본 호환성 수준은 140입니다. 기존 데이터베이스에 대해서는 데이터베이스 호환성 수준을 업데이트하지 않습니다. 이것은 고객의 판단할 문제입니다. 최신 기능 향상을 활용할 수 있게 최신 호환성 수준으로 변경을 고려하는 것이 좋습니다.
> 
> 일반적으로 데이터베이스에 대해 수준 140을 원하지만 110 **카디널리티 추정** 알고리즘을 선호하는 이유가 있는 경우 [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 및 특히 해당 키워드 `LEGACY_CARDINALITY_ESTIMATION = ON`을 참조하세요.
>  
>  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 두 호환성 수준 간의 가장 중요한 쿼리의 성능 차이를 평가하는 방법에 대한 내용은 [Azure SQL Database에서 호환성 수준 130으로 향상된 쿼리 성능](http://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)을 참조하세요. 이 문서에서는 호환성 수준 130 및 SQL Server를 참조하나 SQL Server 및 Azure SQL DB에 대한 140으로 이동에도 같은 방법론이 적용됩니다.


 다음 쿼리를 실행하여 연결된 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 버전을 확인합니다.  
  
```sql  
SELECT SERVERPROPERTY('ProductVersion');  
```  
  
> [!NOTE]  
> 호환성 수준에 따라 달라지는 일부 기능은 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 지원되지 않습니다.  

 현재 호환성 수준을 확인하려면 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)의 **compatibility_level** 열을 쿼리합니다.  
  
```sql  
SELECT name, compatibility_level FROM sys.databases;  
```  
  
## <a name="remarks"></a>Remarks  
모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 경우 기본 호환성 수준은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 버전으로 설정됩니다. 데이터베이스는 **model** 데이터베이스의 호환성 수준이 이보다 낮지 않은 한 이 수준으로 설정됩니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 업그레이드할 때 데이터베이스의 호환성 수준이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 해당 인스턴스에 대해 허용된 최소 이상이면 기존 호환성 수준이 유지됩니다. 허용된 수준보다 낮은 호환성 수준으로 데이터베이스를 업그레이드하면 데이터베이스를 허용된 가장 낮은 호환성 수준으로 설정합니다. 이는 시스템 및 사용자 데이터베이스 모두에 적용됩니다. 데이터베이스의 호환성 수준을 변경하려면 **ALTER DATABASE**를 사용합니다. 데이터베이스의 현재 호환성 수준을 보려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰에서 **compatibility_level** 열을 쿼리합니다.  

> [!NOTE]  
> 이전 SQL Server 버전에서 만들어져 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM 또는 서비스 팩 1로 업그레이드되는 [배포 데이터베이스](../../relational-databases/replication/distribution-database.md)는 호환성 수준이 90이며 다른 데이터베이스에서 지원되지 않습니다. 복제 기능에는 영향을 미치지 않습니다. 이후의 서비스 팩 및 SQL Server 버전으로 업그레이드하면 **마스터** 데이터베이스의 수준에 맞게 배포 데이터베이스의 호환성 수준이 높아집니다.
  
## <a name="using-compatibility-level-for-backward-compatibility"></a>이전 버전과의 호환을 위해 호환성 수준 사용  
 호환성 수준은 전체 서버가 아닌 지정된 데이터베이스의 동작에만 적용됩니다. 호환성 수준은 부분적으로만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전과의 호환성을 제공합니다. 호환성 모드 130부터 기능에 영향을 주는 새로운 쿼리 계획이 새 호환성 모드에만 추가되었습니다. 쿼리 계획 변경으로 인해 성능 저하가 발생하는 업그레이드 중 위험을 최소화하기 위해 이를 수행했습니다. 응용 프로그램 관점에서 목표는 여전히 쿼리 최적화 프로그램 공간에서 수행된 성능 향상 뿐만 아니라 새로운 기능 중 일부를 상속하기 위해 최신 호환성 수준에 있지만 통제된 방법으로 이를 수행합니다. 중간 마이그레이션 도구로 호환성 수준을 사용하여 관련 호환성 수준 설정에서 제어하는 동작의 버전 차이를 해결할 수 있습니다. 자세한 내용은 문서의 뒷부분에서 업그레이드 모범 사례를 참조하세요.  
  
 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 응용 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전에서 동작 차이에 의해 영향을 받으면 응용 프로그램이 새로운 호환성 모드와 매끄럽게 작동되도록 변환합니다. 그런 다음, `ALTER DATABASE`를 사용하여 호환성 수준을 130으로 변경합니다. 데이터베이스에 대한 새로운 호환성 설정은 `USE <database>`가 발급되거나 기본 데이터베이스로 해당 데이터베이스를 사용하여 새 로그인이 처리될 때 적용됩니다.  
 
> [!IMPORTANT]
> 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 도입된 지원되지 않는 기능은 호환성 수준으로 보호되지 않습니다.
> 
> 예를 들어 `FASTFIRSTROW` 힌트는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 더 이상 사용되지 않으며 `OPTION (FAST n )` 힌트로 대체되었습니다. 데이터베이스 호환성 수준을 110으로 설정하면 지원되지 않는 힌트를 복원하지 않습니다.
> 지원되지 않는 기능에 대한 자세한 내용은 [SQL Server 2016에서 지원되지 않는 데이터베이스 엔진 기능](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md), [SQL Server 2014에서 지원되지 않는 데이터베이스 엔진 기능](http://msdn.microsoft.com/library/ms144262(v=sql.120)), [SQL Server 2012에서 지원되지 않는 데이터베이스 엔진 기능](http://msdn.microsoft.com/library/ms144262(v=sql.110)) 및 [SQL Server 2008에서 지원되지 않는 데이터베이스 엔진 기능](http://msdn.microsoft.com/library/ms144262(v=sql.100))을 참조하세요.

> [!IMPORTANT]
> 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 도입된 주요 변경 내용은 호환성 수준으로 보호되지 않을 **수 있습니다**. [!INCLUDE[tsql](../../includes/tsql-md.md)] 동작은 일반적으로 호환성 수준으로 보호됩니다. 그러나 변경되거나 제거된 시스템 개체는 호환성 수준으로 보호되지 **않습니다**.
>
> 호환성 수준으로 **보호되는** 주요 변경 내용의 예는 datetime에서 datetime2 데이터 형식으로의 암시적 변환입니다. 데이터베이스 호환성 수준 130에서 밀리초의 소수 부분을 고려하여 향상된 정확도를 보여 주므로 다르게 변환된 값을 생성합니다. 이전 변환 동작을 복원하려면 데이터베이스 호환성 수준을 120 이하로 설정합니다.
>
> 호환성 수준으로 **보호되지 않는** 주요 변경 내용의 예는 다음과 같습니다.
> -  시스템 개체의 변경된 열 이름입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 sys.dm_os_sys_info의 *single_pages_kb* 열 이름은 *pages_kb*로 변경되었습니다. 호환성 수준에 관계 없이 쿼리 `SELECT single_pages_kb FROM sys.dm_os_sys_info`는 오류 207(잘못된 열 이름)을 생성합니다.
> -  제거된 시스템 개체입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 `sp_dboption`이 제거되었습니다. 호환성 수준에 관계 없이 `EXEC sp_dboption 'AdventureWorks2016CTP3', 'autoshrink', 'FALSE';` 문은 오류 2812(저장된 프로시저 'sp_dboption'을 찾을 수 없음)를 생성합니다.
>
> 주요 변경 내용에 대한 자세한 내용은 [SQL Server 2017에서 데이터베이스 엔진 기능에 대한 주요 변경 내용](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2017.md), [SQL Server 2016에서 데이터베이스 엔진 기능에 대한 주요 변경 내용](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md), [SQL Server 2014에서 데이터베이스 엔진 기능에 대한 주요 변경 내용](http://msdn.microsoft.com/library/ms143179(v=sql.120)), [SQL Server 2012에서 데이터베이스 엔진 기능에 대한 주요 변경 내용](http://msdn.microsoft.com/library/ms143179(v=sql.110)) 및 [SQL Server 2008에서 데이터베이스 엔진 기능에 대한 주요 변경 내용](http://msdn.microsoft.com/library/ms143179(v=sql.100))을 참조하세요.
  
## <a name="best-practices"></a>최선의 구현 방법  
호환성 수준 업그레이드를 위해 권장되는 워크플로는 [데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)을 참조하세요.  
  
## <a name="compatibility-levels-and-stored-procedures"></a>호환성 수준 및 저장 프로시저  
 저장 프로시저가 실행될 때 저장 프로시저는 정의된 데이터베이스의 현재 호환성 수준을 사용합니다. 데이터베이스의 호환성 설정이 변경되면 모든 저장 프로시저도 그에 맞게 자동으로 다시 컴파일됩니다.  

## <a name="differences-between-compatibility-level-130-and-level-140"></a>호환성 수준 130과 수준 140 사이의 차이  
이 섹션에서는 호환성 수준 140으로 도입된 새로운 동작에 대해 설명합니다.

|호환성 수준 설정 130 이하|호환성 수준 설정 140|  
|--------------------------------------------------|-----------------------------------------|  
|다중 문 테이블 반환 함수를 참조하는 명령문에 대한 카디널리티 예상치는 고정된 행 추측을 사용합니다.|다중 문 테이블 반환 함수를 참조하는 적절한 명령문에 대한 카디널리티 예상치는 함수 출력의 실제 카디널리티를 사용합니다.  다중 문 테이블 반환 함수에 대한 **인터리브 실행**을 통해 활성화됩니다.|
|디스크에 대한 분산이 발생하는 부족한 메모리 부여 크기를 요청하는 일괄 처리 모드 쿼리는 연속 실행에 대한 문제가 지속될 수 있습니다.|디스크에 대한 분산이 발생하는 부족한 메모리 부여 크기를 요청하는 일괄 처리 모드 쿼리는 연속 실행에 대한 성능을 향상시킬 수 있습니다. 일괄 처리 모드 연산자에 대해 분산이 발생한 경우 캐시 계획의 메모리 부여 크기를 업데이트하는 **일괄 처리 모드 메모리 부여 피드백**을 통해 활성화됩니다. |
|동시성 문제가 발생하는 과도한 메모리 부여 크기를 요청하는 일괄 처리 모드 쿼리는 연속 실행에 대한 문제가 지속될 수 있습니다.|동시성 문제가 발생하는 과도한 메모리 부여 크기를 요청하는 일괄 처리 모드 쿼리는 연속 실행에 대한 동시성을 향상시킬 수 있습니다. 과도한 양이 요청된 경우 캐시 계획의 메모리 부여 크기를 업데이트하는 **일괄 처리 모드 메모리 부여 피드백**을 통해 활성화됩니다.|
|조인 연산자를 포함하는 일괄 처리 모드 쿼리는 중첩된 루프, 해시 조인 및 병합 조인을 포함하는 세 개의 물리적 조인 알고리즘에 적합합니다. 카디널리티 예측치가 조인 입력에 대해 잘못된 경우 부적절한 조인 알고리즘이 선택될 수 있습니다. 이 문제가 발생하는 경우 성능이 저하되고 부적절한 조인 알고리즘이 캐시 계획이 다시 컴파일될 때까지 사용 중으로 남아 있습니다.|**적응형 조인**이라는 추가 조인 연산자가 있습니다. 카디널리티 예측치가 외부 빌드 조인 입력에 대해 잘못된 경우 부적절한 조인 알고리즘이 선택될 수 있습니다. 이 문제가 발생하고 명령문이 적응형 조인에 대해 적합한 경우 더 작은 조인 입력에 중첩된 루프가 사용되고 다시 컴파일할 필요 없이 더 큰 조인 입력에 해시 조인이 동적으로 사용됩니다. |
|Columnstore 인덱스를 참조하는 간단한 계획은 일괄 처리 모드 실행에 적합하지 않습니다. |Columnstore 인덱스를 참조하는 간단한 계획은 일괄 처리 모드 실행에 적합한 계획을 위해 무시됩니다.|
|`sp_execute_external_script` UDX 연산자는 행 모드에서만 실행할 수 있습니다.|`sp_execute_external_script` UDX 연산자는 일괄 처리 모드 실행에 적합합니다.|  
|다중 문 TVF(테이블 반환 함수)는 인터리브 실행이 없습니다. |계획 품질을 개선하기 위한 다중 문 TVF에 대한 인터리브 실행 |

SQL Server 2017 이전의 SQL Server 이전 버전에서 추적 플래그 4199의 수정 사항이 이제 기본적으로 활성화됩니다. 호환성 모드 140 사용 추적 플래그 4199는 SQL Server 2017 이후에 릴리스되는 새로운 쿼리 최적화 프로그램 수정에 적용됩니다. 추적 플래그 4199에 대한 자세한 내용은 [추적 플래그 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199)를 참조하세요.  
  
## <a name="differences-between-compatibility-level-120-and-level-130"></a>호환성 수준 120과 수준 130 사이의 차이  
이 섹션에서는 호환성 수준 130으로 정의된 새로운 동작에 대해 설명합니다.   

|호환성 수준 설정 120 이하|호환성 수준 설정 130|  
|--------------------------------------------------|-----------------------------------------|  
|Insert select 문의 Insert는 단일 스레드입니다.|Insert select 문에서 Insert는 다중 스레드 형식이거나, 병렬 계획일 수 있습니다.|  
|메모리 최적화 테이블에 대한 쿼리는 단일 스레드를 실행합니다.|메모리 최적화 테이블에 대한 쿼리는 이제 병렬 계획을 가질 수 있습니다.|  
|SQL 2014 카디널리티 평가기 **CardinalityEstimationModelVersion="120"** 을 도입했습니다.|카디널리티 추정 모델 130을 통한 자세한 CE(카디널리티 추정) 개선 사항은 쿼리 계획에서 볼 수 있습니다. **CardinalityEstimationModelVersion="130"**|  
|Columnstore 인덱스가 있는 일괄 처리 모드와 행 모드 비교 변경 내용<br /><br /> Columnstore 인덱스가 있는 테이블에 대한 정렬은 행 모드에 있습니다.<br /><br /> Windowing 함수 집계는 `LAG` 또는 `LEAD`와 같은 행 모드에서 작동합니다.<br /><br /> 여러 고유 절이 있는 Columnstore 테이블에 대한 쿼리는 행 모드에서 작동했습니다.<br /><br /> MAXDOP 1에서 실행되거나 직렬 계획을 사용하는 쿼리는 행 모드에서 실행되었습니다. | Columnstore 인덱스가 있는 일괄 처리 모드와 행 모드 비교 변경 내용<br /><br /> Columnstore 인덱스가 있는 테이블에 대한 정렬은 이제 일괄 처리 모드에 있습니다.<br /><br /> Windowing 집계는 이제 `LAG` 또는 `LEAD`와 같은 일괄 처리 모드에서 작동합니다.<br /><br /> 여러 고유 절이 있는 Columnstore 테이블에 대한 쿼리는 일괄 처리 모드에서 작동합니다.<br /><br /> Maxdop1에서 실행되거나 직렬 계획을 사용하는 쿼리는 일괄 처리 모드에서 실행됩니다.|  
| 통계는 자동으로 업데이트될 수 있습니다. | 자동으로 통계를 업데이트하는 논리는 대형 테이블에 더 적극적입니다.  실제로 고객이 새로 삽입된 행이 빈번하게 쿼리되지만 통계가 해당 값을 포함하도록 업데이트되지 않는 쿼리에 대한 성능 문제를 발견하는 사례를 줄여야 합니다. |  
| 추적 2371은 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 기본적으로 OFF입니다. | [추적 2371](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/)은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 기본적으로 ON입니다. 추적 플래그 2371은 자동 통계 업데이트 도구에 매우 많은 행이 있는 테이블에서 더 작지만 현명한 행의 하위 집합을 샘플링하도록 알려 줍니다. <br/> <br/> 하나의 개선 사항은 최근에 삽입된 더 많은 행을 샘플에 포함하는 것입니다. <br/> <br/> 또 다른 개선 사항은 업데이트 통계 프로세스가 실행되는 동안 쿼리를 차단하기 보다는 쿼리가 실행되도록 두는 것입니다. |  
| 수준 120의 경우 통계는 *단일* 스레드 프로세스를 통해 샘플링됩니다. | 수준 130의 경우 통계는 *다중* 스레드 프로세스를 통해 샘플링됩니다. |  
| 253 들어오는 외래 키는 제한입니다. | 최대 10,000개의 들어오는 외래 키 또는 유사한 참조로 지정된 테이블을 참조할 수 있습니다. 제한 사항에 대해서는 [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md)를 참조하세요. |  
|사용되지 않는 MD2, MD4, MD5, SHA 및 SHA1 해시 알고리즘이 허용됩니다.|SHA2_256 및 SHA2_512 해시 알고리즘만 허용됩니다.|
||[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]는 일부 데이터 형식 변환 및 일부(주로 드문) 작업에서 향상된 기능을 포함합니다. 자세한 내용은 [일부 데이터 형식 및 일반적이지 않은 작업 처리 시 SQL Server 2016의 향상된 기능](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon)을 참조하세요.|
  
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이전 버전에서 추적 플래그 4199의 수정 사항이 이제 기본적으로 활성화됩니다. 호환성 모드 130 사용 추적 플래그 4199는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이후에 릴리스되는 새로운 쿼리 최적화 프로그램 수정에 적용됩니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 이전 쿼리 최적화 프로그램을 사용하려면 호환성 수준 110을 선택해야 합니다. 추적 플래그 4199에 대한 자세한 내용은 [추적 플래그 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199)를 참조하세요.  
  
## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>낮은 호환성 수준과 수준 120 사이의 차이  
 이 섹션에서는 호환성 수준 120으로 정의된 새로운 동작에 대해 설명합니다.  
  
|호환성 수준 설정 110 이하|호환성 수준 설정 120|  
|--------------------------------------------------|-----------------------------------------|  
|이전 쿼리 최적화 프로그램이 사용됩니다.|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]는 쿼리 계획을 만들고 최적화하는 구성 요소에 대한 향상된 기능을 포함합니다. 이러한 새로운 쿼리 최적화 프로그램 기능은 데이터베이스 호환성 수준 120의 사용에 따라 달라집니다. 이러한 향상된 기능을 활용하려면 데이터베이스 호환성 수준 120을 사용하여 새 데이터베이스 응용 프로그램을 개발해야 합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 마이그레이션된 응용 프로그램의 경우 좋은 성능이 유지되거나 향상되었는지 확인하려면 신중하게 테스트해야 합니다. 성능이 저하되면 데이터베이스 호환성 수준을 110 이하로 설정하여 이전 쿼리 최적화 프로그램 방법을 사용할 수 있습니다.<br /><br /> 데이터베이스 호환성 수준 120은 최신 데이터 웨어하우징 및 OLTP 작업에 대해 조정된 새로운 카디널리티 평가기를 사용합니다. 성능 문제 때문에 데이터베이스 호환성 수준을 110으로 설정하려면 먼저 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [데이터베이스 엔진의 새로운 기능](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md) 항목의 쿼리 계획 섹션에서 권장 사항을 참조하세요.|  
|120 미만의 호환성 수준에서는 **date** 값을 문자열 값으로 변환할 때 언어 설정이 무시됩니다. 이 동작은 **date** 유형에만 한정됩니다. 아래에 있는 예제 섹션에서 예제 B를 참조하세요.|**date** 값을 문자열 값으로 변환할 때 언어 설정이 무시되지 않습니다.|  
|`EXCEPT` 절의 오른쪽에 있는 재귀 참조는 무한 루프를 만듭니다. 아래 예제 섹션의 예제 C는 이 동작을 보여 줍니다.|`EXCEPT` 절에 있는 재귀 참조는 ANSI SQL 표준에 따라 오류를 생성합니다.|  
|재귀 CTE(공통 테이블 식)는 중복된 열 이름을 허용합니다.|재귀적 CTE에서 중복 열 이름을 허용하지 않습니다.|  
|해제된 트리거는 트리거가 변경되는 경우 설정됩니다.|트리거를 변경하는 경우 트리거의 상태(설정 또는 해제)가 변경되지 않습니다.|  
|OUTPUT INTO 테이블 절은 `IDENTITY_INSERT SETTING = OFF`를 무시하고 명시적 값이 삽입될 수 있도록 합니다.|`IDENTITY_INSERT`가 OFF로 설정되면 테이블의 ID 열에 명시적 값을 삽입할 수 없습니다.|  
|데이터베이스 포함이 부분으로 설정된 경우 `MERGE` 문의 `OUTPUT` 절에서 `$action` 필드의 유효성을 검사하면 데이터 정렬 오류가 반환될 수 있습니다.|`MERGE` 문의 `$action` 절에서 반환되는 값의 데이터 정렬은 서버 데이터 정렬 대신 데이터베이스 데이터 정렬이며 데이터 정렬 충돌 오류가 반환되지 않습니다.|  
|`SELECT INTO` 문은 항상 단일 스레드 삽입 작업을 만듭니다.|`SELECT INTO` 문은 병렬 삽입 작업을 만들 수 있습니다. 많은 수의 행을 삽입하는 경우 병렬 작업은 성능을 향상시킬 수 있습니다.|  
  
## <a name="differences-between-lower-compatibility-levels-and-levels-110-and-120"></a>낮은 호환성 수준과 수준 110 및 120 사이의 차이  
 이 섹션에서는 호환성 수준 110으로 정의된 새로운 동작에 대해 설명합니다.   이 섹션은 또한 수준 120에도 적용됩니다.  
  
|호환성 수준 설정 100 이하|호환성 수준 설정 110 이상|  
|--------------------------------------------------|--------------------------------------------------|  
|CLR(공용 언어 런타임) 데이터베이스 개체는 CLR 버전 4를 사용하여 실행됩니다. 그러나 CLR 버전 4에 도입된 일부 동작 변경은 발생하지 않습니다. 자세한 내용은 [CLR 통합의 새로운 기능](../../relational-databases/clr-integration/clr-integration-what-s-new.md)을 참조하세요.|CLR 데이터베이스 개체는 CLR 버전 4를 사용하여 실행됩니다.|  
|XQuery 함수 **string-length** 및 **substring**에서 각 서로게이트를 두 개의 문자로 계산합니다.|XQuery 함수 **string-length** 및 **substring**에서 각 서로게이트를 한 개의 문자로 계산합니다.|  
|`PIVOT`이 재귀 CTE(공통 테이블 식) 쿼리에서 허용됩니다. 그러나 그룹화당 여러 행이 있는 경우에는 쿼리에서 잘못된 결과가 반환됩니다.|`PIVOT`이 재귀 CTE(공통 테이블 식) 쿼리에서 허용되지 않습니다. 오류가 반환됩니다.|  
|RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.|RC4 또는 RC4_128를 사용하여 새 자료를 암호화할 수 없습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.|  
|**time** 및 **datetime2** 데이터 형식 중 하나가 계산 열 식에서 사용되는 경우를 제외하고 이러한 데이터 형식에 대한 `CAST` 및 `CONVERT` 연산의 기본 스타일이 121입니다. 계산 열의 경우 기본 스타일은 0입니다. 이 동작은 자동 매개 변수화와 관련된 쿼리에서 이러한 연산이 만들어지고 사용될 때 또는 제약 조건 정의에 사용될 때 계산 열에 영향을 줍니다.<br /><br /> 아래 예제 섹션의 예제 D는 스타일 0과 121의 차이점을 보여 줍니다. 위에서 설명한 동작은 보여 주지 않습니다. 날 짜 및 시간 스타일에 대한 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.|호환성 수준 110에서 **time** 및 **datetime2** 데이터 형식의 `CAST` 및 `CONVERT` 연산에 대한 기본 스타일은 항상 121입니다. 쿼리에 이전 동작이 적용되는 경우 110보다 낮은 호환성 수준을 사용하거나, 해당 쿼리에서 스타일 0을 명시적으로 지정해야 합니다.<br /><br /> 데이터베이스를 호환성 수준 110으로 업그레이드할 경우 디스크에 저장된 사용자 데이터는 변경되지 않습니다. 수동으로 이 데이터를 적절하게 수정해야 합니다. 예를 들어 `SELECT INTO`를 사용하여 위에서 설명한 계산 열 식이 포함된 원본에서 테이블을 만든 경우 계산 열 정의 자체가 아니라 스타일 0을 사용하는 데이터가 저장됩니다. 스타일 121과 일치하도록 이 데이터를 수동으로 업데이트해야 합니다.|  
|분할 뷰에서 참조되는 **smalldatetime** 형식의 원격 테이블 열은 **datetime**으로 매핑됩니다. 로컬 테이블의 해당 열(SELECT 목록의 동일한 서수 위치에 있는 열)은 **datetime** 형식이어야 합니다.|분할 뷰에서 참조되는 **smalldatetime** 형식의 원격 테이블 열은 **smalldatetime**으로 매핑됩니다. 로컬 테이블의 해당 열(SELECT 목록의 동일한 서수 위치에 있는 열)은 **smalldatetime** 형식이어야 합니다.<br /><br /> 110으로 업그레이드한 후에는 데이터 형식이 일치하지 않으므로 분산형 분할 뷰가 실패합니다. 원격 테이블의 데이터 형식을 **datetime**으로 변경하거나 로컬 데이터베이스의 호환성 수준을 100 이하로 설정하여 이 문제를 해결할 수 있습니다.|  
|`SOUNDEX` 함수는 다음 규칙을 구현합니다.<br /><br /> 1) `SOUNDEX` 코드에 동일한 숫자가 있는 두 개의 자음을 구분하는 경우 대문자 H 또는 대문자 W가 무시됩니다.<br /><br /> 2) `SOUNDEX` 코드에서 *character_expression*의 처음 2자에 같은 숫자가 있으면 두 문자 모두 포함됩니다. 위의 경우에 해당되지 않고 `SOUNDEX` 코드에서 나란히 있는 자음에 같은 값이 있으면 첫 번째 문자를 제외한 모든 문자가 제외됩니다.|`SOUNDEX` 함수는 다음 규칙을 구현합니다.<br /><br /> 1) 대문자 H 또는 대문자 W가 동일한 `SOUNDEX` 코드 숫자를 갖는 두 개의 자음을 구분하는 경우 오른쪽의 자음은 무시됩니다.<br /><br /> 2) `SOUNDEX` 코드에서 나란히 있는 자음에 같은 값이 있으면 첫 번째 문자를 제외한 모든 문자가 제외됩니다.<br /><br /> <br /><br /> 추가 규칙으로 인해 `SOUNDEX` 함수에서 계산된 값이 이전 호환성 수준에서 계산된 값과 다를 수 있습니다. 호환성 수준 110으로 업그레이드한 후 `SOUNDEX` 함수를 사용하는 인덱스, 힙 또는 CHECK 제약 조건을 다시 작성해야 할 수 있습니다. 자세한 내용은 [SOUNDEX&#40;Transact-SQL&#41;](../../t-sql/functions/soundex-transact-sql.md)를 참조하세요.|  
  
## <a name="differences-between-compatibility-level-90-and-level-100"></a>호환성 수준 90과 수준 100 사이의 차이  
 이 섹션에서는 호환성 수준 100으로 정의된 새로운 동작에 대해 설명합니다.  
  
|호환성 수준 설정 90|호환성 수준 설정 100|영향력|  
|----------------------------------------|-----------------------------------------|---------------------------|  
|세션 수준 설정과 상관없이 다중 문 테이블 반환 함수를 만든 경우 이 함수에 대해 QUOTED_IDENTIFER 설정은 항상 ON으로 설정됩니다.|다중 문 테이블 반환 함수를 만든 경우 QUOTED IDENTIFIER 세션 설정이 적용됩니다.|보통|  
|파티션 함수를 만들거나 바꾸면 언어 설정을 US_English로 가정하고 함수의 **datetime** 및 **smalldatetime** 리터럴을 평가합니다.|현재 언어 설정은 파티션 함수에서 **datetime** 및 **smalldatetime** 리터럴을 평가하는 데 사용됩니다.|보통|  
|`FOR BROWSE` 절이 `INSERT` 및 `SELECT INTO` 문에서 허용되고 무시됩니다.|`FOR BROWSE` 절이 `INSERT` 및 `SELECT INTO` 문에서 허용되지 않습니다.|보통|  
|전체 텍스트 조건자는 `OUTPUT` 절에서 허용됩니다.|전체 텍스트 조건자는 `OUTPUT` 절에서 허용되지 않습니다.|낮음|  
|`CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST` 및 `DROP FULLTEXT STOPLIST`는 지원되지 않습니다. 시스템 중지 목록은 자동으로 새로운 전체 텍스트 인덱스와 연결됩니다.|`CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST` 및 `DROP FULLTEXT STOPLIST`는 지원됩니다.|낮음|  
|`MERGE`는 예약 키워드가 아닙니다.|MERGE는 완전 예약 키워드입니다. `MERGE` 문은 호환성 수준 100 및 90 모두에서 지원됩니다.|낮음|  
|INSERT 문에서 \<dml_table_source> 인수를 사용하면 구문 오류가 발생합니다.|중첩된 INSERT, UPDATE, DELETE 또는 MERGE 문에서 OUTPUT 절의 결과를 캡처하고 그 결과를 대상 테이블이나 뷰에 삽입할 수 있습니다. 이 작업은 INSERT 문의 \<dml_table_source> 인수를 사용하여 수행됩니다.|낮음|
|`NOINDEX`가 지정되지 않으면 `DBCC CHECKDB` 또는 `DBCC CHECKTABLE`은 단일 테이블이나 인덱싱된 뷰 및 해당하는 모든 비클러스터형 XML 인덱스에 대해 물리적 일관성 검사와 논리적 일관성 검사를 모두 수행합니다. 공간 인덱스는 지원되지 않습니다.|`NOINDEX`가 지정되지 않으면 `DBCC CHECKDB` 또는 `DBCC CHECKTABLE`은 단일 테이블 및 해당하는 모든 비클러스터형 인덱스에 대해 물리적 일관성 검사와 논리적 일관성 검사를 모두 수행합니다. 그러나 XML 인덱스, 공간 인덱스 및 인덱싱된 뷰에 대해서는 기본적으로 물리적 일관성 검사만 수행됩니다.<br /><br /> `WITH EXTENDED_LOGICAL_CHECKS`를 지정하면 인덱싱된 뷰, XML 인덱스 및 공간 인덱스에 대해 논리적 검사가 수행됩니다. 기본적으로 물리적 일관성 검사는 논리적 일관성 검사 전에 수행됩니다. `NOINDEX`도 지정할 경우 논리적 검사만 수행됩니다.|낮음|  
|DML(데이터 조작 언어)로 OUTPUT 절을 사용하는 경우 문 실행 중에 런타임 오류가 발생하면 전체 트랜잭션이 종료되고 롤백됩니다.|DML(데이터 조작 언어) 문으로 `OUTPUT` 절을 사용하는 경우 명령문 실행 중에 런타임 오류가 발생하면 `SET XACT_ABORT` 설정에 따라 동작이 결정됩니다. `SET XACT_ABORT`가 OFF로 설정된 경우 `OUTPUT` 절을 사용하는 DML 문에서 문 중단 오류가 발생하면 해당 문은 종료되지만 일괄 처리의 실행이 계속되고 트랜잭션이 롤백되지 않습니다. `SET XACT_ABORT`가 ON으로 설정된 경우 OUTPUT 절을 사용하는 DML 문에서 런타임 오류가 발생하면 항상 일괄 처리가 종료되고 트랜잭션이 롤백됩니다.|낮음|  
|CUBE 및 ROLLUP은 예약 키워드가 아닙니다.|`CUBE` 및 `ROLLUP`은 GROUP BY 절에서 예약 키워드입니다.|낮음|  
|XML **anyType** 형식의 요소에는 엄격한 유효성 검사가 적용됩니다.|**anyType** 형식의 요소에는 엄격하지 않은 유효성 검사가 적용됩니다. 자세한 내용은 [와일드카드 구성 요소 및 콘텐츠 유효성 검사](../../relational-databases/xml/wildcard-components-and-content-validation.md)를 참조하세요.|낮음|  
|특수 특성 **xsi:nil** 및 **xsi:type**은 데이터 조작 언어 문으로 쿼리하거나 수정할 수 없습니다.<br /><br /> 즉, `/e/@*`에서 **xsi:nil** 및 **xsi:type** 특성을 무시하고 `/e/@xsi:nil`이 실패합니다. 그러나 `xsi:nil = "false"`인 경우에도 `SELECT xmlCol`과의 일관성을 위해 `/e`에서 **xsi:nil** 및 **xsi:type** 특성을 반환합니다.|특수 특성 **xsi:nil** 및 **xsi:type**은 일반 특성으로 저장되므로 쿼리 및 수정이 가능합니다.<br /><br /> 예를 들어 쿼리 `SELECT x.query('a/b/@*')`를 실행하면 **xsi:nil** 및 **xsi:type**을 포함하는 모든 특성이 반환됩니다. 쿼리에서 이러한 유형을 제외하려면 `@*`를 `@*[namespace-uri(.) != "`*insert xsi namespace uri*`"`로 바꿉니다. `(local-name(.) = "type"` 또는 `local-name(.) ="nil".`로는 바꾸지 마십시오.|낮음|  
|XML 상수 문자열 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime 형식으로 변환하는 사용자 정의 함수를 결정적 함수로 표시합니다.|XML 상수 문자열 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime 형식으로 변환하는 사용자 정의 함수를 비결정적 함수로 표시합니다.|낮음|  
|XML union 및 list 형식 중 일부는 지원되지 않습니다.|다음 기능을 포함하여 union 및 list 형식은 모두 지원됩니다.<br /><br /> 목록의 합집합<br /><br /> 합집합의 합집합<br /><br /> 원자성 유형의 목록<br /><br /> 합집합의 목록|낮음|  
|인라인 테이블 반환 함수 또는 뷰에 xQuery 메서드가 포함된 경우 이 메서드에 필요한 SET 옵션의 유효성을 검사하지 않습니다.|인라인 테이블 반환 함수 또는 뷰에 xQuery 메서드가 포함된 경우 이 메서드에 필요한 SET 옵션의 유효성을 검사합니다. 메서드의 SET 옵션을 잘못 설정하면 오류가 발생합니다.|낮음|  
|줄 끝 문자(캐리지 리턴 및 줄 바꿈)를 포함하는 XML 특성 값은 XML 표준에 따라 정규화되지 않습니다. 즉, 하나의 줄 바꿈 문자 대신 두 문자 모두 반환됩니다.|줄 끝 문자(캐리지 리턴 및 줄 바꿈)를 포함하는 XML 특성 값은 XML 표준에 따라 정규화됩니다. 즉, 문서 엔터티를 포함하여 구문 분석된 외부 엔터티의 모든 줄 바꿈은 2자 시퀀스 #xD #xA 및 뒤에 #xA가 오지 않는 #xD 모두를 하나의 #xA 문자로 변환하여 입력에서 정규화됩니다.<br /><br /> 특성을 사용하여 줄 끝 문자를 포함하는 문자열 값을 변환하는 응용 프로그램은 이러한 제출된 문자를 다시 수신하지 않습니다. 정규화 프로세스를 방지하려면 XML 숫자 문자 엔터티를 사용하여 모든 줄 끝 문자를 인코딩합니다.|낮음|  
|열 속성 `ROWGUIDCOL` 및 `IDENTITY`는 제약 조건으로 잘못 이름이 지정될 수 있습니다. 예를 들어 `CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)` 문은 실행되긴 하지만 제약 조건 이름이 보존되지 않으며 이를 통해 사용자에게 액세스할 수 없습니다.|열 속성 `ROWGUIDCOL` 및 `IDENTITY`는 제약 조건으로 이름을 지정할 수 없습니다. 오류 156이 반환됩니다.|낮음|  
|`UPDATE T1 SET @v = column_name = <expression>`과 같은 양방향 할당을 사용하여 열을 업데이트하면 문 실행 중에 `WHER`E 및 `ON` 절과 같은 다른 절에서 문의 시작 값 대신 변수의 현재 값을 사용할 수 있으므로 예상치 못한 결과가 발생할 수 있습니다. 그 결과 각 행에서 조건자의 의미가 예기치 않게 변경될 수 있습니다.<br /><br /> 이 동작은 호환성 수준이 90으로 설정된 경우에만 발생합니다.|양방향 할당을 사용하여 열을 업데이트하면 문 실행 중에 열의 문 시작 값만 액세스되므로 예상대로 결과가 나타납니다.|낮음|  
|아래 예제 섹션의 예제 E를 참조하세요.|아래 예제 섹션의 예제 F를 참조하세요.|낮음|  
|ODBC 함수 {fn CONVERT()}는 언어의 기본 날짜 형식을 사용합니다. 일부 언어에서 기본 형식은 YDM입니다. 이 경우 CONVERT()가 YMD 형식을 사용하는 `{fn CURDATE()}`와 같은 다른 함수와 결합되면 변환 오류가 발생합니다.|ODBC 함수 `{fn CONVERT()}`는 ODBC 데이터 형식 SQL_TIMESTAMP, SQL_DATE, SQL_TIME, SQLDATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP로 변환할 때 스타일 121(언어와 상관없는 YMD 형식)을 사용합니다.|낮음|  
|DATEPART와 같은 datetime 내장 함수에서 문자열 입력 값은 유효한 datetime 리터럴이 아니어도 됩니다. 예를 들어 `SELECT DATEPART (year, '2007/05-30')`는 성공적으로 컴파일됩니다.|`DATEPART`와 같은 datetime 내장 함수에서 문자열 입력 값은 유효한 datetime 리터럴이어야 합니다. 유효하지 않은 datetime 리터럴을 사용하면 오류 241이 반환됩니다.|낮음|  
  
## <a name="reserved-keywords"></a>예약 키워드  
 호환성 설정은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 예약되는 키워드도 결정합니다. 다음 표에서는 각 호환성 수준에 의해 정의된 예약 키워드를 보여 줍니다.  
  
|호환성 수준 설정|예약 키워드|  
|----------------------------------|-----------------------|  
|130|결정될 예정입니다.|  
|120|없음|  
|110|WITHIN GROUP, TRY_CONVERT, SEMANTICKEYPHRASETABLE, SEMANTICSIMILARITYDETAILSTABLE, SEMANTICSIMILARITYTABLE|  
|100|CUBE, MERGE, ROLLUP|  
|90|EXTERNAL, PIVOT, UNPIVOT, REVERT, TABLESAMPLE|  
  
 지정된 호환성 수준의 예약 키워드에는 해당 수준 또는 그 아래 수준에서 정의된 모든 키워드가 포함됩니다. 따라서 수준이 110인 응용 프로그램의 경우에는 위 표에 나열된 모든 키워드가 예약되어 있습니다. 더 낮은 호환성 수준에서 수준이 100인 키워드는 유효한 개체 이름으로 유지되지만 해당 키워드에 대한 수준이 110인 언어 기능은 사용할 수 없습니다.  
  
 정의된 키워드는 예약된 상태로 유지됩니다. 예를 들어 호환성 수준 90에서 정의된 예약 키워드 PIVOT은 수준 100, 110 및 120에서도 예약되어 있습니다.  
  
 응용 프로그램이 호환성 수준에 대한 키워드로 예약되어 있는 식별자를 사용할 경우 제대로 실행되지 않습니다. 이러한 문제를 해결하려면 식별자를 대괄호(**[]**)나 따옴표(**""**)로 묶으십시오. 예를 들어 식별자**EXTERNAL**을 사용하는 응용 프로그램을 호환성 수준 90으로 업그레이드하려면 식별자를 **[EXTERNAL]** 이나 **"EXTERNAL"** 로 변경할 수 있습니다.  
  
 자세한 내용은 [예약된 키워드&#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-compatibility-level"></a>1. 호환성 수준 변경  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 호환성 수준을 `110,`[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)](으)로 변경합니다.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 110;  
GO  
```  
  
 다음 예에서는 현재 데이터베이스의 호환성 수준을 반환합니다.  
  
```sql  
SELECT name, compatibility_level   
FROM sys.databases   
WHERE name = db_name();  
```  
  
### <a name="b-ignoring--the-set-language-statement-except-under-compatibility-level-120"></a>2. 호환성 수준이 120 미만일 때를 제외하고 SET LANGUAGE 문을 무시합니다.  
 다음 쿼리에서는 호환성 수준이 120 미만일 때를 제외하고 SET LANGUAGE 문을 무시합니다.  
  
```sql  
SET DATEFORMAT dmy;   
DECLARE @t2 date = '12/5/2011' ;  
SET LANGUAGE dutch;   
SELECT CONVERT(varchar(11), @t2, 106);   
  
-- Results when the compatibility level is less than 120.   
12 May 2011   
  
-- Results when the compatibility level is set to 120).  
12 mei 2011  
```  
  
### <a name="c"></a>3.  
 110 이하의 호환성 수준 설정의 경우 EXCEPT 절의 오른쪽에 있는 재귀 참조는 무한 루프를 만듭니다.  
  
```sql  
WITH   
cte AS (SELECT * FROM (VALUES (1),(2),(3)) v (a)),  
r   
AS (SELECT a FROM Table1  
UNION ALL  
(SELECT a FROM Table1 EXCEPT SELECT a FROM r) )   
SELECT a   
FROM r;  
  
```  
  
### <a name="d"></a>4.  
 이 예에서는 스타일 0과 스타일 121의 차이점을 보여 줍니다. 날 짜 및 시간 스타일에 대한 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.  
  
```sql  
CREATE TABLE t1 (c1 time(7), c2 datetime2);   
  
INSERT t1 (c1,c2) VALUES (GETDATE(), GETDATE());  
  
SELECT CONVERT(nvarchar(16),c1,0) AS TimeStyle0  
       ,CONVERT(nvarchar(16),c1,121)AS TimeStyle121  
       ,CONVERT(nvarchar(32),c2,0) AS Datetime2Style0  
       ,CONVERT(nvarchar(32),c2,121)AS Datetime2Style121  
FROM t1;  
  
-- Returns values such as the following.  
TimeStyle0       TimeStyle121       
Datetime2Style0      Datetime2Style121  
---------------- ----------------   
-------------------- --------------------------  
3:15PM           15:15:35.8100000   
Jun  7 2011  3:15PM  2011-06-07 15:15:35.8130000  
```  
  
### <a name="e"></a>5.  
 최상위 UNION 연산자가 포함된 문에 변수를 할당할 수 있지만 예상치 않은 결과가 반환됩니다. 예를 들어 다음 문에서 지역 변수 `@v`에는 두 테이블의 합집합의 열 `BusinessEntityID` 값이 할당됩니다. 원래 SELECT 문에서 둘 이상의 값을 반환하면 반환된 값 중 마지막 값이 변수에 할당됩니다. 이 경우 변수에 마지막 값이 올바르게 할당되지만 SELECT UNION 문의 결과 집합도 함께 반환됩니다.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET compatibility_level = 90;  
GO  
USE AdventureWorks2012;  
GO  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM HumanResources.Employee  
UNION ALL  
SELECT @v = BusinessEntityID FROM HumanResources.EmployeeAddress;  
SELECT @v;  
```  
  
### <a name="f"></a>6.  
 최상위 UNION 연산자가 포함된 문에는 변수를 할당할 수 없습니다. 오류 10734가 반환됩니다. 오류를 해결하려면 다음 예와 같이 쿼리를 다시 작성합니다.  
  
```sql  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM   
    (SELECT BusinessEntityID FROM HumanResources.Employee  
     UNION ALL  
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;  
SELECT @v;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [예약 키워드&#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
 [데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 
  
