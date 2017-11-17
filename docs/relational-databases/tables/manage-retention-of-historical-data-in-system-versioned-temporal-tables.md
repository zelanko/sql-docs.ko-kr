---
title: "시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리 | Microsoft 문서"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7925ebef-cdb1-4cfe-b660-a8604b9d2153
caps.latest.revision: 23
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 08416515a890c5e1f2775afa436ed3bcb4bb0bd7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="manage-retention-of-historical-data-in-system-versioned-temporal-tables"></a>시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  시스템 버전 관리된 임시 테이블에서 기록 테이블은 특히 다음과 같은 상황에서 일반 테이블보다 데이터베이스 크기를 좀 더 크게 늘릴 수 있습니다.  
  
-   기록 데이터를 오랫동안 보관  
  
-   업데이트가 있거나 과도한 데이터 수정 패턴을 삭제함  
  
 크기가 크고 점점 증가하는 기록 테이블은 기본 저장소 비용과 임시 쿼리에 대한 성능 세금 부과로 인해 문제가 발생할 수 있습니다. 따라서 기록 테이블에서 데이터를 관리하기 위한 데이터 보존 정책을 개발하는 것이 모든 임시 테이블의 수명 주기 계획 및 관리의 중요한 요소입니다.  
  
## <a name="data-retention-management-for-history-table"></a>기록 테이블에 대한 데이터 보존 관리  
 임시 테이블 데이터 보존 관리는 각 임시 테이블에 대한 필수 보존 기간을 결정하는 것부터 시작됩니다. 대부분의 경우 보존 정책은 임시 테이블을 사용하는 응용 프로그램의 비즈니스 논리의 일부로 간주해야 합니다. 예를 들어 데이터 감사와 시간 이동 시나리오에서 응용 프로그램은 온라인 쿼리에 사용할 수 있는 기록 데이터의 기간 측면에서 확실하게 요구되는 사항이 있습니다.  
  
 데이터 보존 기간을 결정하고 나면 그 다음으로 기록 데이터 저장 방법과 저장 위치, 그리고 요구되는 보존 기간보다 오래된 기록 데이터를 삭제하는 방법 등 기록 데이터를 관리하기 위한 계획을 개발합니다. 다음 네 가지 방법으로 임시 기록 테이블에서 기록 데이터를 관리할 수 있습니다.  
  
