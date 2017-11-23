---
title: "ALTER DATABASE (Azure SQL 데이터 웨어하우스) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
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
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: "20"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.openlocfilehash: 758f303efd228d806db53075f92cc8dd4664d40b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTER DATABASE (Azure SQL 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

이름, 최대 크기 또는 데이터베이스에 대 한 서비스 목표를 수정합니다.  
  
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
수정할 데이터베이스의 이름을 지정 합니다.  

MODIFY NAME = *new_database_name*  
로 지정 된 이름의 데이터베이스를 이름을 바꿉니다. *new_database_name*합니다.  
  
MAXSIZE  
기본값은 10, 240 GB (10TB).  

**적용 대상:** 탄력성 성능 계층에 대해 최적화

데이터베이스에 대 한 최대 허용 크기입니다. 데이터베이스 최대 크기 보다 커질 수 없습니다. 

**적용 대상:** 컴퓨팅 성능 계층에 대해 최적화

Rowstore 데이터는 데이터베이스에 대 한 최대 허용 크기입니다. Rowstore 테이블, columnstore 인덱스의 deltastore 또는 클러스터형된 columnstore 인덱스에서 비클러스터형 인덱스에 저장 된 데이터는 MAXSIZE 보다 커질 수 없습니다.  Columnstore 형식으로 압축 된 데이터 크기 제한이 없고 MAXSIZE 제한 되지 않습니다. 
  
SERVICE_OBJECTIVE  
성능 수준을 지정합니다. 에 대 한 서비스 목표에 대 한 자세한 내용은 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], 참조 [성능 계층](https://azure.microsoft.com/documentation/articles/performance-tiers/)합니다.  
  
## <a name="permissions"></a>Permissions  
이러한 권한이 필요합니다.  
  
-   서버 수준 보안 주체 로그인 (프로 비전 프로세스로 만들어진 하나) 또는  
  
-   멤버는 `dbmanager` 데이터베이스 역할입니다.  
  
데이터베이스의 소유자는 소유자의 멤버인 경우 데이터베이스를 변경할 수 없습니다는 `dbmanager` 역할입니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
현재 데이터베이스에 따라서 변경 된 것 보다 다른 데이터베이스 여야 합니다. **ALTER master 데이터베이스에 연결 되어 있는 동안 실행 해야**합니다.  
  
SQL 데이터 웨어하우스 COMPATIBILITY_LEVEL 130으로 설정 되 고 변경할 수 없습니다. 자세한 내용은 참조 하십시오. [Azure SQL 데이터베이스의 호환성 수준을 130으로 쿼리 성능을 향상](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)합니다.
  
사용 하 여 데이터베이스의 크기를 줄이려면 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
ALTER DATABASE를 실행 하려면 데이터베이스가 온라인 이어야 하며 일시 중지 된 상태에 있을 수 없습니다.  
  
ALTER DATABASE 문의 기본 트랜잭션 관리 모드인 자동 커밋 모드에서 실행 해야 합니다. 이 작업은 연결 설정에서 설정 됩니다.  
  
ALTER DATABASE 문이 사용자 정의 트랜잭션 포함 될 수 없습니다.

데이터베이스 데이터 정렬을 변경할 수 없습니다.  
  
## <a name="examples"></a>예  
이러한 예제를 실행 하기 전에 변경 된 데이터베이스는 현재 데이터베이스 아닌지 확인 합니다. 현재 데이터베이스에 따라서 변경 된 것 보다 다른 데이터베이스 여야 합니다. **ALTER master 데이터베이스에 연결 되어 있는 동안 실행 해야**합니다.  

### <a name="a-change-the-name-of-the-database"></a>1. 데이터베이스의 이름 변경  

```  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>2. 데이터베이스에 대 한 최대 크기를 변경 합니다.  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>3. 성능 수준 변경  
  
```  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>4. 최대 크기와 성능 수준 변경  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>관련 항목:  
[CREATE DATABASE (Azure SQL 데이터 웨어하우스)](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[SQL 데이터 웨어하우스 목록이 참조 항목](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  
