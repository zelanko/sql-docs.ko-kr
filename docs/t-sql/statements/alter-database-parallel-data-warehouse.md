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
ms.openlocfilehash: 3d199b9822d591c10f1f4d9af232b9f74d7e8a81
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE(병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  복제된 테이블, 분산된 테이블 및 트랜잭션 로그인 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 대한 최대 데이터베이스 크기 옵션을 수정합니다. 이 문을 사용하여 크기의 축소나 확대에 따라 데이터베이스에 대한 디스크 공간 할당을 관리합니다.  
  
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
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 REPLICATED_SIZE, DISTRIBUTED_SIZE 및 LOG_SIZE에 대한 값이 데이터베이스에 대한 현재 값 보다 크거나 작거나 같을 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 확장 및 축소 작업은 근사치입니다. 결과로 생성된 실제 크기는 매개 변수에 따라 다를 수 있습니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 원자 조작으로서 ALTER DATABASE 문을 수행 하지 않습니다. 실행 동안 이 문이 중단되는 경우 이미 발생한 변경 내용은 유지됩니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [CREATE DATABASE &#40;병렬 데이터 웨어하우스&#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
