---
title: ALTER DATABASE(병렬 데이터 웨어하우스) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b17fcc15be4c8faf496c469bb1e46fe2c6d42012
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34550494"
---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE(병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  복제된 테이블, 분산된 테이블 및 트랜잭션 로그인 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 대한 최대 데이터베이스 크기 옵션을 수정합니다. 이 문을 사용하여 크기의 축소나 확대에 따라 데이터베이스에 대한 디스크 공간 할당을 관리합니다. 이 항목은 병렬 데이터 웨어하우스에서 데이터베이스 옵션 설정과 관련된 구문을 설명합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Parallel Data Warehouse  
ALTER DATABASE database_name    
    SET ( <set_database_options>   | <db_encryption_option> )  
[;]  
  
<set_database_options> ::=   
{  
    AUTOGROW = { ON | OFF }  
    | REPLICATED_SIZE = size [GB]  
    | DISTRIBUTED_SIZE = size [GB]  
    | LOG_SIZE = size [GB]
    | SET AUTO_CREATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS { ON | OFF } 
    | SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 수정할 데이터베이스의 이름입니다. 데이터베이스 목록을 어플라이언스에 표시하려면 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)을 사용합니다.  
  
 AUTOGROW = { ON | OFF }  
 AUTOGROW 옵션을 업데이트합니다. AUTOGROW가 켜진 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]이 저장소 요구 사항의 증가를 수용할 필요에 따라 복제된 테이블, 분산된 테이블 및 트랜잭션 로그에 대해 할당된 공간을 자동으로 증가시킵니다. AUTOGROW가 꺼진 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 복제된 테이블이나 분산된 테이블 또는 트랜잭션 로그가 최대 크기 설정을 초과한 경우 오류를 반환합니다.  
  
 REPLICATED_SIZE = *size* [GB]  
 변경되는 데이터베이스에 모든 복제된 테이블을 저장하기 위해 계산 노드당 최대 기가바이트를 새로 지정합니다. 어플라이언스 저장 공간을 계획하는 경우 어플라이언스에서 REPLICATED_SIZE에 계산 노드 수를 곱해야 합니다.  
  
 DISTRIBUTED_SIZE = *size* [GB]  
 변경되는 데이터베이스에 모든 분산된 테이블을 저장하기 위해 데이터베이스당 최대 기가바이트를 새로 지정합니다. 해당 크기는 어플라이언스의 모든 계산 노드에 분산됩니다.  
  
 LOG_SIZE = *size* [GB]  
 변경되는 데이터베이스에 모든 트랜잭션 로그를 저장하기 위해 데이터베이스당 최대 기가바이트를 새로 지정합니다. 해당 크기는 어플라이언스의 모든 계산 노드에 분산됩니다.  
  
 ENCRYPTION { ON | OFF }  
 데이터베이스를 암호화하거나(ON) 암호화하지 않도록(OFF) 설정합니다. [sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e)이 **1**로 설정된 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 대한 암호화를 구성할 수 있습니다. 투명한 데이터 암호화를 구성하기 전에 데이터베이스 암호화 키를 만들어야 합니다. 데이터 암호화에 대한 자세한 내용은 [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하십시오.  

 SET AUTO_CREATE_STATISTICS { ON | OFF } 자동 통계 작성 옵션인 AUTO_CREATE_STATISTICS가 ON으로 설정된 경우 쿼리 최적화 프로그램은 필요에 따라 쿼리 조건자의 개별 열에 대한 통계를 작성하므로 쿼리 계획에 대한 카디널리티 예상치의 정확도가 높아집니다. 이러한 단일 열 통계는 기존 통계 개체에 히스토그램이 없는 열에 대해 작성됩니다.

 기본값은 AU7로 업그레이드한 후 생성된 새 데이터베이스에 대해 ON입니다. 기본값은 업그레이드 이전에 생성된 데이터베이스에 대해 OFF입니다. 

 통계에 대한 자세한 내용은 [통계](/sql/relational-databases/statistics/statistics) 참조

 SET AUTO_UPDATE_STATISTICS { ON | OFF } 자동 통계 업데이트 옵션인 AUTO_UPDATE_STATISTICS가 ON으로 설정되면 쿼리 최적화 프로그램은 통계가 최신이 아닌 통계가 되는 시점을 확인한 다음, 쿼리에서 사용될 때 이를 업데이트합니다. 작업 삽입, 업데이트, 삭제 또는 병합을 통해 테이블이나 인덱싱된 뷰의 데이터 분포가 변경되면 통계 내용이 더 이상 최신이 아니게 됩니다. 쿼리 최적화 프로그램은 마지막 통계 업데이트 이후 데이터 수정 개수를 계산한 다음 이 수를 임계값과 비교하여 통계가 최신이 아니게 된 시점을 결정합니다. 임계값은 테이블 또는 인덱싱된 뷰의 행 수를 기준으로 합니다.

 기본값은 AU7로 업그레이드한 후 생성된 새 데이터베이스에 대해 ON입니다. 기본값은 업그레이드 이전에 생성된 데이터베이스에 대해 OFF입니다. 

 통계에 대한 자세한 내용은 [통계](/sql/relational-databases/statistics/statistics)를 참조하세요.


 SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF } 비동기 통계 업데이트 옵션인 AUTO_UPDATE_STATISTICS_ASYNC는 쿼리 최적화 프로그램이 동기 또는 비동기 통계 업데이트를 사용하는지를 결정합니다. AUTO_UPDATE_STATISTICS_ASYNC 옵션은 인덱스에 대해 작성된 통계 개체, 쿼리 조건자의 단일 열 및 CREATE STATISTICS 문으로 작성된 통계에 적용됩니다.

 기본값은 AU7로 업그레이드한 후 생성된 새 데이터베이스에 대해 ON입니다. 기본값은 업그레이드 이전에 생성된 데이터베이스에 대해 OFF입니다. 

 통계에 대한 자세한 내용은 [통계](/sql/relational-databases/statistics/statistics)를 참조하세요.

  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
