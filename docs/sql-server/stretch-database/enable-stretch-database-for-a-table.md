---
title: "테이블에서 Stretch Database 활성화 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, enabling table
- enabling table for Stretch Database
ms.assetid: de4ac0c5-46ef-4593-a11e-9dd9bcd3ccdc
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 18ca9bfffcc53e715668634e0a59e33775c9f2c2
ms.contentlocale: ko-kr
ms.lasthandoff: 07/29/2017

---
# <a name="enable-stretch-database-for-a-table"></a>Enable Stretch Database for a table
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Stretch Database에 테이블을 구성하려면 SQL Server Management Studio에서 테이블에 대해 **늘이기 | 활성화**를 선택하여 **스트레치에 테이블 사용** 마법사를 엽니다. 또한, Transact-SQL을 사용하여 기존 테이블에서 스트레치 데이터베이스를 사용하거나 활성화된 스트레치 데이터베이스로 새 테이블을 만들 수 있습니다.  
  
-   콜드 데이터를 별도 테이블에 저장하는 경우 전체 테이블을 마이그레이션할 수 있습니다.  
  
-   테이블에 핫 데이터와 콜드 데이터가 모두 포함된 경우 필터 함수를 지정하여 마이그레이션할 행을 선택할 수 있습니다.    
 
 **필수 구성 요소**. 테이블에서 **늘이기 | 활성화** 를 선택하고 데이터베이스에서 스트레치 데이터베이스를 활성화하지 않은 경우에는, 마법사가 스트레치 데이터베이스에서 데이터베이스를 먼저 구성합니다. 이 문서의 단계 대신 [Stretch에 데이터베이스 사용 마법사를 실행하여 시작](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md) 의 단계를 따르세요.  
  
 **사용 권한**. 데이터베이스 또는 테이블에 대해 스트레치 데이터베이스를 사용하도록 설정하려면 db_owner 권한이 필요합니다. 또한, 테이블에서 스트레치 데이터베이스를 사용하려면 테이블에 대한 ALTER 권한이 필요합니다.  

 >   [!NOTE]
 > 나중에 Stretch Database를 사용하지 않도록 설정하려는 경우 테이블 또는 데이터베이스에서 Stretch Database를 사용하지 않도록 설정하면 원격 개체가 삭제되지 않습니다. 원격 테이블 또는 원격 데이터베이스를 삭제하려면 Azure 관리 포털을 사용하여 삭제해야 합니다. 원격 개체는 수동으로 삭제할 때까지 Azure 비용이 계속해서 발생합니다.
 
##  <a name="EnableWizardTable"></a> 마법사를 사용하여 테이블에서 스트레치 데이터베이스 활성화  
 **마법사 시작**  
 1.  SQL Server Management Studio의 개체 탐색기에서 스트레치를 사용하도록 설정하려는 테이블을 선택합니다.  
  
2.  마우스 오른쪽 단추로 클릭하고 **스트레치**를 선택하고 **사용** 을 선택하여 마법사를 시작합니다.  
  
 **소개**  
 마법사의 용도 및 필수 구성 요소를 검토합니다.  
  
 **데이터베이스 테이블 선택**  
 사용하려는 테이블이 표시되고 선택되었는지 확인합니다.  
  
 전체 테이블을 마이그레이션하거나 마법사에서 간단한 필터 함수를 지정할 수 있습니다. 다른 유형의 필터 함수를 사용하여 마이그레이션할 행을 선택하려면 다음 중 하나를 수행합니다.  
  
-   마법사를 종료하고 ALTER TABLE 문을 실행하여 테이블에 대해 스트레치를 사용하도록 설정하고 필터 함수를 지정합니다.  
  
-   마법사를 종료한 후 ALTER TABLE 문을 실행하여 필터 함수를 지정합니다. 필수 단계는 [마법사를 실행한 후 필터 함수 추가](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz)를 참조하세요.  
  
 ALTER TABLE 구문은 이 항목의 뒷부분에 설명되어 있습니다.  
  
 **요약**  
 마법사에서 선택한 옵션과 입력한 값을 검토합니다. 그런 다음 **마침** 을 선택하여 스트레치를 사용하도록 설정합니다.  
  
 **결과**  
 결과를 검토합니다.  
  
##  <a name="EnableTSQLTable"></a> Transact-SQL을 사용하여 테이블에서 스트레치 데이터베이스 활성화  
 또한, Transact-SQL을 사용하여 기존 테이블에서 스트레치 데이터베이스를 사용하거나 활성화된 스트레치 데이터베이스로 새 테이블을 만들 수 있습니다.  
  
### <a name="options"></a>옵션  
 CREATE TABLE 또는 ALTER TABLE을 실행하여 테이블에서 스트레치 데이터베이스를 사용하는 경우 다음 옵션을 사용합니다.  
  
-   선택 사항으로, 테이블에 핫 및 콜드 데이터가 모두 포함된 경우 `FILTER_PREDICATE = <function>` 절을 사용하여 함수를 지정해 마이그레이션할 행을 선택할 수 있습니다. 조건자는 인라인 테이블 반환 함수를 호출해야 합니다. 자세한 내용은 [필터 함수를 사용하여 마이그레이션할 행 선택](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)을 참조하세요. 필터 함수를 지정하지 않으면 전체 테이블이 마이그레이션됩니다.  
  
    > [!IMPORTANT]  
    >  제대로 수행되지 않는 필터 함수를 제공하면 데이터 마이그레이션 성능도 저하됩니다. 스트레치 데이터베이스는 CROSS APPLY 연산자를 사용하여 테이블에 필터 함수를 적용합니다.  
  
-   `MIGRATION_STATE = OUTBOUND` 을(를) 지정하여 즉시 마이그레이션을 시작하거나  `MIGRATION_STATE = PAUSED` 을(를) 지정하여 데이터 마이그레이션의 시작을 연기합니다.  
  
### <a name="enable-stretch-database-for-an-existing-table"></a>기존 테이블에서 스트레치 데이터베이스 활성화  
 스트레치 데이터베이스용으로 기존 데이터베이스를 구성하려면 ALTER TABLE 명령을 실행합니다.  
  
 전체 테이블을 마이그레이션하고 즉시 마이그레이션을 시작하는 예제는 다음과 같습니다.  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 `dbo.fn_stretchpredicate` 인라인 테이블 반환 함수에 의해 식별된 행만 마이그레이션하고 데이터 마이그레이션을 연기하는 예제는 다음과 같습니다. 필터 함수에 대한 자세한 내용은 [필터 함수를 사용하여 마이그레이션할 행 선택](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)을 참조하세요.  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
 GO
```  
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
### <a name="create-a-new-table-with-stretch-database-enabled"></a>활성화된 스트레치 데이터베이스에서 새 테이블 만들기  
 활성화된 스트레치 데이터베이스에서 새 테이블을 만들려면 CREATE TABLE 명령을 실행합니다.  
  
 전체 테이블을 마이그레이션하고 즉시 마이그레이션을 시작하는 예제는 다음과 같습니다.  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name>
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 `dbo.fn_stretchpredicate` 인라인 테이블 반환 함수에 의해 식별된 행만 마이그레이션하고 데이터 마이그레이션을 연기하는 예제는 다음과 같습니다. 필터 함수에 대한 자세한 내용은 [필터 함수를 사용하여 마이그레이션할 행 선택](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)을 참조하세요.  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name> 
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
GO  
```  
  
 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
  