-   [스트레치 데이터베이스](https://msdn.microsoft.com/library/mt637341.aspx#using-stretch-database-approach)  
  
-   [테이블 분할](https://msdn.microsoft.com/library/mt637341.aspx#using-table-partitioning-approach)  
  
-   [사용자 지정 정리 스크립트](https://msdn.microsoft.com/library/mt637341.aspx#using-custom-cleanup-script-approach)  

-   [보존 정책](https://msdn.microsoft.com/library/mt637341.aspx#using-temporal-history-retention-policy-approach)  

 기록 데이터 문제 완화 또는 정리를 위한 논리는 이 방법 중 한 가지를 사용하며 현재 테이블에서 기간 종료에 해당하는 열을 기반으로 합니다. 각 행에 대해 기간 값의 끝에서는 행 버전이 "닫힌" 상태가 되는, 즉 기록 테이블에서 해당 값이 처음 삽입되는 순간을 결정합니다. 예를 들어 조건 `SysEndTime < DATEADD (DAYS, -30, SYSUTCDATETIME ())` 은1개월보다 오래된 기록 데이터를 기록 테이블에서 제거하거나 제외해야 한다고 지정합니다.  
  
> **참고:**  이 항목의 예제에서는 이 [임시 테이블 예제](creating-a-system-versioned-temporal-table.md)를 사용합니다.  
  
## <a name="using-stretch-database-approach"></a>스트레치 데이터베이스 접근 방식 사용  
  
> **참고:**  Stretch Database 접근 방식 사용은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에만 적용되며 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]에는 적용되지 않습니다.  
  
 [스트레치 데이터베이스](../../sql-server/stretch-database/stretch-database.md) 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 Azure로 기록 데이터를 투명하게 마이그레이션합니다. 추가 보안을 위해 SQL Server의 [항상 암호화](https://msdnstage.redmond.corp.microsoft.com/library/mt163865.aspx) 기능을 사용하여 동작에 대한 데이터를 암호화할 수 있습니다. 또한 데이터 보호를 위해 [행 수준 보안](../../relational-databases/security/row-level-security.md) 및 기타 고급 SQL Server 보안 기능을 임시 및 스트레치 데이터베이스와 함께 사용할 수 있습니다.  
  
 스트레치 데이터베이스 접근 방식을 사용하면 기록 데이터 일부 또는 전체를 Azure에 스트레치할 수 있으며 SQL Server에서 Azure로 기록 데이터를 자동으로 옮깁니다. 기록 테이블에서 스트레치를 사용하도록 설정한다고 해서 데이터 수정 및 임시 쿼리 측면에서 임시 테이블을 조작하는 방식이 변경되는 것은 아닙니다.  
  
-   **전체 기록 테이블 스트레치:** 주 시나리오에서 기록 데이터에서 데이터 변경 빈도가 높은 반면 쿼리는 상대적으로 드문 환경에서 데이터 감사를 수행할 경우 전체 기록 테이블에 대해 스트레치 데이터베이스를 구성합니다.  즉, 임시 쿼리 작업의 성능이 중요하지 않은 경우 이 방법을 사용합니다. 이 경우 Azure에서 제공하는 비용 효율성이 매력적일 수 있습니다.   
    전체 기록 테이블을 스트레치할 때 스트레치 마법사 또는 TRANSACT-SQL을 사용할 수 있습니다. 두 방법에 대한 예는 아래에 표시됩니다.  
  
-   **일부 기록 테이블 스트레치:** 주 시나리오에서 최근 기록 데이터를 주로 쿼리하지만 필요할 경우 이전 기록 데이터를 저렴한 비용으로 원격 저장하면서 쿼리하는 옵션을 유지하려고 할 경우 성능 개선을 위해 기록 테이블의 일부에 대해서만 스트레치 데이터베이스를 구성합니다. TRANSACT-SQL을 사용하면 전체 행을 마이그레이션하지 않고 기록테이블에서 마이그레이션할 행을 선택할 수 있도록 조건자 함수를 지정하여 이 작업을 수행할 수 있습니다.  임시 테이블에서 작업 시 일반적으로 시간 조건을 기준으로 데이터를 이동하는 것이 좋습니다(예: 기록 테이블의 행 버전 보존 기간 기준)    
    결정적 조건자 함수를 사용하면 현재 데이터가 있는 동일한 데이터베이스에서 기록의 일부를 보관하고 나머지는 Azure로 마이그레이션할 수 있습니다.    
    예제 및 제한 사항에 대한 자세한 내용은 [필터 함수를 사용하여 마이그레이션할 행 선택(Stretch Database)](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)을 참조하세요. 비결정적인 함수는 유효하지 않으므로 슬라이딩 윈도우 방식으로 기록 데이터를 전송하려는 경우에는 로컬로 보관할 행의 창이 보관 기간 측면에서 일정하도록 인라인 조건자 함수 정의를 지속적으로 변경해야 합니다. 슬라이딩 윈도우를 사용하면 1개월이 지난 기록 데이터를 지속적으로 Azure로 이동할 수 있습니다. 이 접근 방법의 예는 아래에 표시됩니다.  
  
> **참고:** Stretch Database는 데이터를 Azure로 마이그레이션합니다. 따라서 대금 청구를 위해 Azure 계정 및 구독이 있어야 합니다. Azure 무료 평가판 계정을 얻으려면 [1개월 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 클릭하세요.  
  
 스트레치 마법사 또는 TRANSACT-SQL을 사용하여 스트레치를 위해 임시 기록 테이블을 구성할 수 있으며 시스템 버전 관리가 **ON**으로 설정되어 있어도 임시 기록 테이블에 스트레치를 사용하도록 설정할 수 있습니다. 현재 테이블을 스트레치하는 것은 의미가 없으므로 허용되지 않습니다.  
  
### <a name="using-the-stretch-wizard-to-stretch-the-entire-history-table"></a>스트레치 마법사를 사용하여 전체 기록 테이블 스트레치  
 초보자를 위한 가장 쉬운 방법은 스트레치 마법사를 사용하여 전체 데이터베이스에 대해 스트레치를 사용하도록 설정한 다음 스트레치 마법사 내에서 임시 기록 테이블을 선택 하는 것입니다(이 예에서는 다른 빈 데이터베이스에서 Department 테이블을 시스템 버전 관리된 임시 테이블로 구성했다고 가정). [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서는 임시 기록 테이블 자체를 마우스 오른쪽 단추로 클릭하고 스트레치를 클릭할 수 없습니다.  
  
1.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**, **스트레치**를 차례로 클릭하고 **사용** 을 클릭하여 마법사를 시작합니다.  
  
2.  **테이블 선택** 창에서 임시 기록 테이블에 대한 확인란을 선택하고 다음을 클릭합니다.  
  
     ![테이블 선택 페이지에서 기록 테이블 선택](../../relational-databases/tables/media/stretch-wizard-2-for-temporal.png "테이블 선택 페이지에서 기록 테이블 선택")  
  
3.  **Azure 구성** 창에서 로그인 자격 증명을 제공합니다. Microsoft Azure에 로그인하거나 계정을 등록합니다. 사용할 구독을 선택하고 Azure 지역을 선택합니다. 그런 다음 새 서버를 만들거나 기존 서버를 선택합니다. **다음**을 클릭합니다.  
  
     ![새 Azure 서버 만들기 - Stretch Database 마법사](../../relational-databases/tables/media/stretch-wizard-4.png "새 Azure 서버 만들기 - Stretch Database 마법사")  
  
4.  **보안 자격 증명** 창에서 원본 SQL Server 데이터베이스 자격 증명을 보호하기 위해 데이터베이스 마스터 키에 대한 암호를 제공하고 다음을 클릭합니다.  
  
     ![Stretch Database 마법사의 보안 자격 증명 페이지](../../relational-databases/tables/media/stretch-wizard-6.png "Stretch Database 마법사의 보안 자격 증명 페이지")  
  
5.  **선택 IP 주소** 창에서 Azure 서버가 SQL Server와 통신할 수 있도록 SQL Server에 대한 IP 주소 범위를 제공합니다. 방화벽 규칙이 이미 있는 기존 서버를 선택한 경우 여기서 다음을 클릭하기만 하면 기존 방화벽 규칙을 사용할 수 있습니다. **다음** 을 클릭하고 **마침** 을 클릭하여 스트레치 데이터베이스를 사용하도록 설정한 다음 임시 기록 테이블을 스트레치합니다.  
  
     ![Stretch Database 마법사의 IP 주소 선택 페이지](../../relational-databases/tables/media/stretch-wizard-7.png "Stretch Database 마법사의 IP 주소 선택 페이지")  
  
6.  마법사가 완료되면 데이터베이스에 스트레치가 사용하도록 설정되었는지 확인합니다. 개체 탐색기에서 데이터베이스가 스트레치되었는지 나타내는 아이콘을 살펴봅니다.  
  
> **참고:** 스트레치에 데이터베이스 사용이 실패하는 경우 오류 로그를 검토하세요. 일반적으로 방화벽 규칙을 잘못 구성했을 때 오류가 발생합니다.  
  
 참고 항목:  
  
-   [데이터베이스에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)  
  
-   [Stretch에 데이터베이스 사용 마법사를 실행하여 시작](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)  
  
-   [테이블에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
### <a name="using-transact-sql-to-stretch-the-entire-history-table"></a>Transact-SQL을 사용하여 전체 기록 테이블 스트레치  
 Transact-SQL을 사용하여 로컬 서버에서 스트레치를 사용하도록 설정하고 [데이터베이스에 대해 스트레치 데이터베이스를 사용](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)하도록 설정할 수 있습니다. 그런 다음  [TRANSACT-SQL을 사용하여 테이블에서 스트레치 데이터베이스를 사용하도록 설정](https://msdn.microsoft.com/library/mt605115.aspx#Anchor_1)할 수 있습니다. 스트레치 데이터베이스에 대해 이전에 사용하도록 설정된 데이터베이스를 사용하여 기존 시스템 버전 관리된 임시 기록 테이블을 스트레치할 수 있도록 다음 Transact-SQL 스크립트를 실행합니다.  
  
```  
ALTER TABLE <history table name>   
SET (REMOTE_DATA_ARCHIVE = ON (MIGRATION_STATE = OUTBOUND));  
```  
  
### <a name="using-transact-sql-to-stretch-a-portion-of-the-history-table"></a>Transact-SQL을 사용하여 일부 기록 테이블 스트레치  
 기록 테이블 중 일부만 스트레치하려면 [인라인 조건자 함수](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)를 만들어 시작합니다. 이 예에서는 2015년 12월 1일에 처음으로 인라인 조건자 함수를 구성하고 2015년 11월 1일보다 오래된 모든 기록 날짜를 Azure로 스트레치한다고 가정합니다. 이 작업 수행을 위해 다음 함수를 만들기 시작합니다.  
  
```  
CREATE FUNCTION dbo.fn_StretchBySystemEndTime20151101(@systemEndTime datetime2)   
RETURNS TABLE   
WITH SCHEMABINDING    
AS    
RETURN SELECT 1 AS is_eligible   
  WHERE @systemEndTime < CONVERT(datetime2, '2015-11-01T00:00:00', 101) ;  
```  
  
 다음 작업으로, 다음 스크립트를 사용하여 필터 조건자를 기록 테이블에 추가하고 마이그레이션 상태를 OUTBOUND로 설정하여 기록 테이블에 대해 조건자 기반 데이터 마이그레이션을 사용하도록 설정합니다.  
  
```  
ALTER TABLE <history table name>   
SET (   
        REMOTE_DATA_ARCHIVE = ON   
                (   
                        FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20151101 (SysEndTime)  
                                , MIGRATION_STATE = OUTBOUND   
                )  
        )   
;  
```  
  
 슬라이딩 윈도우 방식을 유지하려면 조건자 함수를 매일 정확하게 조정해야 합니다(즉, 1일을 기준으로 매일 행 필터링 조건 변경). 다음 스크립트는 2015년 12월 2일에 실행해야 하는 스크립트입니다.  
  
```  
BEGIN TRAN  
           /*(1) Create new predicate function definition */  
        CREATE FUNCTION dbo.fn_StretchBySystemEndTime20151102(@systemEndTime datetime2)  
        RETURNS TABLE  
        WITH SCHEMABINDING   
        AS   
        RETURN SELECT 1 AS is_eligible  
               WHERE @systemEndTime < CONVERT(datetime2,'2015-11-02T00:00:00', 101)  
        GO  
  
        /*(2) Set the new function as filter predicate */  
        ALTER TABLE <history table name>  
        SET   
        (  
               REMOTE_DATA_ARCHIVE = ON  
               (  
                       FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20151102(SysEndTime),  
                       MIGRATION_STATE = OUTBOUND  
               )  
        )   
COMMIT ;  
```  
  
 SQL Server 에이전트 또는 일부 다른 예약 메커니즘을 사용하여 조건자 함수 정의가 항상 유효한지 확인합니다.  
  
## <a name="using-table-partitioning-approach"></a>테이블 분할 접근 방법 사용  
 [테이블 분할](../partitions/create-partitioned-tables-and-indexes.md) 을 사용하면 큰 테이블을 좀 더 관리 및 확장할 수 있습니다. 테이블 분할 방법으로 기록 테이블 파티션을 사용하여 시간 조건을 기반으로 오프라인으로 보관하거나 사용자 지정 데이터를 정리할 수 있습니다. 또한 테이블 분할을 통해 데이터 기록 하위 집합에서 임시 테이블을 쿼리할 때 파티션 제거를 사용하여 성능이 향상될 수도 있습니다.  
  
 테이블 분할 기능을 사용하면 슬라이딩 윈도우 접근 방식을 구현하여 필수 보존 기간에 맞게 데이터를 기록 테이블에서 유지 관리하면서도 기록 테이블에서 가장 오래된 기록 데이터 일부를 이동하여 제외시키고, 기간 측면에서 보관 부분의 크기를 지속적으로 유지할 수 있습니다. SYSTEM_VERSIONING이 ON이더라도 기록 테이블의 데이터를 외부로 전환하는 작업은 지원됩니다. 즉 유지 관리 창을 도입하거나 정기 작업을 차단하지 않고 기록 데이터의 일부를 정리할 수 있습니다.  
  
> **참고:** 파티션 전환 작업을 수행하려면 기록 테이블에서 클러스터형 인덱스를 분할 스키마에 정렬해야 합니다(SysEndTime 포함 필수). 시스템에서 만든 기본 기록 테이블에는 SysEndTime 및 SysStartTime 열이 포함된 클러스터형 인덱스가 있어 분할, 새 기록 데이터 삽입, 일반적인 임시 쿼리 작업에 적합합니다. 자세한 내용은 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)을 참조하세요.  
  
 슬라이딩 윈도우 방식에서는 다음 두 가지 작업을 수행해야 합니다.  
  
-   분할 구성 작업  
  
-   반복적인 파티션 유지 관리 작업  
  
 아래 그림의 경우 6개월 동안에 대한 기록 데이터를 보관하고 월별 데이터를 별도의 파티션으로 유지한다고 가정합니다. 또한 2015년 9월에 시스템 버전 관리를 활성화했다고 가정해 보겠습니다.  
  
 분할 구성 작업으로 기록 테이블에 대한 초기 분할 구성이 만들어집니다. 이 예제의 경우 월별로 슬라이딩 윈도우 크기와 동일한 개수의 파티션과, 미리 준비된 한 개의 추가 빈 파티션(아래에 설명)을 만듭니다. 이 구성을 통해 처음으로 반복적인 파티션 유지 관리 작업을 시작할 때 시스템에서 새 데이터를 제대로 저장할 수 있게 되며, 파티션을 데이터로 분할하지 않아 데이터 이동으로 인한 높은 비용이 발생하지 않습니다. 이 작업은 아래의 예제 스크립트로 TRANSACT-SQL을 사용하여 이 작업을 수행해야 합니다.  
  
 다음 그림은 6개월 분량의 데이터 보관을 위한 초기 분할 구성을 보여 줍니다.  
  
 ![분할](../../relational-databases/tables/media/partitioning.png "분할")  
  
> **참고:** 분할 구성 시 RANGE LEFT와 RANGE RIGHT를 사용할 때 성능에 미치는 영향에 대한 자세한 내용은 아래의 테이블 분할 시 성능 고려 사항을 참조하세요.  
  
 첫 번째 및 마지막 파티션은 각각 위쪽 경계와 아래쪽 경계에 “열린” 상태로 유지됩니다. 이렇게 하면 분할 열 값에 상관없이 모든 새 행에 대상 파티션이 포함됩니다.   
시간이 지남에 따라 기록 테이블의 새 행은 더 높은 파티션에 순서대로 삽입됩니다. 6번째 파티션이 채워지면 대상으로 지정된 보존 기간에 도달합니다. 이 순간에 반복적인 파티션 유지 관리 작업이 처음으로 시작됩니다(이 예에서는 한 달에 한 번 정기적으로 실행하도록 예약해야 합니다).  
  
 다음 그림은 반복적인 파티션 유지 관리 작업을 보여 줍니다(자세한 단계는 아래 참조).  
  
 ![Partitioning2](../../relational-databases/tables/media/partitioning2.png "Partitioning2")  
  
 반복적인 파티션 유지 관리 작업 단계는 아래와 같습니다.  
  
1.  전환: 준비 테이블을 만든 다음 SWITCH PARTITION 인수를 사용하여 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 문에서 기록 테이블과 준비 테이블 사이에서 파티션을 전환합니다(예 C. 테이블 간 파티션 전환 참조).  
  
    ```  
    ALTER TABLE <history table> SWITCH PARTITION 1 TO <staging table>  
    ```  
  
     파티션 전환 후에는 준비 테이블에서 데이터를 선택적으로 보관한 다음 준비 테이블을 삭제하거나 잘라 그 다음에 수행할 반복적인 파티션 유지 관리 작업 준비를 할 수 있습니다.  
  
2.  MERGE RANGE: [ALTER PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)에서 MERGE RANGE를 사용하여 빈 파티션 1을 파티션 2와 병합합니다(예 B 참조). 이 함수를 사용하여 가장 낮은 경계를 제거함으로써 빈 파티션 1을 기존의 파티션 2와 효율적으로 병합하여 새 파티션 1을 생성합니다. 다른 파티션도 효과적으로 서수가 변경됩니다.  
  
3.  SPLIT RANGE: [ALTER PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)에서 SPLIT RANGE를 사용하여 새 빈 파티션 7을 만듭니다(예 A 참조). 이 함수를 사용하여 새 상한 경계를 추가함으로써 다음 달에 대한 별도의 파티션을 효율적으로 만듭니다.  
  
### <a name="use-transact-sql-to-create-partitions-on-history-table"></a>TRANSACT-SQL을 사용하여 기록 테이블에서 파티션 만들기  
 아래 코드 창에서 TRANSACT-SQL 스크립트를 사용하여 파티션 함수, 파티션 스키마를 만들고, 파티션 스키마에 파티션이 정렬되도록 클러스터형 인덱스를 다시 만듭니다. 이 예에서는 2015년 9월부터 시작하는 월별 파티션을 사용하여 6개월의 슬라이딩 윈도우 방식을 만들겠습니다.  
  
```  
BEGIN TRANSACTION  
  
        /*Create partition function*/  
        CREATE PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime] (datetime2(7))   
                    AS RANGE LEFT FOR VALUES   
                                (N'2015-09-30T23:59:59.999'  
                                , N'2015-10-31T23:59:59.999'  
                                , N'2015-11-30T23:59:59.999'  
                                , N'2015-12-31T23:59:59.999'  
                                , N'2016-01-31T23:59:59.999'  
                                , N'2016-02-29T23:59:59.999')  
  
        /*Create partition scheme*/  
        CREATE PARTITION SCHEME [sch_Partition_DepartmentHistory_By_SysEndTime]   
                        AS PARTITION [fn_Partition_DepartmentHistory_By_SysEndTime]   
                        TO ([PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY])  
  
        /*Re-create index to be partition-aligned with the partitioning schema*/  
        CREATE CLUSTERED INDEX [ix_DepartmentHistory] ON [dbo].[DepartmentHistory]  
        (  
                    [SysEndTime] ASC,  
                    [SysStartTime] ASC  
        )  
            WITH   
                        (PAD_INDEX = OFF  
                        , STATISTICS_NORECOMPUTE = OFF  
                        , SORT_IN_TEMPDB = OFF  
                        , DROP_EXISTING = ON  
                        , ONLINE = OFF  
                        , ALLOW_ROW_LOCKS = ON  
                        , ALLOW_PAGE_LOCKS = ON  
                        , DATA_COMPRESSION = PAGE)  
            ON [sch_Partition_DepartmentHistory_By_SysEndTime] ([SysEndTime])  
  
COMMIT TRANSACTION;  
  
```  
  
### <a name="using-transact-sql-to-maintain-partitions-in-sliding-window-scenario"></a>Transact-SQL을 사용하여 슬라이딩 윈도우 시나리오에서 파티션 유지 관리  
 아래 코드 창에서 TRANSACT-SQL 스크립트를 사용하여 슬라이딩 윈도우 시나리오에서 파티션을 유지 관리합니다. 이 예에서는 MERGE RANGE를 사용하여 2015년 9월에 해당하는 파티션을 외부로 전환한 다음 SPLIT RANGE를 사용하여 2016년 3월에 해당하는 새 파티션을 추가합니다.  
  
```  
BEGIN TRANSACTION  
  
         /*(1)  Create staging table */  
         CREATE TABLE [dbo].[staging_DepartmentHistory_September_2015]  
        (  
                 [DeptID] [int] NOT NULL  
                 , [DeptName] [varchar](50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
                 , [ManagerID] [int] NULL  
                 ,  [ParentDeptID] [int] NULL  
                 ,  [SysStartTime] [datetime2](7) NOT NULL  
                 ,  [SysEndTime] [datetime2](7) NOT NULL  
         ) ON [PRIMARY]  
         WITH  
         (  
              DATA_COMPRESSION = PAGE  
         )  
  
         /*(2) Create index on the same filegroups as the partition that will be switched out*/  
         CREATE CLUSTERED INDEX [ox_staging_DepartmentHistory_September_2015]    
         ON [dbo].[staging_DepartmentHistory_September_2015]  
         (  
                  [SysEndTime] ASC,  
                  [SysStartTime] ASC  
         )  
      WITH   
          (  
               PAD_INDEX = OFF  
               , SORT_IN_TEMPDB = OFF  
               , DROP_EXISTING = OFF  
               , ONLINE = OFF  
               , ALLOW_ROW_LOCKS = ON  
               , ALLOW_PAGE_LOCKS = ON  
          )   
         ON [PRIMARY]  
  
         /*(3) Create constraints matching the partition that will be switched out*/  
         ALTER TABLE [dbo].[staging_DepartmentHistory_September_2015]  WITH CHECK   
               ADD  CONSTRAINT [chk_staging_DepartmentHistory_September_2015_partition_1]   
                    CHECK  ([SysEndTime]<=N'2015-09-30T23:59:59.999')  
         ALTER TABLE [dbo].[staging_DepartmentHistory_September_2015]   
               CHECK CONSTRAINT [chk_staging_DepartmentHistory_September_2015_partition_1]  
  
         /*(4) Switch partition to staging table*/  
         ALTER TABLE [dbo].[DepartmentHistory]   
         SWITCH PARTITION 1 TO [dbo].[staging_DepartmentHistory_September_2015]   
         WITH (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 MINUTES, ABORT_AFTER_WAIT = NONE))  
  
         /*(5) [Commented out] Optionally archive the data and drop staging table  
         INSERT INTO [ArchiveDB].[dbo].[DepartmentHistory]   
         SELECT * FROM [dbo].[staging_DepartmentHistory_September_2015];  
         DROP TABLE [dbo].[staging_DepartmentHIstory_September_2015];  
         */  
  
         /*(6) merge range to move lower boundary one month ahead*/  
         ALTER PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime]()   
               MERGE RANGE(N'2015-09-30T23:59:59.999')  
  
         /*(7) Create new empty partition for "April and after" by creating new boundary point and specifying NEXT USED file group*/  
         ALTER PARTITION SCHEME [sch_Partition_DepartmentHistory_By_SysEndTime] NEXT USED [PRIMARY]  
         ALTER PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime]() SPLIT RANGE(N'2016-03-31T23:59:59.999')  
  
COMMIT TRANSACTION  
  
```  
  
 위의 스크립트를 약간만 수정하여 다음과 같이 정기적인 월별 유지 관리 프로세스에서 사용할 수 있습니다.  
  
1.  단계 (1)에서는 제거할 달에 대한 새 준비 테이블을 만듭니다(위 예에서 10월이 그 다음 달에 해당)  
  
2.  단계 (3)에서는 제거할 데이터의 월에 일치하는 제약 조건을 만들고 검사합니다(10월 파티션에 대해 `[SysEndTime]<=N'2015-10-31T23:59:59.999'` ).  
  
3.  단계 (4)에서는 파티션 1을 새로 만든 준비 테이블로 전환합니다.  
  
4.  단계 (6)에서는 하한 경계를 병합하여 파티션 함수를 변경합니다(10월에 대한 데이터를 이동하여 제외한 후 `MERGE RANGE(N'2015-10-31T23:59:59.999'` ).  
  
5.  단계 (7)에서는 새 상한 경계를 만드는 파티션 함수를 분리합니다(10월에 대한 데이터를 이동하여 제외한 후 `SPLIT RANGE (N'2016-04-30T23:59:59.999'` ).  
  
 그러나 최적의 솔루션은 스크립트를 수정하지 않고 매월 적절한 작업을 수행할 수 있도록 일반 TRANSACT-SQL 스크립트를 정기적으로 실행하는 것입니다. 제공된 매개 변수(병합해야 할 하한 경계와 파티션 분할로 만들어지는 새 경계)로 동작을 수행하도록 위 스크립트를 일반화할 수도 있습니다. 매달 준비 테이블 생성을 방지하기 위해 사전에 미리 테이블을 만들고 전환할 파티션과 일치하도록 확인 제약 조건을 변경하여 다시 사용할 수 있습니다. 다음 페이지를 살펴보고 TRANSACT-SQL 스크립트를 사용하여 [슬라이딩 윈도우를 완전히 자동화할 수 있는 방법](https://msdn.microsoft.com/library/aa964122.aspx) 에 대한 아이디어를 얻어보세요.  
  
### <a name="performance-considerations-with-table-partitioning"></a>테이블 분할 시 성능 고려 사항  
 데이터 이동 시 발생되는 성능 오버헤드가 상당할 수 있으므로 데이터 이동을 방지하도록 범위 병합 및 범위 분할 작업을 수행하는 것이 중요합니다. 자세한 내용은 [파티션 함수 수정](../../relational-databases/partitions/modify-a-partition-function.md)을 참조하세요. 이 작업은 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md) 작업 시 RANGE RIGHT보다는 RANGE LEFT를 사용하여 수행합니다.  
  
 먼저 시각적으로 RANGE LEFT 및 RANGE RIGHT 옵션의 의미에 대해 시각적으로 설명해 보겠습니다.  
  
 ![Partitioning3](../../relational-databases/tables/media/partitioning3.png "Partitioning3")  
  
 파티션 함수를 RANGE LEFT로 정의하면 지정된 값은 파티션 상한이 됩니다. RANGE RIGHT를 사용하면 지정된 값은 파티션 하한이 됩니다. MERGE RANGE를 사용하여 파티션 정의 범위에서 경계를 제거할 경우 기본적으로 경계가 포함된 파티션도 제거되도록 구현됩니다. 해당 파티션이 비어 있지 않으면 데이터는 MERGE RANGE 작업의 결과로 생성되는 파티션으로 이동합니다.  
  
 슬라이딩 윈도우 시나리오에서는 항상 가장 낮은 파티션 경계를 제거합니다.  
  
-   RANGE LEFT 사례: RANGE LEFT의 경우, 가장 낮은 파티션 경계가 파티션 전환 후 비어 있는 파티션 1에 속하여 MERGE RANGE로 데이터 이동이 발생되지 않습니다.  
  
-   RANGE RIGHT 사례: RANGE RIGHT의 경우, 전환을 통해 파티션 1이 비었다고 가정하므로 가장 낮은 파티션 경계가 비어 있지 않은 파티션 2에 속합니다. 이 경우 MERGE RANGE에서 데이터 이동이 발생합니다. 즉 파티션 2의 데이터가 파티션 1로 이동합니다. 이 문제를 방지하려면 슬라이딩 윈도우 시나리오에서 RANGE RIGHT에는 항상 빈 상태인 파티션 1이 있어야 합니다. 다시 말하면 RANGE RIGHT를 사용할 경우 RANGE LEFT 경우와 비교되는 추가 파티션을 하나 만들어 유지 관리해야 합니다.  
  
 결론: 슬라이딩 파티션에서 RANGE LEFT를 사용하면 파티션 관리가 훨씬 간단해지고 데이터 이동이 발생하지 않습니다. 하지만 RANGE RIGHT를 사용하여 파티션 경계를 정의하는 것이 datetime 시간 틱 문제를 처리하지 않아도 되므로 좀 더 간단합니다.  
  
## <a name="using-custom-cleanup-script-approach"></a>사용자 지정 정리 스크립트 방식 사용  
 스트레치 데이터베이스 및 테이블 분할 방식이 실행 가능한 옵션이 아닐 경우 세 번째로 사용자 지정 정리 스크립트를 사용하여 기록 데이터에서 데이터를 삭제하는 방법이 있습니다. **SYSTEM_VERSIONING = OFF**일 경우에만 기록 테이블에서 데이터를 삭제할 수 있습니다. 데이터 불일치를 방지하기 위해서는 유지 관리 창(데이터 수정 작업이 활성 상태가 아닌 경우) 또는 트랜잭션(효율적으로 다른 작업 차단) 내에서 정리를 수행해야 합니다.  이 작업을 수행하려면 현재 및 기록 테이블에 **CONTROL** 권한이 있어야 합니다.  
  
 일반 응용 프로그램 및 사용자 쿼리를 최소한으로 차단하려면 트랜잭션 내에서 정리 스크립트를 수행할 때 지연을 두고 더 작은 청크로 데이터를 삭제합니다. 모든 시나리오에서 삭제할 각 데이터 청크에 적합한 크기는 없지만 단일 트랜잭션에서 10,000개 이상의 행을 삭제하면 상당한 영향을 미칠 수 있습니다.  
  
 정리 논리는 모든 임시 테이블에서 동일합니다. 따라서 데이터 기록을 제한하려는 모든 임시 테이블에 대해 정기적인 실행이 예약된 일반 저장 프로시저를 통해 비교적 쉽게 자동화할 수 있습니다.  
  
 다음 다이어그램에서는 실행 중인 작업에 미치는 영향을 줄이기 위해 단일 테이블에 대해 정리 논리를 구성하는 방식을 보여 줍니다.  
  
 ![CustomCleanUpScriptDiagram](../../relational-databases/tables/media/customcleanupscriptdiagram.png "CustomCleanUpScriptDiagram")  
  
 다음은 프로세스의 구현을 위한 높은 수준의 몇 가지 지침입니다. 정리 논리를 매일 실행하고 데이터 정리에 필요한 모든 임시 테이블에서 반복될 수 있게 예약합니다. SQL Server 에이전트 또는 다른 도구를 사용하여 다음 프로세스를 예약합니다.  
  
-   가장 오래된 행부터 시작하여 가장 최신 행까지 작은 청크로 여러 번 반복을 거쳐 모든 임시 테이블의 기록 데이터를 삭제하고, 위 그림에서와 같이 단일 트랜잭션의 모든 행을 삭제하지 마세요.  
  
-   모든 반복은 기록 테이블에서 일부 데이터를 제거하는 일반 저장 프로시저를 호출하여 구현합니다(이 프로시저에 대한 내용은 아래 코드 예제 참조).  
  
-   프로세스를 호출할 때마다 개별 임시 테이블에 대해 삭제해야 하는 행 수를 계산합니다. 행 수와 호출 수에 따라 모든 프로시저 호출에 대한 분할 지점을 동적으로 결정합니다.  
  
-   임시 테이블에 액세스하는 응용 프로그램에 미치는 영향을 줄이기 위해 단일 테이블에 대한 반복 간 지연 기간을 설정하도록 계획합니다.  
  
 단일 임시 테이블에 대한 데이터를 삭제하는 저장 프로시저는 다음 코드 조각과 유사하게 표현될 수 있습니다(환경에 적용하기 전에 이 코드를 주의 깊게 검토한 후 조정 필요).  
  
```  
DROP PROCEDURE IF EXISTS sp_CleanupHistoryData;  
GO  
  
CREATE PROCEDURE sp_CleanupHistoryData  
         @temporalTableSchema sysname  
       , @temporalTableName sysname  
       , @cleanupOlderThanDate datetime2  
AS  
    DECLARE @disableVersioningScript nvarchar(max) = '';  
    DECLARE @deleteHistoryDataScript nvarchar(max) = '';  
    DECLARE @enableVersioningScript nvarchar(max) = '';  
  
DECLARE @historyTableName sysname    
DECLARE @historyTableSchema sysname    
DECLARE @periodColumnName sysname    
  
/*Generate script to discover history table name and end of period column for given temporal table name*/  
EXECUTE sp_executesql   
    N'SELECT @hst_tbl_nm = t2.name, @hst_sch_nm = s.name, @period_col_nm = c.name  
        FROM sys.tables t1   
           JOIN sys.tables t2 on t1.history_table_id = t2.object_id  
        JOIN sys.schemas s on t2.schema_id = s.schema_id  
            JOIN sys.periods p on p.object_id = t1.object_id  
           JOIN sys.columns c on p.end_column_id = c.column_id and c.object_id = t1.object_id  
                  WHERE   
                 t1.name = @tblName and s.name = @schName'  
                , N'@tblName sysname  
                , @schName sysname  
                , @hst_tbl_nm sysname OUTPUT  
                , @hst_sch_nm sysname OUTPUT  
                , @period_col_nm sysname OUTPUT'  
                , @tblName = @temporalTableName  
                , @schName = @temporalTableSchema  
                , @hst_tbl_nm = @historyTableName OUTPUT  
                , @hst_sch_nm = @historyTableSchema OUTPUT  
                , @period_col_nm = @periodColumnName OUTPUT   
  
IF @historyTableName IS NULL OR @historyTableSchema IS NULL OR @periodColumnName IS NULL  
    THROW 50010, 'History table cannot be found. Either specified table is not system-versioned temporal or you have provided incorrect argument values.', 1  
  
/*Generate 3 statements that will run inside a transaction: SET SYSTEM_VERSIONING = OFF, DELETE FROM history_table, SET SYSTEM_VERSIONING = ON */  
SET @disableVersioningScript =  @disableVersioningScript + 'ALTER TABLE [' + @temporalTableSchema + '].[' + @temporalTableName + '] SET (SYSTEM_VERSIONING = OFF)'  
SET @deleteHistoryDataScript =  @deleteHistoryDataScript + ' DELETE FROM  [' + @historyTableSchema + '].[' + @historyTableName + ']   
     WHERE ['+ @periodColumnName + '] < ' + '''' + convert(varchar(128), @cleanupOlderThanDate, 126) +  ''''   
SET @enableVersioningScript =  @enableVersioningScript + ' ALTER TABLE [' + @temporalTableSchema + '].[' + @temporalTableName + ']   
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = [' + @historyTableSchema + '].[' + @historyTableName + '], DATA_CONSISTENCY_CHECK = OFF )); '   
  
BEGIN TRAN  
    EXEC (@disableVersioningScript);  
    EXEC (@deleteHistoryDataScript);  
    EXEC (@enableVersioningScript);  
COMMIT;  
```  

## <a name="using-temporal-history-retention-policy-approach"></a>임시 기록 보존 정책 접근 방식 사용
> **참고:** Temporal 기록 보존 정책 접근 방식 사용은 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 및 SQL Server 2017 CTP 1.3 이상에 적용됩니다.  

Temporal 기록 보존은 개별 테이블 수준에서 구성할 수 있으므로 사용자가 유연한 에이징 정책을 만들 수 있습니다. Temporal 보존 적용은 간단해서, 테이블을 만들거나 스키마를 변경할 때 매개 변수 하나만 설정하면 됩니다.

보존 정책을 정의한 후부터 Azure SQL Database는 자동 데이터 정리를 사용할 수 있는 기록 행이 있는지 정기적으로 확인합니다. 일치하는 행을 식별하고 기록 테이블에서 제거하는 작업은 시스템에서 예약하고 실행하는 백그라운드 태스크로 투명하게 수행됩니다. 기록 테이블 행의 기간 조건은 SYSTEM_TIME 기간의 종료를 나타내는 열을 기준으로 확인됩니다. 예를 들어 보존 기간이 6개월로 설정된 경우 정리할 수 있는 테이블 행은 다음 조건을 만족합니다.
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
앞의 예제에서는 ValidTo 열이 SYSTEM_TIME 기간의 종료에 해당한다고 가정했습니다.
### <a name="how-to-configure-retention-policy"></a>보존 정책을 구성하는 방법
Temporal 테이블의 보존 정책을 구성하려면 먼저 데이터베이스 수준에서 temporal 기록 보존이 사용하도록 설정되어 있는지 확인해야 합니다.
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
데이터베이스 플래그 **is_temporal_history_retention_enabled**는 기본적으로 ON으로 설정되어 있지만 사용자가 ALTER DATABASE 문을 사용하여 변경할 수 있습니다. 특정 시점 복원 작업 후에도 자동으로 OFF로 설정됩니다. 데이터베이스에 대한 temporal 기록 보존 정리를 사용하도록 설정하려면 다음 문을 실행합니다.
```
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
```
보존 정책은 테이블을 만들 때 HISTORY_RETENTION_PERIOD 매개 변수 값을 지정하여 구성합니다.
```
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
```
DAYS, WEEKS, MONTHS 및 YEARS와 같은 여러 시간 단위를 사용하여 보존 기간을 지정할 수 있습니다. HISTORY_RETENTION_PERIOD를 생략하면 INFINITE 보존으로 간주됩니다. INFINITE 키워드를 명시적으로 사용할 수도 있습니다.
일부 시나리오에서는 테이블을 만든 후 보존을 구성할 수도 있고 이전에 구성한 값을 변경할 수도 있습니다. 이런 경우에 ALTER TABLE 문을 사용합니다.
```
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
```
보존 정책의 현재 상태를 살펴보려면 데이터베이스 수준에서 temporal 보존 사용 플래그를 개별 테이블의 보존 기간과 조인하는 다음 쿼리를 사용합니다.
```
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
```
### <a name="how-sql-database-deletes-aged-rows"></a>SQL Database에서 오래된 행을 삭제하는 방법
정리 프로세스는 기록 테이블의 인덱스 레이아웃에 따라 달라집니다. *클러스터형 인덱스(B-트리 또는 columnstore)를 사용하는 기록 테이블에만 유한 보존 정책을 구성할 수 있다*는 점을 기억해야 합니다. 보존 기간이 한정된 모든 temporal 테이블에 대한 오래된 데이터 정리를 수행하는 백그라운드 태스크가 만들어집니다. rowstore(B-트리) 클러스터형 인덱스에 대한 정리 논리에서는 더 작은 청크(최대 10K)의 오래된 행을 삭제하여 데이터베이스 로그 및 I/O 하위 시스템에 주는 부담을 최소화합니다. 정리 논리에서 필요한 B-트리 인덱스를 활용하긴 하지만 보존 기간보다 오래된 행의 삭제 순서를 확실히 보장할 수는 없습니다. 따라서 *응용 프로그램의 정리 순서를 신뢰하지 마세요*.

클러스터형 columnstore에 대한 정리 태스크는 전체 행 그룹을 한 번에 제거하므로(일반적으로 각 그룹에 1백만 개 행 포함) 매우 효율적이며, 기록 데이터가 빠른 속도로 생성되는 경우 특히 효율적입니다.

![클러스터형 columnstore 보존](../../relational-databases/tables/media/cciretention.png "클러스터형 columnstore 보존")

클러스터형 columnstore 인덱스는 데이터 압축이 뛰어나고 보존 정리가 효율적이므로 작업에서 대량의 기록 데이터를 빠르게 생성하는 시나리오에 적합합니다. 이런 패턴은 변경 내용 추적 및 감사, 추세 분석 또는 IoT 데이터 수집에 temporal 테이블을 사용하는 집약적 트랜잭션 처리 작업에서 일반적으로 나타납니다.

자세한 내용은 [보존 정책을 사용하여 임시 테이블에서 기록 데이터 관리](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-temporal-tables-retention-policy)를 참조하세요.

## <a name="see-also"></a>관련 항목:  
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [임시 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [임시 테이블 고려 사항 및 제한 사항](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [임시 테이블 보안](../../relational-databases/tables/temporal-table-security.md)   
 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