## <a name="error-messages"></a>오류 메시지
자동 통계를 사용하지 않고 통계 설정을 변경하려는 경우 PDW에는 "이 옵션은 PDW에서 지원되지 않습니다"라는 오류가 표시됩니다. 시스템 관리자는 기능 스위치[AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md)를 사용하여 자동 통계를 사용할 수 있습니다.

## <a name="general-remarks"></a>일반적인 주의 사항  
 REPLICATED_SIZE, DISTRIBUTED_SIZE 및 LOG_SIZE에 대한 값이 데이터베이스에 대한 현재 값 보다 크거나 작거나 같을 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 확장 및 축소 작업은 근사치입니다. 결과로 생성된 실제 크기는 매개 변수에 따라 다를 수 있습니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 원자 조작으로서 ALTER DATABASE 문을 수행 하지 않습니다. 실행 동안 이 문이 중단되는 경우 이미 발생한 변경 내용은 유지됩니다.  

통계 설정은 관리자가 자동 통계를 사용하는 경우에만 작동합니다.  사용자가 관리자인 경우 기능 스위치[AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md)를 사용하여 자동 통계를 사용하거나 사용하지 않도록 설정합니다. 
  
## <a name="locking-behavior"></a>잠금 동작  
 DATABASE 개체에 대한 공유 잠금을 사용합니다. 읽기 또는 쓰기를 위해 다른 사용자가 사용 중인 데이터베이스는 변경할 수 없습니다. 여기에는 해당 데이터베이스에서 [USE](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15) 문을 발급한 세션이 포함됩니다.  
  
## <a name="performance"></a>성능  
 데이터베이스 축소는 해당 데이터베이스 내의 실제 데이터의 크기와 디스크의 조각화 양에 따라 많은 시간 및 시스템 리소스가 필요할 수 있습니다. 예를 들어 데이터베이스 축소는 여러 시간 이상이 걸릴 수 있습니다.  
  
