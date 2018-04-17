---
title: ALTER DATABASE(Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: 37
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ddec688efe7ce468b7af1c05389b9cc1e86cf4c4
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]을 수정합니다. 데이터베이스의 이름과 데이터베이스의 버전 및 서비스 목표를 변경하고, 탄력적 풀을 조인하고, 데이터베이스 옵션을 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name }  
{  
    MODIFY NAME = new_database_name  
  | MODIFY ( <edition_options> [, ... n] ) 
  | SET { <option_spec> [ ,... n ] } 
  | ADD SECONDARY ON SERVER <partner_server_name>  
    [WITH ( <add-secondary-option>::= [, ... n] ) ]  
  | REMOVE SECONDARY ON SERVER <partner_server_name>  
  | FAILOVER  
  | FORCE_FAILOVER_ALLOW_DATA_LOSS  
}  
[;] 

<edition_options> ::= 
{  

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }  
  | EDITION = { 'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical'} 
  | SERVICE_OBJECTIVE = 
       {  <service-objective>
       | { ELASTIC_POOL (name = <elastic_pool_name>) } 
       } 
}  

<add-secondary-option> ::=  
   {  
      ALLOW_CONNECTIONS = { ALL | NO }  
     | SERVICE_OBJECTIVE = 
       {  <service-objective> 
       | { ELASTIC_POOL ( name = <elastic_pool_name>) } 
       } 
   }  

<service-objective> ::=  { 'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |
       | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' 
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 
      }

```  
  
```
-- SET OPTIONS AVAILABLE FOR SQL Database  
-- Full descriptions of the set options are available in the topic 
-- ALTER DATABASE SET Options. The supported syntax is listed here.  

<option_spec> ::= 
{  
    <auto_option> 
  | <change_tracking_option> 
  | <cursor_option> 
  | <db_encryption_option>  
  | <db_update_option> 
  | <db_user_access_option> 
  | <delayed_durability_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <snapshot_option>  
  | <sql_option> 
  | <target_recovery_time_option> 
  | <termination>  
  | <temporal_history_retention>  
}  
  
<auto_option> ::= 
{  
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] } 
  | AUTO_SHRINK { ON | OFF } 
  | AUTO_UPDATE_STATISTICS { ON | OFF } 
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  

<change_tracking_option> ::=  
{  
  CHANGE_TRACKING 
   { 
       = OFF  
     | = ON [ ( <change_tracking_option_list > [,...n] ) ] 
     | ( <change_tracking_option_list> [,...n] )  
   }  
}  

   <change_tracking_option_list> ::=  
   {  
       AUTO_CLEANUP = { ON | OFF } 
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }  
   }  

<cursor_option> ::= 
{  
    CURSOR_CLOSE_ON_COMMIT { ON | OFF } 
}  
  
<db_encryption_option> ::=  
  ENCRYPTION { ON | OFF }  
  
<db_update_option> ::=  
  { READ_ONLY | READ_WRITE }  
  
<db_user_access_option> ::=  
  { RESTRICTED_USER | MULTI_USER }  
  
<delayed_durability_option> ::=  DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
<parameterization_option> ::=  
  PARAMETERIZATION { SIMPLE | FORCED }  
  
<query_store_options> ::=  
{  
  QUERY_STORE 
  {  
    = OFF 
    | = ON [ ( <query_store_option_list> [,... n] ) ]  
    | ( < query_store_option_list> [,... n] )  
    | CLEAR [ ALL ]  
  }  
} 
  
<query_store_option_list> ::=  
{  
  OPERATION_MODE = { READ_WRITE | READ_ONLY } 
  | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )  
  | DATA_FLUSH_INTERVAL_SECONDS = number 
  | MAX_STORAGE_SIZE_MB = number 
  | INTERVAL_LENGTH_MINUTES = number 
  | SIZE_BASED_CLEANUP_MODE = [ AUTO | OFF ]  
  | QUERY_CAPTURE_MODE = [ ALL | AUTO | NONE ]  
  | MAX_PLANS_PER_QUERY = number  
}  
  
