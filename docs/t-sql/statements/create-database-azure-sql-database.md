---
title: "CREATE DATABASE (Azure SQL 데이터베이스) | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/28/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SERVICE_OBJECTIVE
- SERVICE_OBJECTIVE_TSQL
- ELASTIC_POOL
- ELASTIC_POOL_TSQL
- EDITION
- EDITION_TSQL
- MAXSIZE
- MAXSIZE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVICE_OBJECTIVE
- ELASTIC_POOL
- EDITION SQL Database
- MAXSIZE SQL Database
ms.assetid: 22b167f7-ae86-490b-adb3-ec02ca1c1508
caps.latest.revision: 62
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: cccf648270523e86e502caebfbc7f6ba6a55cfd7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  새 데이터베이스를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
``` 
  
CREATE DATABASE database_name [ COLLATE collation_name ]  
{  
   (<edition_options> [, ...n])   
}  

[ WITH CATALOG_COLLATION = { DATABASE_DEFAULT | SQL_Latin1_General_CP1_CI_AS }  ]
  
<edition_options> ::=   
{  

      MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }    
    | ( EDITION = {  'basic' | 'standard' | 'premium' | 'premiumrs'}   
    | SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

[ AS COPY OF [source_server_name.]source_database_name ]

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
    ]  
 [;] 
 
```  
  
