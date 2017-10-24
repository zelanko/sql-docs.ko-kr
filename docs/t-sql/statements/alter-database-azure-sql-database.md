---
title: "ALTER DATABASE (Azure SQL 데이터베이스) | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 09/25/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: 37
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: f525c0ca01f49be05c1920897951059b126c83e9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/30/2017

---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE (Azure SQL 데이터베이스)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  수정 된 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다. 데이터베이스, 탄력적 풀, 조인 및 데이터베이스 옵션을 설정 하는 데이터베이스, 버전 및 서비스 목표의 이름을 변경합니다.  
  
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
    | EDITION = { 'basic' | 'standard' | 'premium' | 'premiumrs' }   
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
                 | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15' | 
                 | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' | }

```  
  
```
-- SET OPTIONS AVAILABLE FOR SQL Database  
-- Full descriptions of the set options are available in the topic   
-- ALTER DATABASE SET Options. The supported syntax is listed here.  

<optionspec> ::=   
{  
    <auto_option>   
  | <compatibility_level_option>  
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
  
<compatibility_level_option>::=  
COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 }  
  
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
  
<delayed_durability_option> ::=    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
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
  | COMPATIBILITY_LEVEL = { 90 | 100 | 110 | 120}  
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
  
 Set 옵션의 전체 설명은 참조 하세요. [ALTER DATABASE SET 옵션 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) 및 [ALTER DATABASE 호환성 수준 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="arguments"></a>인수  
 *database_name*  
 수정할 데이터베이스의 이름입니다.  
  
 CURRENT  
 현재 사용 중인 데이터베이스를 변경하도록 지정합니다.  
  
 MODIFY NAME  **=**  *new_database_name*  
 로 지정 된 이름의 데이터베이스를 이름을 바꿉니다. *new_database_name*합니다. 다음 예에서는 데이터베이스의 이름을 변경 `db1` 를 `db2`:   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

 수정 (버전  **=**  ['기본' | '표준' | '프리미엄' | premiumrs'])    
 데이터베이스의 서비스 계층을 변경합니다. 다음 예에서는 변경 버전으로 `premium`:
  
```  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

버전 변경이 데이터베이스의 MAXSIZE 속성이 해당 버전에서 지 원하는 올바른 범위를 벗어난 값으로 설정 되어 있으면 실패 합니다.  

 수정 (MAXSIZE  **=**  [100MB | 500MB | 1 | 1024... 4096] GB)  
 데이터베이스의 최대 크기를 지정합니다. 최대 크기는 데이터베이스의 EDITION 속성에 대한 유효한 값 집합을 따라야 합니다. 데이터베이스의 최대 크기를 변경하면 데이터베이스 EDITION이 변경될 수 있습니다. 다음 표에서는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서비스 계층에 대해 지원되는 MAXSIZE 값 및 기본값(D)을 보여 줍니다.  
  
|**MAXSIZE**|**Basic**|**S0 S2**|**S3 S12**|**P1 P6 및 PRS1 PRS6**|**P11 P15**|  
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
|750 GB|해당 사항 없음|√|√|√|√|  
|1024GB|해당 사항 없음|√|√|√|√ (D)|  
|1024GB에서 최대 4, 096 GB 단위로 256 GB *|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|√|√|  
  
 \*P11 및 P15 허용 MAXSIZE 최대 4TB 1024GB 기본 크기 되 고 사용 합니다.  P11 및 P15 추가 비용 없이 최대 4TB의 포함 된 저장소를 사용할 수 있습니다. 프리미엄 계층에서 1TB 보다 큰 최대 크기는 현재 다음 지역에서 사용할 수 있습니다: 미국 East2, 미국 서 부, 미국 정부 기관용 버지니아, 서 부 유럽, 독일 중앙, 동남 아시아, 일본 동부, 오스트레일리아 동부, 중앙 캐나다 및 캐나다 동부 합니다. 현재 제한 사항에 대 한 참조 [데이터베이스를 단일](https://docs.microsoft.com/azure/sql-database-single-database-resources)합니다.  

  
 MAXSIZE 및 EDITION 인수에는 다음과 같은 규칙이 적용됩니다.  
  
-   MAXSIZE 값을 지정 하는 경우 위의 표에 표시 된 유효한 값이 되도록에 있습니다.  
  
-   EDITION이 지정되었지만 MAXSIZE가 지정되지 않은 경우 해당 버전에 대한 기본값이 사용됩니다. 예를 들어 EDITION이 Standard로 설정되었고 MAXSIZE가 지정되지 않았으면 MAXSIZE가 자동으로 500 MB로 설정됩니다.  
  
-   MAXSIZE 또는 EDITION이 모두를 지정 EDITION 표준 (S0)로 설정 되 고 MAXSIZE는 250GB를 설정 됩니다.  
 

 수정 (SERVICE_OBJECTIVE = \<서비스 목표 >)  
 성능 수준을 지정합니다. 다음 예제에서는 변경 내용에 premium 데이터베이스의 서비스 `P6`:
 
```  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  
 서비스 목표에 대 한 사용 가능한 값은: `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `PRS1`, `PRS2`, `PRS4`, 및 `PRS6`합니다. 서비스 목표 설명과 크기, 버전 및 서비스 목표 조합에 대 한 자세한 내용은 [Azure SQL 데이터베이스 서비스 계층 및 성능 수준](http://msdn.microsoft.com/library/azure/dn741336.aspx)합니다. 지정 된 SERVICE_OBJECTIVE 버전에서 지원 되지 않는 경우 오류가 발생 합니다. SERVICE_OBJECTIVE 값을 한 계층에서 다른 계층으로 변경하려면(예: S1에서 P1로 변경), EDITION 값도 변경해야 합니다.  
  
 수정 (SERVICE_OBJECTIVE 탄력적인 =\_풀 (이름 = \<elastic_pool_name >)  
 기존 데이터베이스를 탄력적인 풀에 추가 하려면 데이터베이스의 SERVICE_OBJECTIVE ELASTIC_POOL로 설정 하 고 탄력적 풀의 이름을 제공 합니다. 동일한 서버 내에서 다른 탄력적인 풀에 데이터베이스를 변경 하려면이 옵션을 사용할 수도 있습니다. 자세한 내용은 참조 [만들기 및 SQL 데이터베이스 탄력적 풀 관리](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)합니다. 탄력적 풀에서 데이터베이스를 제거 하는 SERVICE_OBJECTIVE 단일 데이터베이스 성능 수준으로 설정 하려면 ALTER DATABASE를 사용 합니다.  

 보조에 서버 추가 \<partner_server_name >  
 파트너 서버에 로컬 데이터베이스에 지리적 복제, 주에 같은 이름의 지리적 복제 보조 데이터베이스를 만들고 주 데이터베이스에서 새 보조 복제본에 데이터를 비동기적으로 복제를 시작 합니다. 동일한 이름의 데이터베이스가 보조 데이터베이스에 이미 있으면 명령이 실패 합니다. 이 명령은 주 되는 로컬 데이터베이스를 호스팅하는 서버의 master 데이터베이스에서 실행 됩니다.  
  
 ALLOW_CONNECTIONS와 {모든 | **아니요** }  
 ALLOW_CONNECTIONS를 지정 하지 않으면 기본적으로 NO로 설정 됩니다. 모두에 설정 된 경우 연결 하는 데 적절 한 권한이 있는 모든 로그인을 허용 하는 읽기 전용 데이터베이스입니다.  
  
 SERVICE_OBJECTIVE와 {'S0' | 'S1' | 'S 2' | ' S3 "| 'S4' | 'S6' | 'S7' | 'S9' | 'S12' | 'P1' | 'P 2' | 'P4' | 'P6' | 'P11' | 'P15' | 'PRS1' | 'PRS2' | 'PRS4' | PRS6'}  
 SERVICE_OBJECTIVE를 지정 하지 않으면 보조 데이터베이스가 주 데이터베이스와 같은 서비스 수준에서 생성 됩니다. SERVICE_OBJECTIVE를 지정 하면 보조 데이터베이스는 지정된 된 수준에서 생성 됩니다. 이 옵션 보다 저렴 서비스 수준이 있는 지리적 복제 보조를 만들 수 있도록 지원 합니다. 지정 된 SERVICE_OBJECTIVE를 소스로 같은 버전 내에 있어야 합니다. 예를 들어 버전은 premium 경우 S0를 지정할 수 없습니다.  
  
 ELASTIC_POOL (이름 = \<elastic_pool_name)  
 ELASTIC_POOL를 지정 하지 않으면 보조 데이터베이스는 탄력적인 풀의 만들어지지 않습니다. ELASTIC_POOL 지정 된 경우 보조 데이터베이스는 지정된 된 풀에서 생성 됩니다.  
  
> [!IMPORTANT]  
>  보조 추가 명령을 실행 하는 사용자 해야 주 서버에서 DBManager 수, 보조 서버에서 DBManager 로컬 데이터베이스의 db_owner 구성원을가지고 있어야 합니다.  
  
 보조 ON SERVER 제거 \<partner_server_name >  
 지정된 된 지리적 복제 보조 데이터베이스에서 지정된 된 서버를 제거합니다. 이 명령은 주 데이터베이스를 호스팅하는 서버의 master 데이터베이스에서 실행 됩니다.  
  
> [!IMPORTANT]  
>  보조 제거 명령을 실행 하는 사용자는 주 서버에서 DBManager 이어야 합니다.  
  
 FAILOVER  
 이 명령은 주 서버로 실행 되 고 새 보조 데이터베이스를 현재 주 복제본을 보조로 강등 지리적 복제 파트너 관계에 보조 데이터베이스를 수준을 올립니다. 이 과정의 일환으로, 지리적 복제 모드를 일시적으로 비동기 모드에서 동기 모드로 전환 됩니다. 장애 조치 과정:  
  
1.  주 라인 새 트랜잭션을 중지 합니다.  
  
2.  모든 보류 중인 트랜잭션이 보조 복제본에 플러시됩니다.  
  
3.  보조 데이터베이스는 주 되며를 이전 기본 비동기 지리적 복제를 시작 / 새 보조 데이터베이스입니다.  
  
 이 시퀀스는 데이터 손실은 발생 하지 않습니다 확인 합니다. 두 데이터베이스를 사용할 수 없는 기간은 0-25 초는 역할이 전환 된 동안입니다. 작업을 총 1 분 정도 더 이상 수행 해야 합니다. 주 데이터베이스를 사용할 수 없는 경우이 명령을 실행 하는 경우 주 데이터베이스를 사용할 수 없다는 나타내는 오류 메시지와 함께 명령이 실패 합니다. 장애 조치 프로세스가 완료 되지 않으면 눌려 경우 강제 장애 조치 명령을 사용할 수 및-데이터 손실 허용 있으며 손실 된 데이터를 복구 해야 하는 경우 devops 손실 된 데이터를 복구 하려면 (CSS)이 호출 다음.  
  
> [!IMPORTANT]  
>  장애 조치 명령은 실행 하는 사용자는 주 서버와 보조 서버에서 DBManager 이어야 합니다.  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 이 명령은 주 서버로 실행 되 고 새 보조 데이터베이스를 현재 주 복제본을 보조로 강등 지리적 복제 파트너 관계에 보조 데이터베이스를 수준을 올립니다. 현재 주 복제본을 더 이상 사용할 수 있는 경우에이 명령을 사용 합니다. 재해 복구용 으로만 가용성을 복원 하는 것은 중요 하 고 일부 데이터 손실이 허용 되는 설계 되었습니다.  
  
 강제 장애 조치 중:  
  
1.  지정된 된 보조 데이터베이스는 즉시 주 데이터베이스가 됩니다 및 승인을 새 트랜잭션을 시작 합니다.  
  
2.  원래 주 새 주 서버와 다시 연결할 수 있습니다, 증분 백업이 주, 원본에서 수행 되 고 원래 주 새 보조 데이터베이스 됩니다.  
  
3.  이전 주 서버에서이 증분 백업에서 데이터를 복구 하려면 사용자는 devops/CSS를 예약 합니다.  
  
4.  추가 보조 데이터베이스에 있는 경우는 새 주 데이터베이스의 보조 데이터베이스를 자동으로 재구성 됩니다. 이 프로세스는 비동기적 있으며이 프로세스가 완료 될 때까지 지연 수 있습니다. 재구성이 완료 되 면 될 때까지 보조 서버의 계속 이전 기본의 보조 복제본을 수 있습니다.  
  
> [!IMPORTANT]  
>  FORCE_FAILOVER_ALLOW_DATA_LOSS 명령을 실행 하는 사용자는 주 서버와 보조 서버에서 DBManager 이어야 합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여 데이터베이스를 제거 하려면 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)합니다.  
  
 사용 하 여 데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)합니다.  
  
 ALTER DATABASE 문은 자동 커밋 모드(기본 트랜잭션 관리 모드)에서 실행되어야 하며 명시적 또는 암시적 트랜잭션에서는 허용되지 않습니다.  
  
 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "데이터베이스 유지 관리 또는 재구성 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.  
  
 프로시저 캐시는 다음 시나리오에도 플러시됩니다.  
  
-   데이터베이스에서 AUTO_CLOSE 데이터베이스 옵션이 ON으로 설정되어 있습니다. 사용자 연결이 데이터베이스를 참조하거나 사용하지 않으면 백그라운드 작업에서 자동으로 데이터베이스를 닫고 종료하려고 합니다.  
  
-   기본 옵션이 있는 데이터베이스에 대해 여러 가지 쿼리를 실행합니다. 그러면 데이터베이스가 삭제됩니다.  
  
-   데이터베이스에 대한 트랜잭션 로그를 성공적으로 다시 작성합니다.  
  
-   데이터베이스 백업을 복원합니다.  
  
-   데이터베이스를 분리합니다.  
  
## <a name="viewing-database-information"></a>데이터베이스 정보 보기  
 카탈로그 뷰, 시스템 함수 및 시스템 저장 프로시저를 사용하여 데이터베이스, 파일 및 파일 그룹에 대한 정보를 반환할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 프로비전 프로세스를 통해 만들어진 서버 수준의 보안 주체 로그인 또는 `dbmanager` 데이터베이스 역할의 구성원만 데이터베이스를 변경할 수 있습니다.  
  
> [!IMPORTANT]  
>  데이터베이스의 소유자가 `dbmanager` 역할의 구성원인 경우 데이터베이스를 변경할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-check-the-edition-options-and-change-them"></a>1. 버전 옵션을 확인 하 고 변경 합니다.

```
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>2. 다른 탄력적 풀에 데이터베이스를 이동  
 기존 데이터베이스 풀 1 이라는 풀으로 이동 합니다.  
  
```  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>3. 지리적 복제 보조를 추가 합니다.  
 서버에 db1 읽을 수 없는 보조 데이터베이스를 만듭니다. `secondaryserver` 로컬 서버에서 d b 1의 합니다.  
  
```  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = NO )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>4. 지리적 복제 보조를 제거 합니다.  
 서버에서 보조 데이터베이스에서는 db1 제거 `secondaryserver`합니다.  
  
```  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>5. 지리적 복제 보조 복제본으로 장애 조치  
 서버에서 보조 데이터베이스에서는 db1 승격 `secondaryserver` 새로운 주 데이터베이스 서버에서 실행 되도록 `secondaryserver`합니다.  
  
```  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE database&#40; Azure SQL 데이터베이스 &#41;](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION level&#40; Transact SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.data_spaces &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [시스템 데이터베이스](../../relational-databases/databases/system-databases.md)  
  
  

