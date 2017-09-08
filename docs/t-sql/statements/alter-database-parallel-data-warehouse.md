---
title: "ALTER DATABASE (병렬 데이터 웨어하우스) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 74b47bec1033728d47e5fe577af29c6d43e9af65
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE (병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  복제 된 테이블, 분산된 테이블 및에서 트랜잭션 로그에 대 한 최대 데이터베이스 크기 옵션을 수정 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다. 이 문을 사용 하 여 확대 하 되거나 크기를 축소 데이터베이스에 대 한 디스크 공간 할당을 관리 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 수정할 데이터베이스의 이름입니다. 데이터베이스 목록이 어플라이언스에서 표시 하려면 사용 [sys.databases&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 자동 증가 = {ON | OFF}  
 자동 증가 옵션을 업데이트합니다. 자동 증가 ON 일 때 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 성장 저장소 요구 사항에 맞게 필요에 따라 복제 된 테이블, 분산된 테이블 및 트랜잭션 로그에 할당된 된 공간을 자동으로 증가 합니다. 자동 증가 옵션이 OFF, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 에서 오류를 반환 하는 경우 복제 된 테이블, 분산 테이블 또는 트랜잭션 로그의 최대 크기 설정을 초과 합니다.  
  
 REPLICATED_SIZE = *크기* [GB]  
 복제 된 테이블의 모든 변경 되는 데이터베이스에 저장 하기 위한 계산 노드당 최대 새 기가바이트를 지정 합니다. 어플라이언스 저장 공간을 계획 하는 경우 어플라이언스의 계산 노드 수 REPLICATED_SIZE 곱한 해야 합니다.  
  
 DISTRIBUTED_SIZE = *크기* [GB]  
 모든 분산된 테이블이 변경 되는 데이터베이스에 저장 하기 위한 데이터베이스 당 최대 새 기가바이트를 지정 합니다. 크기는 모든 어플라이언스의 계산 노드에 분산 됩니다.  
  
 LOG_SIZE = *크기* [GB]  
 변경할 데이터베이스의 모든 트랜잭션 로그를 저장 하기 위한 데이터베이스 당 최대 새 기가바이트를 지정 합니다. 크기는 모든 어플라이언스의 계산 노드에 분산 됩니다.  
  
 암호화 {ON | OFF}  
 데이터베이스를 암호화하거나(ON) 암호화하지 않도록(OFF) 설정합니다. 암호화에 대해 구성할 수 있습니다 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 때 [가 sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e) 가로 설정 된 **1**합니다. 투명 한 데이터 암호화를 구성 하려면 데이터베이스 암호화 키를 만들어야 합니다. 데이터베이스 암호화에 대 한 자세한 내용은 참조 [투명 한 데이터 암호화 &#40; Tde&#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대 한 ALTER 권한이 필요합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 REPLICATED_SIZE, DISTRIBUTED_SIZE, 및 LOG_SIZE에 대 한 값 보다 큰, 같은지 또는 데이터베이스에 대 한 현재 값 보다 작은 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 확장 및 축소 작업 사항은 근사값으로 표시 합니다. 결과 실제 크기 크기 매개 변수에서 달라질 수 있습니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]원자 단위 연산으로 ALTER DATABASE 문을 수행 하지 않습니다. 문을 실행 하는 동안 중단 되 면 이미 발생 한 변경 내용이 유지 됩니다.  
  
## <a name="locking-behavior"></a>잠금 동작  
 데이터베이스 개체에 대 한 공유 잠금을 사용합니다. 읽기 또는 쓰기에 대 한 다른 사용자가 사용 중인 데이터베이스를 변경할 수 없습니다. 발급 세션 여기에 한 [사용](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15) 데이터베이스에서 문입니다.  
  
## <a name="performance"></a>성능  
 데이터베이스 축소 된 데이터베이스 내의 실제 데이터의 크기에 따라 시간 및 시스템 리소스에 많은 양 및 디스크에 조각화의 양은 걸릴 수 있습니다. 예를 들어 데이터베이스 축소 이상 걸릴 수 있습니다 여러 시간입니다.  
  
## <a name="determining-encryption-progress"></a>암호화 진행률을 결정  
 다음 쿼리를 사용 하 여 데이터베이스 투명 한 데이터 암호화를 백분율로 진행률을 확인 하려면:  
  
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
  
 TDE를 구현 하는의 모든 단계를 보여 주는 포괄적인 예제를 보려면 [투명 한 데이터 암호화 &#40; Tde&#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>1. 자동 증가 설정 변경  
 데이터베이스에 대 한 자동 증가 ON으로 설정 `CustomerSales`합니다.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>2. 복제 된 테이블에 대 한 최대 저장소 변경  
 다음 예제에서는 데이터베이스에 대 한 복제 된 테이블 저장소 용량 한도 1GB로 설정 `CustomerSales`합니다. 이것이 계산 노드당 저장소 용량 한도입니다.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>3. 분산된 테이블에 대 한 최대 저장소 변경  
 다음 예제에서는 데이터베이스에 대해 1, 000GB (1tb)에 분산된 테이블 저장소 용량 한도 설정 `CustomerSales`합니다. 모든 계산 노드에 대 한 기기 계산 노드당 저장소 제한 안 결합 된 저장소 용량 한도입니다.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>4. 트랜잭션 로그에 대 한 최대 저장소 변경  
 다음 예에서는 데이터베이스를 업데이트 `CustomerSales` 최대값을 가질 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 어플라이언스에 대 한 10GB의 트랜잭션 로그 크기입니다.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE database&#40; 병렬 데이터 웨어하우스 &#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