<snapshot_option> ::=  
{  
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT {ON | OFF }  
}  
<sql_option> ::= 
{  
    ANSI_NULL_DEFAULT { ON | OFF }   
  | ANSI_NULLS { ON | OFF }   
  | ANSI_PADDING { ON | OFF }   
  | ANSI_WARNINGS { ON | OFF }   
  | ARITHABORT { ON | OFF }   
  | COMPATIBILITY_LEVEL = { 100 | 110 | 120 | 130 | 140 }  
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}  
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  

<temporal_history_retention>  ::=  TEMPORAL_HISTORY_RETENTION { ON | OFF }
```  
  
 설정 옵션의 전체 설명은 [ALTER DATABASE SET 옵션(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md) 및 [ALTER DATABASE 호환성 수준(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
## <a name="arguments"></a>인수  

*database_name*  

수정할 데이터베이스의 이름입니다.  
  
CURRENT  

현재 사용 중인 데이터베이스를 변경하도록 지정합니다.  
  
MODIFY NAME **=***new_database_name*  

데이터베이스의 이름을 지정된 이름 *new_database_name*으로 바꿉니다. 다음 예에서는 `db1` 데이터베이스의 이름을 `db2`로 변경합니다.   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

MODIFY (EDITION **=** ['basic' | 'standard' | 'premium' |'GeneralPurpose' | 'BusinessCritical'])    

데이터베이스의 서비스 계층을 변경합니다. ‘Premiumrs’에 대한 지원이 제거되었습니다. 질문에 대해서는, 이메일 별칭(premium-rs@microsoft.com)을 사용하세요.

다음 예제에서는 버전을 `premium`으로 변경합니다.
  
```  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

데이터베이스의 MAXSIZE 속성이 해당 버전에서 지원되는 유효 범위 밖의 값으로 설정되면 EDITION 변경이 실패합니다.  

MODIFY (MAXSIZE **=** [100 MB | 500 MB | 1 | 1024…4096] GB)  

데이터베이스의 최대 크기를 지정합니다. 최대 크기는 데이터베이스의 EDITION 속성에 대한 유효한 값 집합을 따라야 합니다. 데이터베이스의 최대 크기를 변경하면 데이터베이스 EDITION이 변경될 수 있습니다. 다음 표에서는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서비스 계층에 대해 지원되는 MAXSIZE 값 및 기본값(D)을 보여 줍니다.  
  
**DTU 기반 모델**

|**MAXSIZE**|**기본**|**S0-S2**|**S3-S12**|**P1-P6**|**P11-P15**|  
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|  
|100MB|√|√|√|√|√|  
|250MB|√|√|√|√|√|  
|500MB|√|√|√|√|√|  
|1GB|√|√|√|√|√|  
|2GB|√ (D)|√|√|√|√|  
|5GB|해당 사항 없음|√|√|√|√|  
|10GB|해당 사항 없음|√|√|√|√|  
|20GB|해당 사항 없음|√|√|√|√|  
|30GB|해당 사항 없음|√|√|√|√|  
|40GB|해당 사항 없음|√|√|√|√|  
|50GB|해당 사항 없음|√|√|√|√|  
|100GB|해당 사항 없음|√|√|√|√|  
|150GB|해당 사항 없음|√|√|√|√|  
|200GB|해당 사항 없음|√|√|√|√|  
|250GB|해당 사항 없음|√ (D)|√ (D)|√|√|  
|300GB|해당 사항 없음|√|√|√|√|  
|400GB|해당 사항 없음|√|√|√|√|  
|500GB|해당 사항 없음|√|√|√ (D)|√|  
|750GB|해당 사항 없음|√|√|√|√|  
|1024GB|해당 사항 없음|√|√|√|√ (D)|  
|1024GB에서 최대 4096GB(256 GB*로 증분)|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|√|√|  
  