## <a name="determining-encryption-progress"></a>암호화 진행률 결정  
 다음 쿼리를 사용하여 데이터베이스 TDE(투명한 데이터 암호화) 진행률을 백분율로 확인하십시오.  
  
```  
WITH  
database_dek AS (  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,  
        dek.encryption_state, dek.percent_complete,  
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,  
        type  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
        ON dek.database_id = node_db_map.database_id   
        AND dek.pdw_node_id = node_db_map.pdw_node_id  
    LEFT JOIN sys.pdw_database_mappings AS db_map  
        ON node_db_map .physical_name = db_map.physical_name  
    INNER JOIN sys.dm_pdw_nodes nodes  
        ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
),  
dek_percent_complete AS (  
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete  
    FROM database_dek  
    WHERE type = 'COMPUTE'  
    GROUP BY database_dek.database_id  
)  
SELECT DB_NAME( database_dek.database_id ) AS name,  
    database_dek.database_id,  
    ISNULL(  
       (SELECT TOP 1 dek_encryption_state.encryption_state  
        FROM database_dek AS dek_encryption_state  
        WHERE dek_encryption_state.database_id = database_dek.database_id  
        ORDER BY (CASE encryption_state  
            WHEN 3 THEN -1  
            ELSE encryption_state  
            END) DESC), 0)  
        AS encryption_state,  
dek_percent_complete.percent_complete,  
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint  
FROM database_dek  
INNER JOIN dek_percent_complete   
    ON dek_percent_complete.database_id = database_dek.database_id  
WHERE type = 'CONTROL';  
```  
  
 TDE를 구현하는 모든 단계를 보여주는 포괄적인 예제는 [투명한 데이터 암호화 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)을 참조합니다.  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]   
  
### <a name="a-altering-the-autogrow-setting"></a>1. AUTOGROW 설정 변경  
 데이터베이스에 대해 AUTOGROW를 ON으로 설정합니다 `CustomerSales`.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>2. 복제된 테이블에 대해 최대 저장소 변경  
 다음 예제에서는 데이터베이스 `CustomerSales`에 대해 복제된 테이블 저장소 용량 한도를 1GB로 설정. 계산 노드당 저장소 용량 한도입니다.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>3. 분산된 테이블에 대해 최대 저장소 변경  
 다음 예제에서는 데이터베이스 `CustomerSales`에 대해 분산된 테이블 저장소 용량 한도를 1000GB(1테라바이트)로 설정합니다. 계산 노드당 저장소 용량 한도가 아닌 모든 계산 노드에 대해 어플라이언스에서 결합된 저장소 용량 한도입니다.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>4. 트랜잭션 로그에 대해 최대 저장소 변경  
 다음 예제에서는 어플라이언스에 대해 10GB의 트랜잭션 로그 크기가 최대값[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 갖도록 데이터베이스 `CustomerSales`를 업데이트합니다.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  

### <a name="e-check-for-current-statistics-values"></a>5. 현재 통계 값에 대한 확인

다음 쿼리는 모든 데이터베이스에 대해 현재 통계 값을 반환합니다. 값이 1이면 기능이 켜져있고 0이면 기능이 꺼져있다는 의미입니다.

```sql
SELECT NAME,
    is_auto_create_stats_on,
    is_auto_update_stats_on,
    is_auto_update_stats_async_on
FROM sys.databases;
```
### <a name="f-enable-auto-create-and-auto-update-stats-for-a-database"></a>6. 데이터베이스에 대한 통계 자동 작성 및 자동 업데이트 사용
다음 명령문을 사용하여 CustomerSales 데이터베이스에 대한 통계를 자동 및 비동기적으로 만들고 업데이트할 수 있습니다.  이렇게 하면 고품질의 쿼리 계획을 만들기 위한 필요에 따라 단일 열 통계를 만들고 업데이트합니다.

```sql
ALTER DATABASE CustomerSales
    SET AUTO_CREATE_STATISTICS ON;
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS ON; 
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS_ASYNC ON;
```
  
## <a name="see-also"></a>참고 항목  
 [CREATE DATABASE &#40;병렬 데이터 웨어하우스&#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
