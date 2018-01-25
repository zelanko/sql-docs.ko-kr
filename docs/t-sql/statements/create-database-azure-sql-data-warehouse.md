---
title: "(Azure SQL 데이터 웨어하우스) 데이터베이스 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: 
ms.prod_service: sql-data-warehouse
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
author: barbkess
ms.author: barbkess
manager: craigg
ms.openlocfilehash: 51db5c7cbaa2932cfcb819538d743fe1368f6442
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="create-database-azure-sql-data-warehouse"></a>(Azure SQL 데이터 웨어하우스) 데이터베이스 만들기
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
새 데이터베이스의 이름입니다. 이 이름은 둘 다 포함할 수 있는 SQL server에서 고유 해야 합니다. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 데이터베이스 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 데이터베이스, 준수 및는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자에 대 한 규칙입니다. 자세한 내용은 참조 [식별자](http://go.microsoft.com/fwlink/p/?LinkId=180386)합니다.  
  
*collation_name*  
데이터베이스의 기본 데이터 정렬을 지정합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 지정 하지 않으면 기본 데이터 정렬 sql_latin1_general_cp1_ci_as는 데이터베이스에 할당 됩니다.  
  
Windows 및 SQL 데이터 정렬 이름에 대 한 자세한 내용은 참조 [COLLATE (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)합니다.  
  
*버전*  
데이터베이스의 서비스 계층을 지정합니다. 에 대 한 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 'datawarehouse'를 사용 합니다.  
  
*MAXSIZE*  
기본값은 10, 240 GB (10TB).  

**적용 대상:** 탄력성 성능 계층에 대해 최적화

데이터베이스에 대 한 최대 허용 크기입니다. 데이터베이스 최대 크기 보다 커질 수 없습니다. 

**적용 대상:** 컴퓨팅 성능 계층에 대해 최적화

Rowstore 데이터는 데이터베이스에 대 한 최대 허용 크기입니다. Rowstore 테이블, columnstore 인덱스의 deltastore 또는 클러스터형된 columnstore 인덱스에서 비클러스터형 인덱스에 저장 된 데이터는 MAXSIZE 보다 커질 수 없습니다.  Columnstore 형식으로 압축 된 데이터 크기 제한이 없고 MAXSIZE 제한 되지 않습니다.
  
SERVICE_OBJECTIVE  
성능 수준을 지정합니다. 에 대 한 서비스 목표에 대 한 자세한 내용은 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], 참조 [성능 계층](https://azure.microsoft.com/documentation/articles/performance-tiers/)합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
사용 하 여 [DATABASEPROPERTYEX &#40; Transact SQL &#41; ](../../t-sql/functions/databasepropertyex-transact-sql.md) 데이터베이스 속성을 표시 합니다.  
  
사용 하 여 [ALTER database&#40; Azure SQL 데이터 웨어하우스 &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) 최대 크기를 변경 하거나 목표 값을 나중에 서비스입니다.   

SQL 데이터 웨어하우스 COMPATIBILITY_LEVEL 130으로 설정 되 고 변경할 수 없습니다. 자세한 내용은 참조 하십시오. [Azure SQL 데이터베이스의 호환성 수준을 130으로 쿼리 성능을 향상](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)합니다.
  
## <a name="permissions"></a>Permissions  
필수 사용 권한:  
  
-   서버 수준 보안 주체 로그인을 프로 비전 프로세스로 만들어진 또는  
  
-   멤버는 `dbmanager` 데이터베이스 역할입니다.  
  
## <a name="error-handling"></a>오류 처리  
데이터베이스의 크기가 MAXSIZE에 도달 하면 40544 오류 코드가 받게 됩니다. 이 경우 삽입 하 및 데이터를 업데이트 하거나 새 개체 (예: 테이블, 저장된 프로시저, 뷰 및 함수)를 만들 수 없습니다. 읽기 및 데이터를 삭제, 테이블 자르기, 테이블 및 인덱스를 삭제 하 고 수 있습니다 인덱스를 다시 작성 합니다. 그런 다음 MAXSIZE를 현재 데이터베이스 크기보다 큰 값으로 업데이트하거나 일부 데이터를 삭제하여 저장소 공간을 비울 수 있습니다. 새 데이터 삽입까지 최대 15분을 지연시킬 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
새 데이터베이스를 만들려면 master 데이터베이스에 연결해야 합니다.  
  
`CREATE DATABASE` 문은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 유일한 문이어야 합니다.

데이터베이스를 만든 후 데이터베이스 데이터 정렬을 변경할 수 없습니다.   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>예제:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>1. 간단한 예  
데이터 웨어하우스 데이터베이스를 만들기 위한 간단한 예입니다. 그러면 데이터베이스 10240 GB, sql_latin1_general_cp1_ci_as를 기본 데이터 정렬 및 DW100는 가장 작은 계산 능력은 가장 작은 최대 크기로 생성 됩니다.  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>2. 모든 옵션으로 데이터 웨어하우스 데이터베이스 만들기  
만드는 예는 모든 옵션을 사용 하는 10 테라바이트의 데이터 웨어하우스 합니다.  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>관련 항목:  
[ALTER database&#40; Azure SQL 데이터 웨어하우스 &#40; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) 
 [테이블 만들기 &#40; Azure SQL 데이터 웨어하우스 &#41; ](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)  
 [DROP database&#40; Transact SQL &#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  