\* P11과 P15는 기본 크기인 1024를 사용하여 MAXSIZE를 최대 4TB까지 허용합니다.  P11 및 P15는 추가 비용없이 최대 4TB가 포함된 저장소를 사용할 수 있습니다. 프리미엄 계층에서 1TB 초과의 MAXSIZE는 현재 미국 동부2, 미국 서부, 미국 버지니아 주 정부, 서부 유럽, 독일 중앙, 동남 아시아, 일본 동부, 오스트레일리아 동부, 캐나다 중앙 및 캐나다 동부에서 사용할 수 있습니다. DTU 기반 모델에 대한 리소스 제한에 대한 자세한 내용은 [DTU 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요.  

DTU 기반 모델에 대한 MAXSIZE 값은 지정된 경우 지정된 서비스 계층에 대한 위의 표에 표시된 유효한 값이어야 합니다.
 
**vCore 기반 모델**

**범용 서비스 계층**

|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_4|GP_Gen4_8|GP_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|최대 데이터 크기(GB)|1024|1024|1536|3072|4096|

**중요 비즈니스용 서비스 계층**

|성능 수준|BC_Gen4_1|BC_Gen4_2|BC_Gen4_4|BC_Gen4_8|BC_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|최대 데이터 크기(GB)|1024|1024|1536|2048|2048|

vCore 모델을 사용할 때 `MAXSIZE`값이 설정되지 않은 경우 기본값은 32GB입니다. vCore 기반 모델에 대한 리소스 제한에 대한 자세한 내용은 [vCore 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요.
  
MAXSIZE 및 EDITION 인수에는 다음과 같은 규칙이 적용됩니다.  
  
- EDITION이 지정되었지만 MAXSIZE가 지정되지 않은 경우 해당 버전에 대한 기본값이 사용됩니다. 예를 들어 EDITION이 Standard로 설정되었고 MAXSIZE가 지정되지 않았으면 MAXSIZE가 자동으로 500 MB로 설정됩니다.  
  
- MAXSIZE 또는 EDITION이 모두 지정되지 않았으면 EDITION이 Standard(S0)로 설정되고, MAXSIZE는 250GB로 설정됩니다.  

MODIFY (SERVICE_OBJECTIVE = \<service-objective>)  

성능 수준을 지정합니다. 다음 예제에서는 프리미엄 데이터베이스의 서비스 목표를 `P6`으로 변경합니다.
 
```sql  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  

성능 수준을 지정합니다. 서비스 목표에 사용 가능한 값은 `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16`입니다. 

서비스 목표 설명과 크기, 버전 및 서비스 목표 조합 등의 정보에 대한 자세한 내용은 [Azure SQL Database 서비스 계층 및 성능 수준](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) 및 [DTU 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) 및 [vCore 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요. PRS 서비스 목표에 대한 지원이 제거되었습니다. 질문에 대해서는, 이메일 별칭(premium-rs@microsoft.com)을 사용하세요. 
  
MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>)  

탄력적 풀에 기존 데이터베이스를 추가하려면 데이터베이스의 SERVICE_OBJECTIVE를 ELASTIC_POOL로 설정하고 탄력적 풀의 이름을 입력합니다. 동일한 서버 내의 다른 탄력적 풀에 데이터베이스를 변경하려면 이 옵션을 사용할 수도 있습니다. 자세한 내용은 [SQL Database 탄력적 풀 만들기 및 관리](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)를 참조하세요. 탄력적 풀에서 데이터베이스를 제거하려면 ALTER DATABASE를 사용하여 SERVICE_OBJECTIVE를 단일 데이터베이스 성능 수준으로 설정합니다.  

ADD SECONDARY ON SERVER \<partner_server_name>  

파트너 서버에 동일한 이름의 지역 복제 보조 데이터베이스를 만들고, 지역 복제 주 데이터베이스에 로컬 데이터베이스를 만들고, 주 데이터베이스에서 새 보조 데이터베이스에 데이터를 비동기적으로 복제하기 시작합니다. 동일한 이름의 데이터베이스가 보조 데이터베이스에 이미 있으면 명령이 실패합니다. 이 명령은 주가 되는 로컬 데이터베이스를 호스팅하는 서버의 master 데이터베이스에서 실행됩니다.  
  
WITH ALLOW_CONNECTIONS { **ALL** | NO }  

ALLOW_CONNECTIONS를 지정하지 않으면 기본적으로 ALL로 설정됩니다. ALL로 설정된 경우 연결할 적절한 권한이 있는 모든 로그인을 허용하는 읽기 전용 데이터베이스입니다.  
  
WITH SERVICE_OBJECTIVE {  `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16` }  

SERVICE_OBJECTIVE를 지정하지 않으면 보조 데이터베이스가 주 데이터베이스와 동일한 서비스 수준에서 생성됩니다. SERVICE_OBJECTIVE를 지정하면 보조 데이터베이스가 지정된 수준에서 생성됩니다. 이 옵션은 보다 저렴한 서비스 수준에서 지역 복제된 보조 데이터베이스를 만들도록 지원합니다. 지정된 SERVICE_OBJECTIVE를 소스와 동일한 버전 내에 있어야 합니다. 예를 들어 버전이 프리미엄인 경우 S0를 지정할 수 없습니다.  
  
ELASTIC_POOL (name = \<elastic_pool_name)  

ELASTIC_POOL을 지정하지 않으면 보조 데이터베이스는 탄력적인 풀에서 생성되지 않습니다. ELASTIC_POOL을 지정하면 보조 데이터베이스는 탄력적인 풀에서 생성됩니다.  
  
> [!IMPORTANT]  
>  ADD SECONDARY 명령을 실행하는 사용자는 주 서버에서 DBManager이고, 로컬 데이터베이스에서 db_owner 멤버 자격과 보조 서버에서 DBManager 멤버 자격이 있어야 합니다.  
  
REMOVE SECONDARY ON SERVER  \<partner_server_name>  

지정된 서버에서 지정되고 지역 복제된 보조 데이터베이스를 제거합니다. 이 명령은 주 데이터베이스를 호스팅하는 서버의 master 데이터베이스에서 실행됩니다.  
  
> [!IMPORTANT]  
>  REMOVE SECONDARY 명령을 실행하는 사용자는 주 서버에서 DBManager여야 합니다.  
  
FAILOVER  

지역 복제 파트너 자격에서 보조 데이터베이스를 승격합니다. 여기서 명령을 실행하여 주 데이터베이스가 되고 현재 주 데이터베이스를 새 보조 데이터베이스로 강등시킵니다. 이 과정의 일환으로 지역 복제 모드를 일시적으로 비동기 모드에서 동기 모드로 전환합니다. 장애 조치 과정 중:  
  
1.  주 데이터베이스는 새 트랜잭션 사용을 중지합니다.  
  
2.  모든 대기 중인 트랜잭션은 보조 데이터베이스에 플러시됩니다.  
  
3.  보조 데이터베이스는 주 데이터베이스가 되고, 이전 주 데이터베이스/새 보조 데이터베이스에서 비동기 지역 복제를 시작합니다.  
  
이 시퀀스는 데이터 손실이 발생하지 않게 합니다. 두 데이터베이스를 사용할 수 없는 기간은 역할이 전환되는 동안의 0~25초 순서입니다. 전체 작업은 1분 넘게 걸리지 않아야 합니다. 주 데이터베이스를 사용할 수 없는 경우 이 명령을 실행할 때 주 데이터베이스를 사용할 수 없다는 오류 메시지를 표시하며 명령이 실패합니다. 장애 조치 프로세스가 완료되지 않고 중단된 경우 강제 장애 조치 명령을 사용하여 데이터 손실을 허용할 수 있습니다. 그런 다음, 손실 데이터를 복구해야 하는 경우 DevOps(CSS)를 호출하여 손실 데이터를 복구합니다.  
  
> [!IMPORTANT]  
>  FAILOVER 명령을 실행하는 사용자는 주 서버와 보조 서버 모두에서 DBManager여야 합니다.  
  
FORCE_FAILOVER_ALLOW_DATA_LOSS  

지역 복제 파트너 자격에서 보조 데이터베이스를 승격합니다. 여기서 명령을 실행하여 주 데이터베이스가 되고 현재 주 데이터베이스를 새 보조 데이터베이스로 강등시킵니다. 현재 주 데이터베이스를 더 이상 사용할 수 없는 경우에만 이 명령을 사용합니다. 가용성을 복원하는 것이 중요한 경우에 재해 복구 전용으로 설계되어 일부 데이터 손실을 허용 가능합니다.  
  
강제 장애 조치(failover) 중:  
  
1. 지정된 보조 데이터베이스는 즉시 주 데이터베이스가 되고 새 트랜잭션을 허용하기 시작합니다.  
  
2. 원래 주 데이터베이스가 새 주 데이터베이스와 다시 연결될 수 있는 경우 원래 주 데이터베이스에서 증분 백업이 수행되고 원래 주 데이터베이스는 새 보조 데이터베이스가 됩니다.  
  
3. 이전 주 데이터베이스의 이 증분 백업으로부터 데이터를 복구하기 위해 사용자는 DevOps/CSS를 사용합니다.  
  
4. 추가 보조 데이터베이스가 있는 경우 새 주 데이터베이스의 보조 데이터베이스가 되도록 자동으로 재구성됩니다. 이 프로세스는 비동기적이며 이 프로세스가 완료될 때까지 지연될 수 있습니다. 재구성이 완료될 때까지 보조 데이터베이스는 여전히 이전 기본 데이터베이스의 보조 데이터베이스입니다.  
  
> [!IMPORTANT]  
>  FORCE_FAILOVER_ALLOW_DATA_LOSS 명령을 실행하는 사용자는 주 서버와 보조 서버에서 DBManager여야 합니다.  
  
## <a name="remarks"></a>Remarks  

데이터베이스를 제거하려면 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)를 사용합니다.  
데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)를 사용합니다.  
  
ALTER DATABASE 문은 자동 커밋 모드(기본 트랜잭션 관리 모드)에서 실행되어야 하며 명시적 또는 암시적 트랜잭션에서는 허용되지 않습니다.  
  
계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "데이터베이스 유지 관리 또는 재구성 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.  
  
프로시저 캐시는 다음 시나리오에도 플러시됩니다.  
  
- 데이터베이스에서 AUTO_CLOSE 데이터베이스 옵션이 ON으로 설정되어 있습니다. 사용자 연결이 데이터베이스를 참조하거나 사용하지 않으면 백그라운드 작업에서 자동으로 데이터베이스를 닫고 종료하려고 합니다.  
  
- 기본 옵션이 있는 데이터베이스에 대해 여러 가지 쿼리를 실행합니다. 그러면 데이터베이스가 삭제됩니다.  
  
- 데이터베이스에 대한 트랜잭션 로그를 성공적으로 다시 작성합니다.  
  
- 데이터베이스 백업을 복원합니다.  
  
- 데이터베이스를 분리합니다.  
  
## <a name="viewing-database-information"></a>데이터베이스 정보 보기  

카탈로그 뷰, 시스템 함수 및 시스템 저장 프로시저를 사용하여 데이터베이스, 파일 및 파일 그룹에 대한 정보를 반환할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  

프로비전 프로세스를 통해 만들어진 서버 수준의 보안 주체 로그인 또는 `dbmanager` 데이터베이스 역할의 구성원만 데이터베이스를 변경할 수 있습니다.  
  
> [!IMPORTANT]  
>  데이터베이스의 소유자가 `dbmanager` 역할의 구성원인 경우 데이터베이스를 변경할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-check-the-edition-options-and-change-them"></a>1. 버전 옵션을 확인하고 변경합니다.

```sql
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>2. 다른 탄력적 풀에 데이터베이스 이동  

기존 데이터베이스를 pool1이라는 풀로 이동합니다.  
  
```sql  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>3. 지역 복제 보조 데이터베이스 추가  

로컬 서버에 있는 db1의 `secondaryserver` 서버에서 읽기 가능한 보조 데이터베이스 db1을 만듭니다.  
  
```sql  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = ALL )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>4. 지역 복제 보조 데이터베이스 제거  
 
`secondaryserver` 서버에서 보조 데이터베이스 db1을 제거합니다.  
  
```sql  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>5. 지역 복제 보조 데이터베이스로 장애 조치  

`secondaryserver` 서버에서 실행될 때 `secondaryserver` 서버에서 보조 데이터베이스 db1을 승격하여 새로운 주 데이터베이스를 만듭니다.  
  
```sql  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>관련 항목:
  
[CREATE DATABASE - Azure SQL Database](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [시스템 데이터베이스](../../relational-databases/databases/system-databases.md)  
  
  
