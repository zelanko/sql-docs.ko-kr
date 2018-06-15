---
title: CREATE DATABASE(병렬 데이터 웨어하우스) | Microsoft Docs
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
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a7cef1f977e59e8145a57c806d7edaeb262b1275
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33702290"
---
# <a name="create-database-parallel-data-warehouse"></a>CREATE DATABASE(병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스에 새 데이터베이스를 만듭니다. 이 문을 사용하여 어플라이언스 데이터베이스와 관련된 모든 파일을 만들고 데이터베이스 테이블 및 트랜잭션 로그에 대한 최대 크기 및 자동 증가 옵션을 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 새 데이터베이스의 이름입니다. 허용된 데이터베이스 이름에 대한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "개체 명명 규칙" 및 "예약된 데이터베이스 이름"을 참조합니다.  
  
 AUTOGROW = ON | **OFF**  
 이 데이터베이스에 대한 *replicated_size*, *distributed_size* 및 *log_size* 매개 변수가 지정된 크기를 넘어 필요에 따라 자동으로 증가하는지 여부를 지정합니다. 기본값은 **OFF**입니다.  
  
 AUTOGROW가 ON인 경우 *replicated_size*, *distributed_size* 및 *log_size*가 각 데이터 삽입, 업데이트 또는 이미 할당된 것보다 더 많은 저장 용량이 필요한 기타 작업의 필요에 따라(지정된 초기 크기의 블록에서가 아니라) 성장하게 됩니다.  
  
 AUTOGROW가 OFF이면 크기가 자동으로 증가하지 않습니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 *replicated_size*, *distributed_size* 또는 *log_size*가 지정된 값을 초과하여 성장할 것을 요구하는 작업을 시도할 경우 오류를 반환합니다.  
  
 AUTOGROW는 모든 크기에 대해 ON이거나 OFF입니다. 예를 들어 *log_size*에 대해 AUTOGROW를 ON으로 설정하는 것이 가능하지 않지만 *replicated_size*에 대해서는 ON으로 설정하지 않습니다.  
  
 *replicated_size* [ GB ]  
 양수입니다. *각 계산 노드에서* 복제된 테이블과 해당 데이터에 할당된 총 공간에 대한 크기(정수 또는 10진 기가바이트로)를 설정합니다. 최소 및 최대 *replicated_size* 요구 사항은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "최소 및 최대 값"를 참조합니다.  
  
 AUTOGROW가 ON인 경우 복제된 테이블이 이 제한을 초과해 성장하도록 허용됩니다.  
  
 AUTOGROW가 OFF인 경우 사용자가 *replicated_size*를 초과하여 크기가 증가하는 식으로 새로 복제된 테이블을 만들고 기존 복제된 테이블에 데이터를 삽입하고 또는 기존 복제된 테이블을 업데이트하려고 하면 오류가 반환됩니다.  
  
 *distributed_size* [ GB ]  
 양수입니다. *어플라이언스 전반에 걸쳐* 복제된 테이블(및 해당 데이터)에 할당된 총 공간에 대한 정수 또는 10진 기가바이트로 표시된 크기입니다. 최소 및 최대 *distributed_size* 요구 사항은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "최소 및 최대 값"를 참조합니다.  
  
 AUTOGROW가 ON인 경우 분산된 테이블이 이 제한을 초과해 성장하도록 허용됩니다.  
  
 AUTOGROW가 OFF인 경우 사용자가 *distributed_size*를 초과하여 크기가 증가하는 식으로 새로 분산된 테이블을 만들고 기존 분산된 테이블에 데이터를 삽입하고 또는 기존 분산된 테이블을 업데이트하려고 하면 오류가 반환됩니다.  
  
 *log_size* [ GB ]  
 양수입니다. *어플라이언스 전반에 걸친* 트랜잭션 로그에 대한 크기(정수 또는 10진 기가바이트로 표시된)입니다.  
  
 최소 및 최대 *log_size* 요구 사항은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "최소 및 최대 값"를 참조합니다.  
  
 AUTOGROW가 ON인 경우 로그 파일은 이 제한을 초과하여 성장하도록 허용됩니다. [DBCC SHRINKLOG(Azure SQL 데이터 웨어하우스)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) 문을 사용하여 로그 파일의 크기를 원래 크기로 줄입니다.  
  
 AUTOGROW가 OFF인 경우 *log_size*를 초과한 개별 계산 노드에서 로그 크기를 증가시키는 모든 작업에 대해서 사용자에게 오류가 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 master 데이터베이스에서 **CREATE ANY DATABASE** 권한 또는 **sysadmin** 고정 서버 역할에서 멤버자격이 필요합니다.  
  
 다음 예에서는 데이터베이스 사용자 Fay에게 데이터베이스를 만들 수 있는 권한을 제공합니다.  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에 대한 호환성 수준인 데이터베이스 호환성 수준 120으로 데이터베이스를 만듭니다. 이렇게 하면 데이터베이스는 PDW가 사용하는 모든 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 기능을 사용할 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 명시적 트랜잭션에서는 CREATE DATABASE 문을 사용할 수 없습니다. 자세한 내용은 [문](../../t-sql/statements/statements.md)을 참조하십시오.  
  
 데이터베이스에 대한 최소 및 최대 제약 조건에 관한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 “최소 및 최대 값”을 참조합니다.  
  
 데이터베이스를 만들 경우 다음 크기의 총합계를 할당하기 위해 *각 계산 노드*에 충분히 사용할 수 있는 여유 공간이 있어야 합니다.  
  
-   *replicated_table_size* 크기의 테이블이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
-   (*distributed_table_size* / 계산 노드 수) 크기의 테이블이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
-   (*log_size* / 계산 노드 수) 크기의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그입니다.  
  
## <a name="locking"></a>잠금  
 DATABASE 개체에 대한 공유 잠금을 사용합니다.  
  
## <a name="metadata"></a>메타데이터  
 이 작업이 성공한 후 이 데이터베이스에 대한 항목이 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 및 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)메타 데이터 보기에 표시됩니다.  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]   
  
### <a name="a-basic-database-creation-examples"></a>1. 기본 데이터베이스 만들기 예제  
 다음 예제에서는 복제된 테이블에 대해 계산 노드당 100GB, 분산된 테이블에 대해 어플라이언스당 500GB, 트랜잭션 로그에 대해 어플라이언스당 100GB의 저장 용량이 있는 `mytest` 데이터베이스를 만듭니다. 이 예제에서는 AUTOGROW가 기본으로 Off로 설정돼 있습니다.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 다음 예제에서는 AUTOGROW가 켜진 경우를 제외하고 위와 동일한 매개 변수가 있는 `mytest` 데이터베이스를 만듭니다. 이렇게 하면 데이터베이스가 지정된 크기 매개 변수를 벗어나 성장할 수 있습니다.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>2. 부분 기가바이트 크기를 사용하여 데이터베이스 만들기  
 다음 예제에서는 복제된 테이블에 대해 계산 노드당 1.5GB, 분산된 테이블에 대해 어플라이언스당 5.25GB, 트랜잭션 로그에 대해 어플라이언스당 10GB의 저장 용량을 가진 그리고 AUTOGROW가 Off로 설정된 `mytest` 데이터베이스를 만듭니다.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE &#40;병렬 데이터 웨어하우스&#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
