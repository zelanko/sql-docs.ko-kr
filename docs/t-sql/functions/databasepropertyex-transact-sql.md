---
description: DATABASEPROPERTYEX(Transact-SQL)
title: DATABASEPROPERTYEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATABASEPROPERTYEX
- DATABASEPROPERTYEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DATABASEPROPERTYEX function
- displaying database properties
- database properties [SQL Server]
ms.assetid: 8a9e0ffb-28b5-4640-95b2-a54e3e5ad941
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f269a6bc94c1685d9d91f280614348bf0a203020
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478744"
---
# <a name="databasepropertyex-transact-sql"></a>DATABASEPROPERTYEX(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 지정된 데이터베이스에 대해 지정된 데이터베이스 옵션이나 속성의 현재 설정을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DATABASEPROPERTYEX ( database , property )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*database*  
`DATABASEPROPERTYEX`에서 명명된 속성 정보를 반환할 데이터베이스의 이름을 나타내는 식입니다. *database* 에는 **nvarchar(128)** 데이터 형식이 있습니다.  

[!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서는 `DATABASEPROPERTYEX`에 현재 데이터베이스의 이름을 반환합니다. 다른 데이터베이스 이름을 제공하는 경우 모든 속성에 대해 NULL을 반환합니다.
  
*property*  
반환할 데이터베이스 속성의 이름을 나타내는 식입니다. *property* 에는 **varchar(128)** 데이터 형식이 있고, 이 표의 값 중 하나가 지원됩니다.
  
> [!NOTE]  
>  데이터베이스가 아직 시작되지 않은 경우 `DATABASEPROPERTYEX`가 메타데이터에서 검색하는 대신 직접 데이터베이스 액세스를 통해 이러한 값을 검색할 경우 `DATABASEPROPERTYEX`에서 NULL을 반환합니다. AUTO_CLOSE가 ON으로 설정되어 있거나 오프라인 상태인 데이터베이스는 '시작되지 않은 것'으로 간주됩니다.  
  
|속성|Description|반환 값|  
|---|---|---|
|데이터 정렬|데이터베이스의 기본 데이터 정렬 이름입니다.|데이터 정렬 이름<br /><br /> NULL: 데이터베이스가 시작되지 않음<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|ComparisonStyle|데이터 정렬의 Windows 비교 스타일입니다. 다음 스타일 값을 사용하여 완성된 ComparisonStyle 값에 대한 비트맵을 빌드합니다.<br /><br /> 대/소문자 무시: 1<br /><br /> 악센트 무시: 2<br /><br /> 일본어 가나 무시: 65536<br /><br /> 전자/반자 무시: 131072<br /><br /> <br /><br /> 예를 들어 기본값 196609는 대/소문자 무시, 일본어 가나 무시 및 전자/반자 무시 옵션이 결합된 결과입니다.|비교 스타일을 반환합니다.<br /><br /> 모든 이진 데이터 정렬에 대해 0을 반환합니다.<br /><br /> 기본 데이터 형식: **int**|  
|버전|데이터베이스 버전 또는 서비스 계층입니다.|**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]<br /><br /> <br /><br /> 범용<br /><br /> 중요 비즈니스용<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium<br /><br /> 시스템(master 데이터베이스용)<br /><br /> NULL: 데이터베이스가 시작되지 않음<br /><br /> 기본 데이터 형식: **nvarchar(64)**|  
|IsAnsiNullDefault|데이터베이스가 Null 값 허용에 대해 ISO 규칙을 따릅니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsAnsiNullsEnabled|Null에 대한 모든 비교는 알 수 없음이 됩니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsAnsiPaddingEnabled|비교 또는 삽입하기 전에 문자열이 동일한 길이만큼 채워집니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsAnsiWarningsEnabled|표준 오류 조건이 발생하면 SQL Server에서 오류 메시지나 경고 메시지를 표시합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsArithmeticAbortEnabled|쿼리 실행 시 오버플로나 0으로 나누기 오류가 발생하면 쿼리가 종료됩니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsAutoClose|마지막 사용자가 끝낸 후 데이터베이스가 완전히 종료되고 리소스가 해제됩니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsAutoCreateStatistics|쿼리 최적화 프로그램에서 필요할 경우 단일 열 통계를 작성하여 쿼리 성능을 향상시킵니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsAutoCreateStatisticsIncremental|가능하면 자동으로 만든 단일 열 통계는 증분합니다.|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsAutoShrink|데이터베이스 파일을 주기적으로 자동 축소합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsAutoUpdateStatistics|쿼리에서 오래된 기존 통계를 사용할 경우 쿼리 최적화 프로그램이 이러한 통계를 업데이트합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 입력이 잘못됨<br /><br /> 기본 데이터 형식: **int**|
|IsClone|데이터베이스는 DBCC CLONEDATABASE로 만든 사용자 데이터베이스의 스키마 및 통계 전용 복사본입니다. 자세한 내용은 [Microsoft 지원 아티클](https://support.microsoft.com/help/3177838)을 참조하세요.|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 이상.<br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**| 
|IsCloseCursorsOnCommitEnabled|트랜잭션이 커밋되면 열려 있는 모든 커서가 닫힙니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsFulltextEnabled|데이터베이스에 전체 텍스트 및 의미 체계 인덱싱을 사용하도록 설정되어 있습니다.|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> <br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 입력이 잘못됨<br /><br /> 기본 데이터 형식: **int**<br /><br /> **참고:** 이 속성의 값은 이제 아무런 영향을 주지 않습니다. 사용자 데이터베이스는 전체 텍스트 검색을 사용하도록 항상 설정됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 릴리스에서는 이 속성이 제거될 예정입니다. 새 개발 작업에서는 이 속성을 사용하지 말고 현재 이 속성을 사용하는 애플리케이션은 가능한 한 빨리 수정하세요.|  
|IsInStandBy|데이터베이스가 로그 복원이 허용된 읽기 전용으로 온라인 상태입니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsLocalCursorsDefault|커서는 기본적으로 LOCAL로 선언됩니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsMemoryOptimizedElevateToSnapshotEnabled|메모리 액세스에 최적화된 테이블은 세션 설정 TRANSACTION ISOLATION LEVEL이 READ COMMITTED, READ UNCOMMITTED 또는 낮은 격리 수준으로 설정된 경우 SNAPSHOT 격리를 사용하여 액세스됩니다.|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> <br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> 기본 데이터 형식: **int**|  
|IsMergePublished|복제가 설치된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스의 테이블을 병합 복제용으로 게시하도록 지원합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsNullConcat|Null 연결 피연산자가 NULL을 반환합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsNumericRoundAbortEnabled|식의 전체 자릿수에서 일부가 손실되면 오류가 발생합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsParameterizationForced|PARAMETERIZATION 데이터베이스 SET 옵션이 FORCED입니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력|  
|IsQuotedIdentifiersEnabled|식별자에 큰따옴표를 사용할 수 있습니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsPublished|복제가 설치된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 테이블을 스냅샷 또는 트랜잭션 복제용으로 게시하도록 지원합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsRecursiveTriggersEnabled|트리거를 재귀적으로 실행하도록 설정합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsSubscribed|데이터베이스가 게시를 구독합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsSyncWithBackup|데이터베이스는 게시된 데이터베이스이거나 배포 데이터베이스이며, 트랜잭션 복제를 중단하지 않는 복원을 지원합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**|  
|IsTornPageDetectionEnabled|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 정전이나 기타 시스템 중단으로 인해 완료되지 않은 I/O 작업을 검색합니다.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**| 
|IsVerifiedClone|데이터베이스는 DBCC CLONEDATABASE의 WITH VERIFY_CLONEDB 옵션을 사용하여 만든 사용자 데이터베이스의 스키마 및 통계 전용 복사본입니다. 자세한 내용은 이 [Microsoft 지원 아티클](https://support.microsoft.com/help/3177838)을 참조하세요.|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2부터 시작<br /><br /> <br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **int**| 
|IsXTPSupported|데이터베이스가 In-Memory OLTP, 즉, 메모리 최적화 테이블과 고유하게 컴파일된 모듈을 만들고 사용하는 것을 지원하는지 여부를 나타냅니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에만 해당 :<br /><br /> IsXTPSupported는 In-Memory OLTP 개체를 만드는 데 필요한 MEMORY_OPTIMIZED_DATA 파일 그룹의 존재 여부와 관계가 없습니다.|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> 1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL: 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않음<br /><br /> 기본 데이터 형식: **int**|  
|LastGoodCheckDbTime|지정된 데이터베이스에서 성공적으로 실행된 마지막 DBCC CHECKDB의 시간 및 날짜입니다.<sup>1</sup> DBCC CHECKDB가 데이터베이스에서 실행되지 않은 경우 1900-01-01 00:00:00.000이 반환됩니다.|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2부터</br>[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] CU9부터</br>[!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 이상</br>Azure SQL Database.<br/><br/>datetime 값<br /><br /> NULL: 잘못된 입력<br /><br /> 기본 데이터 형식: **datetime**| 
|LCID|데이터 정렬의 Windows LCID(로캘 ID)입니다.|LCID 값(10진수 형식)입니다.<br /><br /> 기본 데이터 형식: **int**|  
|MaxSizeInBytes|최대 데이터베이스 크기(바이트)입니다.|**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]<br /><br />[Azure SQL Database 및 Azure Synapse Analytics](/azure/sql-database/sql-database-single-database-scale#dtu-based-purchasing-model) – 추가 스토리지를 구매하지 않으면 값은 SLO를 기반으로 합니다.<br /><br />[vCore](/azure/sql-database/sql-database-single-database-scale#vcore-based-purchasing-model) – 값은 최대 크기까지 1GB씩 증가합니다.<br /><br />NULL: 데이터베이스가 시작되지 않음<br /><br /> 기본 데이터 형식: **bigint**|  
|복구|데이터베이스 복구 모델|FULL: 전체 복구 모델<br /><br /> BULK_LOGGED: 대량 로그 모델<br /><br /> SIMPLE: 단순 복구 모델<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|ServiceObjective|[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 또는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 데이터베이스 성능 수준을 설명합니다.|다음 중 하나<br /><br /> Null: 데이터베이스가 시작되지 않았습니다.<br /><br /> 공유(Web/Business 버전)<br /><br /> Basic<br /><br /> S0<br /><br /> S1<br /><br /> S2<br /><br /> S3<br /><br /> P1<br /><br /> P2<br /><br /> P3<br /><br /> ElasticPool<br /><br /> 시스템(master DB용)<br /><br /> 기본 데이터 형식: **nvarchar(32)**|  
|ServiceObjectiveId|[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]의 서비스 목표 ID입니다.|서비스 목표를 식별하는 **uniqueidentifier** 입니다.|  
|SQLSortOrder|이전 버전의 SQL Server에서 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 정렬 순서 ID입니다.|0: 데이터베이스가 Windows 데이터 정렬을 사용함<br /><br /> >0: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 정렬 순서 ID<br /><br /> NULL: 입력이 잘못되었거나 데이터베이스가 시작되지 않음<br /><br /> 기본 데이터 형식: **tinyint**|  
|상태|데이터베이스 상태입니다.|ONLINE: 쿼리에서 데이터베이스를 제공합니다.<br /><br /> **참고:** 데이터베이스가 열려 있고 아직 복구되지 않았을 때는 함수가 ONLINE 상태를 반환할 수 있습니다. ONLINE 데이터베이스가 연결을 허용할 수 있는지 파악하려면 **DATABASEPROPERTYEX** 의 데이터 정렬 속성을 쿼리합니다. 데이터베이스 데이터 정렬이 null이 아닌 값을 반환하면 ONLINE 데이터베이스가 연결을 허용할 수 있습니다. Always On 데이터베이스의 경우 `sys.dm_hadr_database_replica_states`의 database_state 또는 database_state_desc 열을 쿼리합니다.<br /><br /> OFFLINE: 데이터베이스가 명시적으로 오프라인 상태입니다.<br /><br /> RESTORING: 데이터베이스 복원이 시작되었습니다.<br /><br /> RECOVERING: 데이터베이스 복구가 시작되었고 데이터베이스가 아직 쿼리에 대해 준비되지 않았습니다.<br /><br /> SUSPECT: 데이터베이스가 복구되지 않았습니다.<br /><br /> EMERGENCY: 데이터베이스가 응급 읽기 전용 상태입니다. sysadmin 멤버만 액세스할 수 있습니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|Updateability|데이터 수정 가능 여부를 나타냅니다.|READ_ONLY: 데이터베이스가 데이터 읽기를 지원하지만 데이터 수정은 지원하지 않습니다.<br /><br /> READ_WRITE: 데이터베이스가 데이터 읽기 및 수정을 지원합니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|UserAccess|데이터베이스에 액세스할 수 있는 사용자를 나타냅니다.|SINGLE_USER: 한 번에 한 명의 db_owner, dbcreator 또는 sysadmin 사용자만 액세스할 수 있습니다.<br /><br /> RESTRICTED_USER: db_owner, dbcreator 또는 sysadmin 역할의 멤버만 액세스할 수 있습니다.<br /><br /> MULTI_USER: 모든 사용자가 액세스할 수 있습니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|버전|데이터베이스가 만들어진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드의 내부 버전 번호입니다. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|버전 번호: 데이터베이스가 열려 있습니다.<br /><br /> NULL: 데이터베이스가 시작되지 않았습니다.<br /><br /> 기본 데이터 형식: **int**| 

<br/>   

> [!NOTE]  
> <sup>1</sup> 가용성 그룹의 일부인 데이터베이스의 경우 `LastGoodCheckDbTime`은 명령을 실행하는 복제본에 관계 없이 주 복제본에서 성공적으로 실행된 마지막 DBCC CHECKDB의 시간과 날짜를 반환합니다. 

## <a name="return-types"></a>반환 형식
**sql_variant**
  
## <a name="exceptions"></a>예외  
오류가 발생하거나 호출자에게 개체를 볼 수 있는 권한이 없으면 NULL을 반환합니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자는 소유하고 있거나 사용 권한을 부여받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자에게 개체에 대한 권한이 없으면 `OBJECT_ID`와 같은 메타데이터 내보내기 기본 제공 함수에서 NULL을 반환할 수 있습니다. 자세한 내용은 [메타데이터 표시 유형 구성](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.
  
## <a name="remarks"></a>설명  
`DATABASEPROPERTYEX`는 한 번에 하나의 속성 설정만 반환합니다. 여러 속성 설정을 표시하려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰를 사용하세요.
  
## <a name="examples"></a>예제  
  
### <a name="a-retrieving-the-status-of-the-auto_shrink-database-option"></a>A. AUTO_SHRINK 데이터베이스 옵션의 상태 검색  
이 예에서는 `AdventureWorks` 데이터베이스에 대한 AUTO_SHRINK 데이터베이스 옵션의 상태를 반환합니다.
  
```sql
SELECT DATABASEPROPERTYEX('AdventureWorks2014', 'IsAutoShrink');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)] 이것은 AUTO_SHRINK가 해제되었음을 의미합니다.
  
```
------------------  
0  
```  
  
### <a name="b-retrieving-the-default-collation-for-a-database"></a>B. 데이터베이스의 기본 데이터 정렬 검색  
이 예에서는 `AdventureWorks` 데이터베이스의 여러 속성을 반환합니다.
  
```sql
SELECT   
    DATABASEPROPERTYEX('AdventureWorks2014', 'Collation') AS Collation,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'Edition') AS Edition,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'ServiceObjective') AS ServiceObjective,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'MaxSizeInBytes') AS MaxSizeInBytes  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Collation                     Edition        ServiceObjective  MaxSizeInBytes  
----------------------------  -------------  ----------------  --------------  
SQL_Latin1_General_CP1_CI_AS  DataWarehouse  DW1000            5368709120  
```  
  
## <a name="see-also"></a>참고 항목
[ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[데이터베이스 상태](../../relational-databases/databases/database-states.md)  
[sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)
  
  
