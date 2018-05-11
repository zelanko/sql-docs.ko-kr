---
title: ALTER DATABASE(Azure SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 2e89ba1dde52c1b5cb919ff34181d7ca723b6c61
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTER DATABASE(Azure SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

데이터베이스의 이름, 최대 크기 또는 서비스 목표를 수정합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER DATABASE database_name  

  MODIFY NAME = new_database_name  
| MODIFY ( <edition_option> [, ... n] )  
  
<edition_option> ::=   
      MAXSIZE = { 
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 
          | 92160 | 102400 | 153600 | 204800 | 245760 
      } GB  
      | SERVICE_OBJECTIVE = { 
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' 
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' 
          | 'DW3000' | 'DW6000' | 'DW1000c' | 'DW1500c' | 'DW2000c' 
          | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c' | 'DW7500c' 
          | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }  
```  
  
## <a name="arguments"></a>인수  
*database_name*  
수정할 데이터베이스의 이름을 지정합니다.  

MODIFY NAME = *new_database_name*  
데이터베이스의 이름을 지정된 이름 *new_database_name*으로 바꿉니다.  
  
MAXSIZE  
기본값은 245,760GB(240TB)입니다.  

**적용 대상:** 탄력성 성능 계층에 최적화됨

데이터베이스의 최대 허용 크기입니다. 데이터베이스는 MAXSIZE 이상으로 커질 수 없습니다. 

**적용 대상:** 컴퓨팅 성능 계층에 최적화됨

데이터베이스의 rowstore 데이터에 허용되는 최대 크기입니다. Rowstore 테이블, columnstore 인덱스의 deltastore 또는 클러스터된 columnstore 인덱스의 비클러스터된 인덱스에 저장된 데이터는 MAXSIZE 보다 커질 수 없습니다.  columnstore 형식으로 압축된 데이터에는 크기 제한이 없으며 MAXSIZE에 의해 제한되지 않습니다. 
  
SERVICE_OBJECTIVE  
성능 수준을 지정합니다. [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]의 서비스 목표에 대한 자세한 내용은 [성능 계층](https://azure.microsoft.com/documentation/articles/performance-tiers/)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
다음과 같은 사용 권한이 필요합니다.  
  
-   서버 수준 보안 주체 로그인(프로비전 프로세스에 의해 생성됨) 또는  
  
-   `dbmanager` 데이터 베이스 역할의 멤버  
  
데이터베이스의 소유자가 `dbmanager` 역할의 멤버가 아니면 데이터베이스를 변경할 수 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
현재 데이터베이스는 변경된 것과 다른 데이터베이스여야 합니다. 따라서 **ALTER는 master 데이터베이스에 연결되어 있는 동안 실행되어야 합니다**.  
  
SQL Data Warehouse가 COMPATIBILITY_LEVEL 130으로 설정되어 있으며 변경할 수 없습니다. 자세한 내용은 [Azure SQL Database의 호환성 수준 130으로 향상된 쿼리 성능](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)을 참조하세요.
  
데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)를 사용합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
ALTER DATABASE를 실행하려면 데이터베이스가 온라인이어야 하며 일시 중지된 상태일 수 없습니다.  
  
ALTER DATABASE 문은 기본 트랜잭션 관리 모드인 자동 커밋 모드에서 실행해야 합니다. 이 항목은 연결 설정에서 설정됩니다.  
  
ALTER DATABASE 문은 사용자 정의 트랜잭션에 포함될 수 없습니다.

데이터베이스 데이터 정렬을 변경할 수 없습니다.  
  
## <a name="examples"></a>예  
이러한 예제를 실행하기 전에 변경하는 데이터베이스가 현재 데이터베이스가 아닌지 확인합니다. 현재 데이터베이스는 변경된 것과 다른 데이터베이스여야 합니다. 따라서 **ALTER는 master 데이터베이스에 연결되어 있는 동안 실행되어야 합니다**.  

### <a name="a-change-the-name-of-the-database"></a>1. 데이터베이스의 이름을 변경합니다.  

```  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>2. 데이터베이스의 최대 크기를 변경합니다.  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>3. 성능 수준을 변경합니다.  
  
```  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>4. 최대 크기와 서비스 계층을 변경합니다.  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>참고 항목  
[CREATE DATABASE(Azure SQL Data Warehouse)](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[참조 항목의 SQL Data Warehouse 목록](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  
