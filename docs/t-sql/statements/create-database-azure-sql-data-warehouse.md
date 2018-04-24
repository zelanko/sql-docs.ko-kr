---
title: CREATE DATABASE(Azure SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 02/14/20178
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 394f1ebcb7b4d3f70a59e0d2458c8d2025a9d213
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="create-database-azure-sql-data-warehouse"></a>CREATE DATABASE(Azure SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

새 데이터베이스를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 
          250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 
        | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 
        | 153600 | 204800 | 245760 
      } GB ,
    ]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 
         'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' 
        | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' 
        | 'DW1000c' | 'DW1500c' | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c' 
        | 'DW6000c' | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
    }  
)  
[;]  
```  
  
## <a name="arguments"></a>인수  
*database_name*  
새 데이터베이스의 이름입니다. 이 이름은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 데이터베이스 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 데이터베이스를 모두 호스트할 수 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자에 대한 규칙을 준수할 수 있는 SQL 서버에서 고유해야 합니다. 자세한 내용은 [식별자](http://go.microsoft.com/fwlink/p/?LinkId=180386)를 참조하세요.  
  
*collation_name*  
데이터베이스의 기본 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 지정되지 않는 경우 해당 데이터베이스가 기본 데이터 정렬 SQL_Latin1_General_CP1_CI_AS에 할당됩니다.  
  
Windows 및 SQL 데이터 정렬 이름에 대한 자세한 내용은 [COLLATE(Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)를 참조하세요.  
  
*EDITION*  
데이터베이스의 서비스 계층을 지정합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에 대한 'datawarehouse'를 사용합니다.  
  
*MAXSIZE*  
기본값은 245,760GB(240TB).  

**적용 대상:** 탄력성 성능 계층에 최적화됨

데이터베이스의 최대 허용 크기입니다. 데이터베이스는 MAXSIZE 이상으로 커질 수 없습니다. 

**적용 대상:** 컴퓨팅 성능 계층에 최적화됨

데이터베이스의 rowstore 데이터에 허용되는 최대 크기입니다. Rowstore 테이블, columnstore 인덱스의 deltastore 또는 클러스터된 columnstore 인덱스의 비클러스터된 인덱스에 저장된 데이터는 MAXSIZE 보다 커질 수 없습니다.  columnstore 형식으로 압축된 데이터에는 크기 제한이 없으며 MAXSIZE에 의해 제한되지 않습니다.
  
SERVICE_OBJECTIVE  
성능 수준을 지정합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 서비스 목표에 대한 자세한 내용은 [성능 계층](https://azure.microsoft.com/documentation/articles/performance-tiers/)을 참조하세요.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
[DATABASEPROPERTYEX&#40; Transact -SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)을 사용하여 데이터베이스 속성을 참조합니다.  
  
나중에 최대 크기, 또는 서비스 목표 값을 변경하려면, [ALTER DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)를 사용하세요.   

SQL Data Warehouse가 COMPATIBILITY_LEVEL 130으로 설정되어 있으며 변경할 수 없습니다. 자세한 내용은 [Azure SQL Database의 호환성 수준 130으로 향상된 쿼리 성능](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)을 참조하세요.
  
## <a name="permissions"></a>사용 권한  
필요한 권한  
  
-   프로비전 프로세스에 의해 생성된 서버 수준 보안 주체 로그인 또는  
  
-   `dbmanager` 데이터 베이스 역할의 멤버  
  
## <a name="error-handling"></a>오류 처리  
데이터베이스 크기가 MAXSIZE에 도달하면 40544 오류 코드가 나타납니다. 이 경우, 데이터를 삽입 및 업데이트하거나 새 개체(예: 테이블, 저장된 프로시저, 뷰 및 함수)를 만들 수 없습니다. 데이터 읽기 및 삭제, 테이블 자르기, 테이블 및 인덱스 삭제 및 인덱스 다시 작성은 여전히 가능합니다. 그런 다음 MAXSIZE를 현재 데이터베이스 크기보다 큰 값으로 업데이트하거나 일부 데이터를 삭제하여 저장소 공간을 비울 수 있습니다. 새 데이터 삽입까지 최대 15분을 지연시킬 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
새 데이터베이스를 만들려면 master 데이터베이스에 연결해야 합니다.  
  
`CREATE DATABASE` 문은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 유일한 문이어야 합니다.

데이터베이스를 만든 후에는 데이터베이스 데이터 정렬을 변경할 수 없습니다.   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]   
  
### <a name="a-simple-example"></a>1. 간단한 예  
데이터 웨어하우스 데이터베이스를 만드는 간단한 예 그러면 10240 GB의 가장 작은 최대 크기, SQL_Latin1_General_CP1_CI_AS의 기본 데이터 정렬 및 DW100인 가장 작은 계산 능력을 가진 데이터베이스가 생성됩니다.  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>2. 모든 옵션을 사용하여 데이터 웨어하우스 데이터베이스 만들기  
모든 옵션을 사용하여 10 테라바이트 데이터 웨어하우스를 생성하는 예입니다.  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>참고 항목  
[ALTER DATABASE &#40;Azure SQL Data Warehouse&#40;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)
[CREATE TABLE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) 
[DROP DATEBASE &#40;Transact-SQL&#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  

