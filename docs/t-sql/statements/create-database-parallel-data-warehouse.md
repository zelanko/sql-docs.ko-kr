---
title: "(병렬 데이터 웨어하우스) 데이터베이스 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: "13"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e9ff76a4d260604a93f59baa3b61f5c37b4952f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="create-database-parallel-data-warehouse"></a>(병렬 데이터 웨어하우스) 데이터베이스 만들기
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  에 새 데이터베이스를 만듭니다는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 기기입니다. 어플라이언스 데이터베이스와 관련 된 모든 파일을 만들 수 및 최대 크기 및 데이터베이스 테이블 및 트랜잭션 로그에 대 한 자동 증가 옵션을 설정 하려면이 문을 사용 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE DATABASE database_name   
WITH (   
    [ AUTOGROW = ON | OFF , ]   
    REPLICATED_SIZE = replicated_size [ GB ] ,  
    DISTRIBUTED_SIZE = distributed_size [ GB ] ,  
    LOG_SIZE = log_size [ GB ] )  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 새 데이터베이스의 이름입니다. 허용 된 데이터베이스 이름에 대 한 자세한 내용은 "개체 이름 지정 규칙" 및 "예약 된 데이터베이스 이름"의 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 자동 증가 = ON | **OFF**  
 지정 여부는 *replicated_size*, *distributed_size*, 및 *log_size* 의 지정 된 다음 필요에 따라이 데이터베이스에 대 한 매개 변수 자동 증가 크기입니다. 기본값은 **OFF**합니다.  
  
 자동 증가 옵션이 ON 이면 경우 *replicated_size*, *distributed_size*, 및 *log_size* 으로 커집니다 (지정된 된 초기 크기의 블록)에 없는 각 데이터 삽입에 필요 업데이트 또는 기타 필요한 작업을 보다 저장 용량이 큽니다가 이미 할당 되었습니다.  
  
 자동 증가 옵션이 OFF 이면 크기가 자동으로 증가 하지 않습니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]필요한 작업을 시도할 때 오류가 반환 됩니다 *replicated_size*, *distributed_size*, 또는 *log_size* 의 지정 된 값을 초과 하 게 합니다.  
  
 자동 증가 모든 크기에 대 한 ON 또는 OFF 모든 크기에 대 한 합니다. 에 대 한 자동 증가 ON을 설정 하는 예를 들어 *log_size*, 하지만 대해 설정 되지 *replicated_size*합니다.  
  
 *replicated_size* [ GB ]  
 양수입니다. 복제 된 테이블 및 해당 데이터에 할당 된 총 공간에 대 한 크기 (기가바이트) 정수나 10 진수 설정 *각 계산 노드에*합니다. 최소 및 최대 *replicated_size* 에서 "최소 및 최대 값"를 참조 하는 요구 사항는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 자동 증가 옵션이 ON 이면 경우 복제 된 테이블이이 제한을 초과 하 게 허용 됩니다.  
  
 자동 증가 옵션이 OFF 이면 오류가 반환 됩니다 데이터를 기존 복제 된 테이블을 쿼리하거나 기존 업데이트 삽입 테이블 보다 더 증가 하 게 하는 방식으로 복제 사용자를 새 복제 된 테이블을 만드는 경우 *replicated_size*.  
  
 *distributed_size* [ GB ]  
 양수입니다. 분산된 테이블 (및 해당 되는 데이터)에 할당 된 총 공간에 대 한 정수 또는 10 진수 기가바이트 단위로 크기 *기기에서*합니다. 최소 및 최대 *distributed_size* 에서 "최소 및 최대 값"를 참조 하는 요구 사항는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 자동 증가 옵션이 ON 이면 하는 경우이 제한을 초과 하 게 분산된 테이블 허용 됩니다.  
  
 자동 증가 옵션이 OFF 이면 오류가 반환 됩니다 삽입 데이터를 기존 distributed 테이블을 쿼리하거나 외에도 크기를 증가 하 게 하는 방식으로 분산 된 기존 테이블을 업데이트할 사용자 분산된 새 테이블을 만들 경우 *distributed_size* .  
  
 *log_size* [GB]  
 양수입니다. 크기 (기가바이트) 정수나 10 진수 트랜잭션 로그에 대 한 *기기에서*합니다.  
  
 최소 및 최대 *log_size* 에서 "최소 및 최대 값"를 참조 하는 요구 사항는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 자동 증가 옵션이 ON 이면 로그 파일이이 제한을 초과 하 게 허용 됩니다. 사용 하 여는 [DBCC SHRINKLOG (Azure SQL 데이터 웨어하우스)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) 크기를 줄이려면 로그 파일의 원래 크기에 문의 합니다.  
  
 개별 계산 노드 외의 로그 크기를 증가 하 게 하는 모든 작업에 대 한 사용자에 게 오류가 반환 될 자동 증가 옵션이 OFF 면 *log_size*합니다.  
  