## <a name="arguments"></a>인수  
 이 구문 다이어그램은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 지원되는 인수를 보여 줍니다.  
  
 *database_name*  
 새 데이터베이스의 이름입니다. 이 이름은 둘 다 포함할 수 있는 SQL server에서 고유 해야 합니다. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 데이터베이스 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 데이터베이스, 준수 및는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자에 대 한 규칙입니다. 자세한 내용은 참조 [식별자](http://go.microsoft.com/fwlink/p/?LinkId=180386)합니다.  
  
 *데이터 정렬 이름*  
 데이터베이스의 기본 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 지정되지 않는 경우 해당 데이터베이스가 기본 데이터 정렬 SQL_Latin1_General_CP1_CI_AS에 할당됩니다.  
  
 Windows 및 SQL 데이터 정렬 이름에 대 한 자세한 내용은 [COLLATE (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)합니다.  
  
 *CATALOG_COLLATION*  
메타 데이터 카탈로그에 대 한 기본 데이터 정렬을 지정합니다. *DATABASE_DEFAULT* 메타 데이터 카탈로그에 사용 되도록 지정 시스템 뷰 및 시스템 테이블은 데이터베이스에 대 한 기본 데이터 정렬에 맞게 대조해 야 합니다.  이것은 SQL Server에서 동작 합니다. 

*SQL_Latin1_General_CP1_CI_AS* 메타 데이터 카탈로그에 사용 되도록 지정 시스템 뷰와 테이블에 고정된 된 SQL_Latin1_General_CP1_CI_AS 데이터 정렬을 대조해 야 합니다.  지정 되지 않은 경우 이것이 Azure SQL 데이터베이스에서 기본 설정입니다.

 *버전*  
 데이터베이스의 서비스 계층을 지정합니다. 사용 가능한 값은: '기본', 'standard', '프리미엄' 및 'premiumrs'.  
  
 EDITION이 지정 하지만 MAXSIZE가 지정 되지 않은 경우 MAXSIZE는 버전에서 지원 하는 가장 제한적인 크기로 설정 됩니다.  
  
 *MAXSIZE*  
 데이터베이스의 최대 크기를 지정합니다. MAXSIZE는 지정된 EDITION(서비스 계층)에 대해 유효해야 합니다. 지원되는 MAXSIZE 값 및 서비스 계층의 기본값(D)은 다음과 같습니다.  
  
|**MAXSIZE**|**Basic**|**S0 S2**|**S3 S12**|**P1 P6 및 PRS1 PRS6**| **P11 P15** 
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
|300GB|해당 사항 없음|해당 사항 없음|√|√|√|  
|400GB|해당 사항 없음|해당 사항 없음|√|√|√|
|500GB|해당 사항 없음|해당 사항 없음|√|√ (D)|√|
|750 GB|해당 사항 없음|해당 사항 없음|√|√|√|
|1024GB|해당 사항 없음|해당 사항 없음|√|√|√ (D)|
|1024GB에서 최대 4, 096 GB 단위로 256 GB * |해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|√|√|  
  
 \*P11 및 P15 허용 MAXSIZE 최대 4TB 1024GB 기본 크기 되 고 사용 합니다.  P11 및 P15 추가 비용 없이 최대 4TB의 포함 된 저장소를 사용할 수 있습니다. 프리미엄 계층에서 1TB 보다 큰 최대 크기는 현재 다음 지역에서 사용할 수 있습니다: 미국 East2, 미국 서 부, 미국 정부 기관용 버지니아, 서 부 유럽, 독일 중앙, 동남 아시아, 일본 동부, 오스트레일리아 동부, 중앙 캐나다 및 캐나다 동부 합니다. 현재 제한 사항에 대 한 참조 [데이터베이스를 단일](https://docs.microsoft.com/azure/sql-database-single-database-resources)합니다.  
  
 MAXSIZE 및 EDITION 인수에는 다음과 같은 규칙이 적용됩니다.  
  
-   MAXSIZE 값(지정된 경우)은 위 표에 표시된 유효한 값이어야 합니다.  
  
-   EDITION이 지정되었지만 MAXSIZE가 지정되지 않은 경우 해당 버전에 대한 기본값이 사용됩니다. 예를 들어 EDITION이 Standard로 설정 하는 경우 MAXSIZE는 지정 하지 않으면 MAXSIZE 250MB로 설정 자동으로 됩니다.  
  
-   MAXSIZE 또는 EDITION이 모두를 지정 EDITION 표준 (S0)로 설정 되 고 MAXSIZE는 250GB를 설정 됩니다.  
  
 SERVICE_OBJECTIVE  
 성능 수준을 지정합니다. 서비스 목표 설명과 크기, 버전 및 서비스 목표 조합에 대 한 자세한 내용은 [Azure SQL 데이터베이스 서비스 계층 및 성능 수준](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) 및 [SQL 데이터베이스 리소스 제한](https://azure.microsoft.com/documentation/articles/sql-database-resource-limits)합니다. 지정된 SERVICE_OBJECTIVE를 EDITION에서 지원하지 않는 경우 오류가 표시됩니다.  
  
 ELASTIC_POOL (이름 = \<elastic_pool_name >) 탄력적 데이터베이스 풀에서 새 데이터베이스를 만들려는 데이터베이스의 SERVICE_OBJECTIVE ELASTIC_POOL로 설정 하 고 풀의 이름을 제공 합니다. 자세한 내용은 참조 [만들기 및 관리 (미리 보기)는 SQL 데이터베이스 탄력적 데이터베이스 풀](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)합니다.  
  
 *다른 이름으로 복사본 [source_server_name] source_database_name*  
 동일한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버 또는 다른 서버에 데이터베이스를 복사하기 위한 것입니다.  
  
 *source_server_name*  
 원본 데이터베이스가 위치한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버의 이름입니다. 이 매개 변수는 원본 데이터베이스와 대상 데이터베이스가 동일한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 있을 때 선택할 수 있습니다.  
  
 참고:는 `AS COPY OF` 인수는 정규화 된 고유 도메인 이름을 지원 하지 않습니다. 즉, 서버의 정규화된 도메인 이름은 `serverName.database.windows.net`이며, 데이터베이스 복사 중 `serverName`만 사용합니다.  
  
 *source_database_name*  
 복사할 데이터베이스의 이름입니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]사용할 때 다음 인수와 옵션을 지원 하지 않습니다는 `CREATE DATABASE` 문:  
  
-   매개 변수 파일의 물리적 위치와 같은 관련 \<filespec > 및 \<파일 그룹 >  
  
-   DB_CHAINING and TRUSTWORTHY와 같은 외부 액세스 옵션입니다.  
  
-   데이터베이스 연결  
  
-   ENABLE_BROKER, NEW_BROKER 및 ERROR_BROKER_CONVERSATIONS 등의 서비스 브로커 옵션입니다.  
  
-   데이터베이스 스냅숏  
  
 인수에 대 한 자세한 내용은 및 `CREATE DATABASE` 문을 참조 [CREATE database&#40; SQL Server transact-sql&#41; ](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 데이터베이스에는 데이터베이스가 만들어질 때 설정된 몇 가지 기본 설정이 있습니다. 이러한 기본 설정에 대 한 자세한 내용은 참조 값 목록이 [DATABASEPROPERTYEX &#40; Transact SQL &#41; ](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
 MAXSIZE에는 데이터베이스의 크기를 제한하는 기능이 있습니다. 데이터베이스의 크기가 해당 MAXSIZE에 도달 하면 40544 오류 코드가 나타납니다. 이 경우, 데이터를 삽입 또는 업데이트하거나 새 개체(예: 테이블, 저장된 프로시저, 뷰 및 함수)를 만들 수 없습니다. 그러나 데이터 읽기 및 삭제, 테이블 자르기, 테이블 및 인덱스 삭제, 인덱스 다시 작성은 가능합니다. 그런 다음 MAXSIZE를 현재 데이터베이스 크기보다 큰 값으로 업데이트하거나 일부 데이터를 삭제하여 저장소 공간을 비울 수 있습니다. 새 데이터 삽입까지 최대 15분을 지연시킬 수 있습니다.  
  
> [!IMPORTANT]  
>  `CREATE DATABASE` 문은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 유일한 문이어야 합니다. 
  
 크기, edition 또는 서비스 목표 값을 나중에 변경 하려면 사용 [ALTER database&#40; Azure SQL 데이터베이스 &#41; ](../../t-sql/statements/alter-database-azure-sql-database.md).  

데이터베이스 생성 중에 CATALOG_COLLATION 인수는 사용할 수만 있습니다. 
  
## <a name="database-copies"></a>데이터베이스 복사본  
 사용 하 여 데이터베이스 복사는 `CREATE DATABASE` 문에 비동기 작업입니다. 따라서 전체 복사 프로세스가 끝날 때까지 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 연결할 필요가 없습니다. `CREATE DATABASE` 문은 sys.databases에서 항목이 만들어졌지만 데이터베이스 복사 하기 전에 작업이 완료 된 후 사용자에 게 제어를 반환 합니다. 즉, 데이터베이스 복사가 진행 중인 동안에 `CREATE DATABASE` 문을 반환합니다.  
  
-   복사 프로세스에 대 한 모니터링는 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 서버: 쿼리는 `percentage_complete` 또는 `replication_state_desc` 열에는 [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md) 또는 `state` 열에는 **sys.databases** 보기입니다. [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 뷰는 데이터베이스 복사본을 포함 하 여 데이터베이스 작업의 상태를 반환 하는 것도 사용할 수 있습니다.  
  
 복사 프로세스가 완료되면 트랜잭션에서 대상 데이터베이스가 원본 데이터베이스와 일치하게 됩니다.  
  
 `AS COPY OF` 인수를 사용할 때는 다음 구문 및 의미 체계 규칙에 따라야 합니다.  
  
-   원본 서버 이름과 복사 대상 서버의 이름은 서로 같아도 되고 달라도 됩니다. 동일한 인 경우이 매개 변수는 선택적 이며 현재 세션의 서버 컨텍스트가 기본적으로 사용 됩니다.  
  
-   원본 및 대상 데이터베이스 이름은 고유하게 지정해야 하며 식별자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 규칙을 따라야 합니다. 자세한 내용은 참조 [식별자](http://go.microsoft.com/fwlink/p/?LinkId=180386)합니다.  
  
-   `CREATE DATABASE` 문은 새 데이터베이스가 만들어질 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버의 master 데이터베이스 컨텍스트 내에서 실행되어야 합니다.  
  
-   복사를 마친 뒤에는 대상 데이터베이스를 독립적인 데이터베이스로 관리해야 합니다. 원본 데이터베이스와 별도로 새 데이터베이스에 대해 `ALTER DATABASE` 및 `DROP DATABASE` 문을 실행할 수 있습니다. 또한 새 데이터베이스를 다른 새 데이터베이스에 복사할 수 있습니다.  
  
-   데이터베이스 복사가 진행 중인 동안에도 계속해서 원본 데이터베이스에 액세스할 수 있습니다.  
  
 자세한 내용은 참조 [TRANSACT-SQL을 사용 하 여 Azure SQL 데이터베이스의 복사본을 만들고](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/)합니다.  
  
## <a name="permissions"></a>Permissions  
 로그인을 만들려면 데이터베이스 들은 다음 중 하나 이상을 여야 합니다.  
  
-   서버 수준 보안 주체 로그인  
  
-   로컬 Azure SQL Server에 대 한 Azure AD 관리자  
  
-   멤버인 로그인은 `dbmanager` 데이터베이스 역할  
  
 **사용에 대 한 추가 요구 사항 `CREATE DATABASE ... AS COPY OF` 구문:** 로컬 서버에는 문을 실행 하는 로그인 수도 있어야 적어도 `db_owner` 원본 서버에 있습니다. 로그인 기반으로 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 로컬 서버에는 문을 실행 하는 로그인 원본에 대해 일치 하는 로그인을가지고 있어야 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버, 동일한 이름 및 암호.  
  
## <a name="examples"></a>예  
SQL Server Management Studio를 사용 하 여 Azure SQL 데이터베이스에 연결 하는 방법을 보여 주는 빠른 시작 자습서를 참조 하십시오. [Azure SQL 데이터베이스: 연결 및 데이터를 쿼리를 사용 하 여 SQL Server Management Studio](/azure/sql-database/sql-database-connect-query-ssms)합니다.  
  
### <a name="simple-example"></a>간단한 예  
 데이터베이스를 만들기 위한 간단한 예입니다.  
  
```tsql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>Edition 간단한 예  
 표준 데이터베이스를 만들기 위한 간단한 예입니다.  
  
```tsql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>추가 옵션으로는 예제  
 여러 개의 옵션을 사용 하는 예제입니다.  
  
```tsql  
CREATE DATABASE hito   
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS   
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>복사본 만들기  
 데이터베이스의 복사본을 만드는 예입니다.  
  
```tsql  
CREATE DATABASE escuela   
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>탄력적 풀의 데이터베이스 만들기  
 S3M100 이라는 풀에 새 데이터베이스를 만듭니다.  
  
```tsql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>다른 서버에서 데이터베이스의 복사본 만들기  
 다음 예에서는 P2 성능 수준에서 db_copy 단일 데이터베이스에 대 한 명명 된 db_original 데이터베이스의 복사본을 만듭니다.  탄력적 풀 또는 단일 데이터베이스에 대 한 성능 수준을 db_original 인지에 관계 없이 유용 합니다.  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 다음 예에서는 라는 ep1 라는 탄력적 풀의 db_copy db_original 데이터베이스의 복사본을 만듭니다.  탄력적 풀 또는 단일 데이터베이스에 대 한 성능 수준을 db_original 인지에 관계 없이 유용 합니다.  Db_original 다른 이름의 탄력적 풀에 있으면 db_copy ep1에 생성 계속 됩니다.  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original   
    (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>지정 된 카탈로그 데이터 정렬 값을 가진 데이터베이스 만들기

다음 예제에서는 DATABASE_DEFAULT 카탈로그 데이터 정렬이 카탈로그 데이터 정렬은 데이터베이스 데이터 정렬으로 동일 하 게 설정 하는 데이터베이스 생성 중 설정 합니다.

```tsql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
      WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>참고 항목  

-  [sys.dm_database_copies &#40; Azure SQL 데이터베이스 &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

-   [ALTER database&#40; Azure SQL 데이터베이스 &#41;](/sql-docs/docs/t-sql/statements/alter-database-azure-sql-database)   
    
  


