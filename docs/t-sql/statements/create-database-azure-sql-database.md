---
title: CREATE DATABASE(Azure SQL Datebase) | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: e5d3ff692dc3935bb8791d4c71285b3b7f2a55b7
ms.sourcegitcommit: 02c889a1544b0859c8049827878d66b2301315f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225281"
---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  새 데이터베이스를 만듭니다.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

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
  | ( EDITION = {  'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical' } 
  | SERVICE_OBJECTIVE = 
    {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
      | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' | 'GP_GEN4_24' |
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 'BC_GEN4_24' |
      | 'GP_GEN5_2' | 'GP_GEN5_4' | 'GP_GEN5_8' | 'GP_GEN5_16' | 'GP_GEN5_24' | 'GP_GEN5_32' | 'GP_GEN5_48' | 'GP_GEN5_80' |
      | 'BC_GEN5_2' | 'BC_GEN5_4' | 'BC_GEN5_8' | 'BC_GEN5_16' | 'BC_GEN5_24' | 'BC_GEN5_32' | 'BC_GEN5_48' | 'BC_GEN5_80' |
      | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE = 
      {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' | 'GP_GEN4_24' |
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 'BC_GEN4_24' |
      | 'GP_GEN5_2' | 'GP_GEN5_4' | 'GP_GEN5_8' | 'GP_GEN5_16' | 'GP_GEN5_24' | 'GP_GEN5_32' | 'GP_GEN5_48' | 'GP_GEN5_80' |
      | 'BC_GEN5_2' | 'BC_GEN5_4' | 'BC_GEN5_8' | 'BC_GEN5_16' | 'BC_GEN5_24' | 'BC_GEN5_32' | 'BC_GEN5_48' | 'BC_GEN5_80' |
        | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
  ]  
 [;] 
 
```  
  
## <a name="arguments"></a>인수  
 이 구문 다이어그램은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 지원되는 인수를 보여 줍니다.  
  
*database_name* 
 
새 데이터베이스의 이름입니다. 이 이름은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 데이터베이스 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 데이터베이스를 모두 호스트할 수 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자에 대한 규칙을 준수할 수 있는 SQL 서버에서 고유해야 합니다. 자세한 내용은 [식별자](http://go.microsoft.com/fwlink/p/?LinkId=180386)를 참조하세요.  
  
*Collation_name*  

데이터베이스의 기본 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 지정되지 않는 경우 해당 데이터베이스가 기본 데이터 정렬 SQL_Latin1_General_CP1_CI_AS에 할당됩니다.  
  
Windows 및 SQL 데이터 정렬 이름에 대한 자세한 내용은 [COLLATE(Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)를 참조하세요.  
  
CATALOG_COLLATION  

메타데이터 카탈로그의 기본 데이터 정렬을 지정합니다. *DATABASE_DEFAULT*는 시스템 뷰와 시스템 테이블에 사용된 메타데이터 카탈로그가 데이터베이스의 기본 데이터 정렬과 일치하게 데이터를 정렬하도록 지정합니다.   이것은 SQL Server에서 발견되는 동작입니다. 

*SQL_Latin1_General_CP1_CI_AS*는 시스템 뷰와 테이블에 사용된 메타데이터 카탈로그가 고정된 SQL_Latin1_General_CP1_CI_AS 데이터 정렬로 정렬되도록 지정합니다.  이것이 지정되지 않은 경우 Azure SQL Database의 기본 설정입니다.

버전
 
데이터베이스의 서비스 계층을 지정합니다. 사용 가능한 값은: '기본', '표준', '프리미엄', 'GeneralPurpose' 및 'BusinessCritical'입니다. ‘Premiumrs’에 대한 지원이 제거되었습니다. 질문에 대해서는, 이메일 별칭(premium-rs@microsoft.com)을 사용하세요.
  
 EDITION이 지정되고 MAXSIZE는 지정되지 않은 경우, MAXSIZE는 버전에서 지원되는 가장 제한적인 크기로 설정됩니다.  
  
 MAXSIZE

데이터베이스의 최대 크기를 지정합니다. MAXSIZE는 지정된 EDITION(서비스 계층)에 대해 유효해야 합니다. 지원되는 MAXSIZE 값 및 서비스 계층의 기본값(D)은 다음과 같습니다.

**DTU 기반 모델**

|**MAXSIZE**|**기본**|**S0-S2**|**S3-S12**|**P1-P6**| **P11-P15** | 
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
|750GB|해당 사항 없음|해당 사항 없음|√|√|√|
|1024GB|해당 사항 없음|해당 사항 없음|√|√|√ (D)|
|1024GB에서 최대 4096GB(256 GB*로 증분) |해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|√|√|  
  
\* P11과 P15는 기본 크기인 1024를 사용하여 MAXSIZE를 최대 4TB까지 허용합니다.  P11 및 P15는 추가 비용없이 최대 4TB가 포함된 저장소를 사용할 수 있습니다. 프리미엄 계층에서 1TB 초과의 MAXSIZE는 현재 미국 동부2, 미국 서부, 미국 버지니아 주 정부, 서부 유럽, 독일 중앙, 동남 아시아, 일본 동부, 오스트레일리아 동부, 캐나다 중앙 및 캐나다 동부에서 사용할 수 있습니다. DTU 기반 모델에 대한 리소스 제한에 대한 자세한 내용은 [DTU 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요.  

DTU 기반 모델에 대한 MAXSIZE 값은 지정된 경우 지정된 서비스 계층에 대한 위의 표에 표시된 유효한 값이어야 합니다.
 
**vCore 기반 모델**

**범용 서비스 계층 - 4세대 계산 플랫폼**
|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_4|GP_Gen4_8|GP_Gen4_16|GP4_24|
|:--- | --: |--: |--: |--: |--: |--:|
|최대 데이터 크기(GB)|1024|1024|1536|3072|4096|4096|

**범용 서비스 계층 - 5세대 계산 플랫폼**
|MAXSIZE|GP_Gen5_2|GP_Gen5_4|GP_Gen5_8|GP_Gen5_16|GP_Gen5_24|GP_Gen5_32|GP_Gen5_48|GP_Gen5_80|
|:----- | ------: |-------: |-------: |--------: |--------: |---------:|--------: |---------: |
|최대 데이터 크기(GB)|1024|1024|1536|3072|4096|4096|4096|4096|


**중요 비즈니스용 서비스 계층 - 4세대 계산 플랫폼**
|성능 수준|BC_Gen4_1|BC_Gen4_2|BC_Gen4_4|BC_Gen4_8|BC_Gen4_16|
|:--- | --: |--: |--: |--: |--: |--: |
|최대 데이터 크기(GB)|1024|1024|1024|1024|1024|1024|

**중요 비즈니스용 서비스 계층 - 5세대 계산 플랫폼**
|MAXSIZE|BC_Gen5_2|BC_Gen5_4|BC_Gen5_8|BC_Gen5_16|BC_Gen5_24|BC_Gen5_32|BC_Gen5_48|BC_Gen5_80|
|:----- | ------: |-------: |-------: |--------: |--------: |---------:|--------: |---------: |
|최대 데이터 크기(GB)|1024|1024|1024|1024|2048|4096|4096|4096|

vCore 모델을 사용할 때 `MAXSIZE`값이 설정되지 않은 경우 기본값은 32GB입니다. vCore 기반 모델에 대한 리소스 제한에 대한 자세한 내용은 [vCore 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요.
  
MAXSIZE 및 EDITION 인수에는 다음과 같은 규칙이 적용됩니다.  
  
- EDITION이 지정되었지만 MAXSIZE가 지정되지 않은 경우 해당 버전에 대한 기본값이 사용됩니다. 예를 들어 EDITION이 Standard로 설정되었고 MAXSIZE가 지정되지 않았으면 MAXSIZE가 자동으로 250MB로 설정됩니다.  
- MAXSIZE 또는 EDITION이 모두 지정되지 않았으면 EDITION이 Standard(S0)로 설정되고, MAXSIZE는 250GB로 설정됩니다.  

SERVICE_OBJECTIVE

성능 수준을 지정합니다. 서비스 목표에 사용 가능한 값은 `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1`, `BC_GEN4_2`, `BC_GEN4_4`, `BC_GEN4_8`, `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`, `GP_Gen5_8`, `GP_Gen5_16`, `GP_Gen5_24`, `GP_Gen5_32`, `GP_Gen5_48`, `GP_Gen5_80`, `BC_Gen5_2`, `BC_Gen5_4`, `BC_Gen5_8`, `BC_Gen5_16`, `BC_Gen5_24`, `BC_Gen5_32`, `BC_Gen5_48`, `BC_Gen5_80`입니다. 

서비스 목표 설명과 크기, 버전 및 서비스 목표 조합 등의 정보에 대한 자세한 내용은 [Azure SQL Database 서비스 계층](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers)을 참조하세요. 지정된 SERVICE_OBJECTIVE를 EDITION에서 지원하지 않는 경우 오류가 표시됩니다. SERVICE_OBJECTIVE 값을 한 계층에서 다른 계층으로 변경하려면(예: S1에서 P1로 변경), EDITION 값도 변경해야 합니다. 서비스 목표 설명과 크기, 버전 및 서비스 목표 조합 등의 정보에 대한 자세한 내용은 [Azure SQL Database 서비스 계층 및 성능 수준](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) 및 [DTU 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) 및 [vCore 기반 리소스 제한](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)을 참조하세요.  PRS 서비스 목표에 대한 지원이 제거되었습니다. 질문에 대해서는, 이메일 별칭(premium-rs@microsoft.com)을 사용하세요. 
  
ELASTIC_POOL(name = \<elastic_pool_name>)
 
탄력적 데이터베이스 풀에서 새 데이터베이스를 만들려면 데이터베이스의 SERVICE_OBJECTIVE를 ELASTIC_POOL로 설정하고 풀의 이름을 제공합니다. 자세한 내용은 [SQL Database 탄력적 데이터베이스 풀 만들기 및 관리(미리보기)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)를 참조하세요.  
  
AS COPY OF [source_server_name.]source_database_name

동일한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버 또는 다른 서버에 데이터베이스를 복사하기 위한 것입니다.  
  
*source_server_name*  

원본 데이터베이스가 위치한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버의 이름입니다. 이 매개 변수는 원본 데이터베이스와 대상 데이터베이스가 동일한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 있을 때 선택할 수 있습니다.  
  
> [!NOTE]
> `AS COPY OF` 인수는 정규화된 고유 도메인 이름을 지원하지 않습니다. 즉, 서버의 정규화된 도메인 이름은 `serverName.database.windows.net`이며, 데이터베이스 복사 중 `serverName`만 사용합니다.  
  
*source_database_name*

복사할 데이터베이스의 이름입니다.  
  
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]은 `CREATE DATABASE` 문 사용시 다음 인수 및 옵션을 지원하지 않습니다.  
  
- \<filespec> 및 \<filegroup> 등 파일의 물리적 위치와 관련된 매개 변수  
  
- DB_CHAINING and TRUSTWORTHY와 같은 외부 액세스 옵션입니다.  
  
- 데이터베이스 연결  
  
- ENABLE_BROKER, NEW_BROKER 및 ERROR_BROKER_CONVERSATIONS 등의 서비스 브로커 옵션입니다.  
  
- 데이터베이스 스냅숏  
  
인수 및 `CREATE DATABASE` 명령문에 대한 자세한 내용은 [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>Remarks
 
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 데이터베이스에는 데이터베이스가 만들어질 때 설정된 몇 가지 기본 설정이 있습니다. 이러한 기본 설정에 대한 자세한 내용은 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)의 값 목록을 참조하세요.  
  
MAXSIZE에는 데이터베이스의 크기를 제한하는 기능이 있습니다. 데이터베이스 크기가 MAXSIZE에 도달하면 40544 오류 코드가 나타납니다. 이 경우, 데이터를 삽입 또는 업데이트하거나 새 개체(예: 테이블, 저장된 프로시저, 뷰 및 함수)를 만들 수 없습니다. 그러나 데이터 읽기 및 삭제, 테이블 자르기, 테이블 및 인덱스 삭제, 인덱스 다시 작성은 가능합니다. 그런 다음 MAXSIZE를 현재 데이터베이스 크기보다 큰 값으로 업데이트하거나 일부 데이터를 삭제하여 저장소 공간을 비울 수 있습니다. 새 데이터 삽입까지 최대 15분을 지연시킬 수 있습니다.  
  
> [!IMPORTANT]  
>  `CREATE DATABASE` 문은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 유일한 문이어야 합니다. 
  
나중에 크기, 버전 또는 서비스 목표 값을 변경하려면, [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)를 사용하세요.  

CATALOG_COLLATION 인수는 데이터베이스를 생성하는 동안에만 사용할 수 있습니다. 
  
## <a name="database-copies"></a>데이터베이스 복사본  

`CREATE DATABASE` 문을 사용한 데이터베이스 복사는 비동기 작업입니다. 따라서 전체 복사 프로세스가 끝날 때까지 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 연결할 필요가 없습니다. `CREATE DATABASE` 문은 sys.databases에서 항목을 만든 후 데이터베이스 복사 작업이 완료되기 전에 사용자에게 컨트롤을 반환합니다. 즉, 데이터베이스 복사가 진행 중인 동안에 `CREATE DATABASE` 문을 반환합니다.  
  
- [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 서버에서 복사 프로세스 모니터링: [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)의 `percentage_complete` 또는 `replication_state_desc` 열 또는 **sys.databases** 보기의 `state` 열을 쿼리합니다. 데이터베이스 복사를 포함해서 데이터베이스 작업의 상태를 반환하는 것뿐만 아니라 [ sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 보기도 사용할 수 있습니다.  
  
복사 프로세스가 완료되면 트랜잭션에서 대상 데이터베이스가 원본 데이터베이스와 일치하게 됩니다.  
  
`AS COPY OF` 인수를 사용할 때는 다음 구문 및 의미 체계 규칙에 따라야 합니다.  
  
- 원본 서버 이름과 복사 대상 서버의 이름은 서로 같아도 되고 달라도 됩니다. 이름이 동일한 경우 이 매개 변수는 선택적으로, 현재 세션의 서버 컨텍스트가 기본값으로 사용됩니다.  
  
- 원본 및 대상 데이터베이스 이름은 고유하게 지정해야 하며 식별자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 규칙을 따라야 합니다. 자세한 내용은 [식별자](http://go.microsoft.com/fwlink/p/?LinkId=180386)를 참조하세요.  
  
- `CREATE DATABASE` 문은 새 데이터베이스가 만들어질 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버의 master 데이터베이스 컨텍스트 내에서 실행되어야 합니다. 
- 복사를 마친 뒤에는 대상 데이터베이스를 독립적인 데이터베이스로 관리해야 합니다. 원본 데이터베이스와 별도로 새 데이터베이스에 대해 `ALTER DATABASE` 및 `DROP DATABASE` 문을 실행할 수 있습니다. 또한 새 데이터베이스를 다른 새 데이터베이스에 복사할 수 있습니다.  
  
- 데이터베이스 복사가 진행 중인 동안에도 계속해서 원본 데이터베이스에 액세스할 수 있습니다.  
  
 자세한 내용은 [Transact-SQL을 사용하여 Azure SQL 데이터베이스의 복사본 만들기](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스를 만들려면 로그인은 다음 중 하나여야 합니다.  
  
- 서버 수준 보안 주체 로그인  
  
- 로컬 Azure SQL Server에 대한 Azure AD 관리자  
  
- 로그인은 `dbmanager` 데이터베이스 역할의 멤버입니다.  
  
 `CREATE DATABASE ... AS COPY OF` 구문 사용에 대한 **추가 요구 사항: 로컬 서버에는 문을 실행 하는**  로그인은 적어도 `db_owner` 원본 서버에 있어야 합니다. 로그인이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 기반으로 하는 경우, 로컬 서버의 문을 실행하는 로그인에는 동일한 이름과 암호를 사용하여 원본 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에서 일치하는 로그온이 있어야 합니다.  
  
## <a name="examples"></a>예  
SQL Server Management Studio를 사용하여 Azure SQL 데이터베이스에 연결하는 방법을 보여주는 빠른 시작 자습서를 보려면, [Azure SQL Database: SQL Server Management Studio를 사용하여 데이터 연결 및 쿼리](/azure/sql-database/sql-database-connect-query-ssms)를 참조합니다.  
  
### <a name="simple-example"></a>간단한 예  
 데이터베이스를 만드는 간단한 예  
  
```sql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>에디션을 사용하는 간단한 예  
 표준 데이터베이스를 만드는 간단한 예  
  
```sql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>추가 옵션이 있는 예  
 여러 옵션을 사용하는 예  
  
```sql  
CREATE DATABASE hito 
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS 
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>복사본 만들기  
 데이터베이스의 복사본을 만드는 예  
  
```sql  
CREATE DATABASE escuela 
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>탄력적 풀에 데이터베이스 만들기  
 S3M100이라는 풀에 새 데이터베이스를 만듭니다.  
  
```sql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>다른 서버에서 데이터베이스 복사본 만들기  
 다음 예에서는 단일 데이터베이스의 P2 성능 수준에 db_copy라는 이름의 db_original 데이터베이스의 복사본을 만듭니다.  이것은 db_original이 단일 데이터베이스의 탄력적 풀 또는 성능 수준에 관계없이 적용됩니다.  
  
```sql  
CREATE DATABASE db_copy 
  AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 다음 예에서는 ep1이라는 이름의 탄력적 풀에 db_copy라는 이름의 db_original 데이터베이스의 복사본을 만듭니다.  이것은 db_original이 단일 데이터베이스의 탄력적 풀 또는 성능 수준에 관계없이 적용됩니다.  Db_original이 다른 이름을 가진 탄력적 풀에 있으면 db_copy는 여전히 ep1에 생성됩니다.  
  
```sql  
CREATE DATABASE db_copy 
  AS COPY OF ozabzw7545.db_original 
  (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>지정된 카탈로그 데이터 정렬 값을 사용하여 데이터베이스 만들기

다음 예에서는 카탈로그 데이터 정렬을 데이터베이스 데이터 생성 중에 DATABASE_DEFAULT로 설정하며, 카탈로그 데이터 정렬을 데이터베이스 데이터 정렬과 동일하게 설정합니다.

```sql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
  WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>관련 항목:  

-  [sys.dm_database_copies&#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

- [ALTER DATABASE &#40;Azure SQL Database&#41;](alter-database-azure-sql-database.md) 
  
  