## <a name="permissions"></a>Permissions  
 필요는 **CREATE ANY DATABASE** master 데이터베이스 또는의 멤버 자격에는 권한이 **sysadmin** 고정된 서버 역할입니다.  
  
 다음 예에서는 데이터베이스 사용자 Fay에게 데이터베이스를 만들 수 있는 권한을 제공합니다.  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 데이터베이스에 대 한 수준 호환성은 데이터베이스 호환성 수준 120으로 생성 됩니다 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]합니다. 이렇게 하면는 데이터베이스를 모두 사용할 수는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] PDW 사용 하는 기능입니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 CREATE DATABASE 문은 명시적 트랜잭션에서 허용 되지 않습니다. 자세한 내용은 참조 [문을](../../t-sql/statements/statements.md)합니다.  
  
 "최소 및 최대 값" 데이터베이스에 최소 및 최대 제약 조건에 대 한 자세한 내용은 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 데이터베이스를 만드는 동시에 있어야 사용할 수 있는 충분 한 공간이 *각 계산 노드에* 다음 크기의 합계를 할당할 수:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]테이블이 있는 데이터베이스의 크기 *replicated_table_size*합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]테이블이 있는 데이터베이스의 크기 (*distributed_table_size* / 계산 노드 수)입니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로그의 크기 (*log_size* / 계산 노드 수)입니다.  
  
## <a name="locking"></a>잠금  
 데이터베이스 개체에 대 한 공유 잠금을 사용합니다.  
  
## <a name="metadata"></a>메타데이터  
 이 작업에 성공한 경우 항목이이 데이터베이스에 표시 됩니다는 [sys.databases&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 및 [sys.objects&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)메타 데이터 보기입니다.  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-basic-database-creation-examples"></a>1. Basic 데이터베이스 만들기 예제  
 다음 예제에서는 데이터베이스 `mytest` 계산 노드에 복제 된 테이블, 500GB 분산된 테이블에 대 한 어플라이언스 당 및 트랜잭션 로그에 대 한 어플라이언스 당 100 GB 당 100GB의 저장소 할당 합니다. 이 예제에서는 자동 증가 기본적으로 해제 되어 있습니다.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 다음 예제에서는 데이터베이스 `mytest` 위와 같은 동일한 매개 변수를 해당 데이터베이스가 자동 증가 제외 하 고 설정 되어 있습니다. 이렇게 하면 데이터베이스를 지정한 크기 매개 변수를 넘어 확장 합니다.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>2. 부분 기가바이트 크기를 사용 하 여 데이터베이스 만들기  
 다음 예제에서는 데이터베이스 `mytest`, 자동 증가 해제, 복제 된 테이블에 대 한 계산 노드당 1.5 g B, 분산된 테이블에 대 한 어플라이언스 당 5.25 GB 및 트랜잭션 로그에 대 한 어플라이언스 당 10GB의 저장소 할당 합니다.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER database&#40; 병렬 데이터 웨어하우스 &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
