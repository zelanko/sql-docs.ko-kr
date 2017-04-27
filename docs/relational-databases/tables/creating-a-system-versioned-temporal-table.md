---
title: "시스템 버전 임시 테이블 만들기 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21e6d74f-711f-40e6-a8b7-85f832c5d4b3
caps.latest.revision: 20
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a75bde97eddb1b99546ec4d5ff0dbb33340e19e4
ms.lasthandoff: 04/11/2017

---
# <a name="creating-a-system-versioned-temporal-table"></a>시스템 버전 임시 테이블 만들기
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  기록 테이블을 지정하는 방법과 관련해서 시스템 버전 임시 테이블을 만드는 다음 세 가지 방법이 있습니다.  
  
-   익명 기록 테이블이 포함된 임시 테이블: 현재 테이블의 스키마를 지정하고 시스템이 자동 생성된 이름으로 해당 기록 테이블을 만들도록 합니다.  
  
-   기본 기록 테이블이 포함된 임시 테이블: 기록 테이블 스키마 이름 및 테이블 이름을 지정하고 시스템이 해당 스키마에 기록 테이블을 만들도록 합니다.  
  
-   미리 만든 사용자 정의 기록 테이블이 포함된 임시 테이블: 요구에 가장 알맞은 기록 테이블을 만든 다음 임시 테이블을 만드는 동안 해당 테이블을 참조합니다.  
  
## <a name="creating-a-temporal-table-with-an-anonymous-history-table"></a>익명 기록 테이블이 포함된 임시 테이블 만들기  
 "익명" 기록 테이블이 포함된 임시 테이블 만들기는 특히 프로토타입 및 시험 환경에서 빠른 개체 만들기에 편리한 옵션입니다. 또한 **SYSTEM_VERSIONING** 절에 매개 변수가 필요하지 않으므로 임시 테이블을 만드는 가장 간단한 방법이기도 합니다. 아래 예제에서는 기록 테이블의 이름을 정의하지 않고 시스템 버전 관리를 사용하도록 설정한 상태에서 새 테이블을 만듭니다.  
  
```  
CREATE TABLE Department   
(    
     DeptID int NOT NULL PRIMARY KEY CLUSTERED  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 GENERATED ALWAYS AS ROW START NOT NULL  
   , SysEndTime datetime2 GENERATED ALWAYS AS ROW END NOT NULL  
   , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)    
WITH (SYSTEM_VERSIONING = ON)   
;  
```  
  
### <a name="important-remarks"></a>중요한 주의 사항  
  
-   시스템 버전 임시 테이블에는 기본 키가 정의되어 있어야 하며 **PERIOD FOR SYSTEM_TIME** 로 선언된 datetime2 열 두 개를 사용하여 정확히 한 개의 **PERIOD FOR SYSTEM_TIME**을 정의해야 합니다.  
  
-   **PERIOD** 열은 null 허용 여부를 지정하지 않은 경우에도 언제나 null을 허용하지 않는다고 가정합니다. **PERIOD** 열을 명시적으로 null 허용으로 정의한 경우 **CREATE TABLE** 문이 실패합니다.  
  
-   기록 테이블은 언제나 열 수, 열 이름, 순서 및 데이터 형식에서 현재 또는 임시 테이블과 스키마를 맞춰야 합니다.  
  
-   익명 기록 테이블은 자동으로 현재 또는 임시 테이블과 같은 스키마에 생성됩니다.  
  
-   익명 기록 테이블 이름의 형식은 *MSSQL_TemporalHistoryFor_<current_temporal_table_object_id>_[suffix]*입니다. 접미사는 선택 사항이며 테이블 이름의 첫 번째 부분이 고유하지 않은 경우에만 추가됩니다.  
  
-   기록 테이블은 rowstore 테이블로 생성됩니다. 페이지 압축은 가능하면 적용되며, 그렇지 않으면 기록 테이블을 압축하지 않습니다. 예를 들어 스파스 열과 같은 일부 테이블 구성은 압축을 허용하지 않습니다.  
  
-   기본 클러스터형 인덱스는 형식 *IX_<history_table_name>*의 자동 생성된 이름을 가진 기록 테이블에 대해 생성됩니다. 클러스터형 인덱스는 **PERIOD** 열(시작, 종료)을 포함합니다.  
  
-   현재 테이블을 메모리 액세스에 최적화된 테이블로 만들려면 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)을 참조하세요.  
  
## <a name="creating-a-temporal-table-with-a-default-history-table"></a>기본 기록 테이블이 포함된 임시 테이블 만들기  
 이름 지정은 제어하면서 시스템이 기본 구성을 사용하여 기록 테이블을 만들도록 하려는 경우 기본 기록 테이블이 포함된 임시 테이블을 만들면 편리합니다. 아래 예제에서는 기록 테이블의 이름을 명시적으로 정의하고 시스템 버전 관리를 사용하도록 설정한 상태에서 새 테이블을 만듭니다.  
  
```  
CREATE TABLE Department   
(    
     DeptID int NOT NULL PRIMARY KEY CLUSTERED  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 GENERATED ALWAYS AS ROW START NOT NULL  
   , SysEndTime datetime2 GENERATED ALWAYS AS ROW END NOT NULL  
   , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)     
)   
WITH    
   (   
      SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory)   
   )   
;  
```  
  
### <a name="important-remarks"></a>중요한 주의 사항  
 기록 테이블은 명명된 기록 테이블에 명시적으로 적용되는 다음 규칙을 사용하여 "익명" 기록 테이블 만들기에 적용되는 것과 같은 규칙을 사용하여 생성됩니다.  
  
-   스키마 이름은 **HISTORY_TABLE** 매개 변수에 필수입니다.  
  
-   지정된 스키마가 없는 경우 **CREATE TABLE** 문이 실패합니다.  
  
-   **HISTORY_TABLE** 매개 변수에 의해 지정한 테이블이 이미 있는 경우 [스키마 일관성 및 임시 데이터 일관성](http://msdn.microsoft.com/library/dn935015.aspx)측면에서 새로 생성된 임시 표에 대해 유효성이 검사됩니다. 잘못된 기록 테이블을 지정하면 **CREATE TABLE** 문이 실패합니다.  
  
## <a name="creating-a-temporal-table-with-a-user-defined-history-table"></a>사용자 정의 기록 테이블이 포함된 임시 테이블 만들기  
 사용자 정의 기록 테이블이 포함된 임시 테이블 만들기는 특정 저장소 옵션 및 추가 인덱스를 가진 기록 테이블을 지정하려는 경우에 편리한 옵션입니다. 아래 예제에서는 생성될 임시 테이블과 정렬된 스키마를 가진 사용자 정의 기록 테이블을 만듭니다. 이 사용자 정의 기록 테이블에 대해 포인트 조회를 위해 클러스터형 columnstore 인덱스 및 추가 비클러스터형 rowstore(Btree) 인덱스를 만듭니다. 이 사용자 정의 기록 테이블이 생성된 후 사용자 정의 기록 테이블을 기본 기록 테이블로 지정하는 시스템 버전 임시 테이블이 생성됩니다.  
  
```  
CREATE TABLE DepartmentHistory   
(    
     DeptID int NOT NULL  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 NOT NULL  
   , SysEndTime datetime2 NOT NULL   
);   
GO   
CREATE CLUSTERED COLUMNSTORE INDEX IX_DepartmentHistory   
   ON DepartmentHistory;   
CREATE NONCLUSTERED INDEX IX_DepartmentHistory_ID_PERIOD_COLUMNS   
   ON DepartmentHistory (SysEndTime, SysStartTime, DeptID);   
GO   
CREATE TABLE Department   
(    
    DeptID int NOT NULL PRIMARY KEY CLUSTERED  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 GENERATED ALWAYS AS ROW START NOT NULL  
   , SysEndTime datetime2 GENERATED ALWAYS AS ROW END NOT NULL     
   , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)      
)    
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory))   
;  
```  
  
### <a name="important-remarks"></a>중요한 주의 사항  
  
-   집계 또는 창 작업 기능을 채택하는 기록 데이터에 대해 분석 쿼리를 실행할 계획인 경우 기본 인덱스로 클러스터형 columnstore 만들기는 압축 및 쿼리 성능에 권장되는 옵션입니다.  
  
-   기본 사용 사례가 데이터 감사(즉, 현재 테이블에서 단일 행에 대한 기록 변경 내용 검색)인 경우 클러스터형 인덱스를 가진 rowstore 기록 테이블을 만드는 것이 좋습니다.  
  
-   기록 테이블은 기본 키, 외래 키, 고유 인덱스, 테이블 제약 조건 또는 트리거를 가질 수 없습니다. 또한 변경 데이터 캡처, 변경 내용 추적, 트랜잭션 또는 병합 복제에 대해 구성할 수 없습니다.  
  
## <a name="alter-non-temporal-table-to-be-system-versioned-temporal-table"></a>비임시 테이블을 시스템 버전 임시 테이블로 변경  
 사용자 지정 임시 솔루션을 기본 제공 지원으로 마이그레이션하려는 경우처럼 기존 테이블을 사용하여 시스템 버전 관리를 사용하도록 설정해야 하는 경우입니다.   
예를 들어 트리거를 사용하여 버전 관리를 구현하는 테이블 집합이 있을 수 있습니다. 임시 시스템 버전 관리 사용은 덜 복잡하며 다음과 같은 추가 이점을 제공합니다.  
  
-   변경할 수 없는 기록  
  
-   시간 여행 쿼리를 위한 새로운 구문  
  
-   DML 성능 향상  
  
-   유지 관리 비용 최소화  
  
 기존 테이블을 변환하는 경우 새 열을 처리하도록 설계되지 않은 기존 응용 프로그램에 대한 영향을 피하기 위해 **HIDDEN** 절을 사용하여 새 **PERIOD** 열을 숨기는 것을 고려하세요.  
  
### <a name="adding-versioning-to-non-temporal-tables"></a>비임시 테이블에 버전 관리 추가  
 데이터를 포함하는 비임시 테이블에 대해 변경 내용 추적을 시작하려면 **PERIOD** 정의를 추가하고 선택적으로 SQL Server가 만드는 빈 기록 테이블에 대한 이름을 입력해야 합니다.  
  
```  
CREATE SCHEMA History;   
GO   
ALTER TABLE InsurancePolicy   
   ADD   
      SysStartTime datetime2(0) GENERATED ALWAYS AS ROW START HIDDEN    
           CONSTRAINT DF_SysStart DEFAULT SYSUTCDATETIME()  
      , SysEndTime datetime2(0) GENERATED ALWAYS AS ROW END HIDDEN    
           CONSTRAINT DF_SysEnd DEFAULT CONVERT(datetime2 (0), '9999-12-31 23:59:59'),   
      PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);   
GO   
ALTER TABLE InsurancePolicy   
   SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.InsurancePolicy))   
;  
```  
  
#### <a name="important-remarks"></a>중요한 주의 사항  
  
-   SQL Server Enterprise Edition 이외의 모든 버전에서 데이터가 포함된 기존 테이블에 기본값을 가진 null이 허용되지 않는 열을 추가하는 경우 데이터 작업(메타데이터 작업)의 크기에 주의해야 합니다. SQL Server Standard Edition에서 데이터가 포함된 큰 기존 기록 테이블의 경우 null이 아닌 열을 추가하면 작업 비용이 많이 들 수 있습니다.  
  
-   기간 시작 및 기간 종료 열에 대한 제약 조건을 신중하게 선택해야 합니다.  
  
    -   시작 열에 대한 기본값은 기존 행이 유효하다고 생각하는 시점을 지정합니다. 미래의 datetime 포인트로 지정할 수 없습니다.  
  
    -   종료 시간은 지정된 datetime2 정밀도에 대한 최대값으로 지정해야 함  
  
-   기간을 추가하면 기간 열에 대한 기본값이 유효한지 확인하기 위해 현재 테이블에 대해 데이터 일관성 검사를 수행합니다.  
  
-   **SYSTEM_VERSIONING**을 사용하도록 설정할 때 기존 기록 테이블을 지정하는 경우 현재 테이블과 기록 테이블 둘 다에 대해 데이터 일관성 검사가 수행됩니다. **DATA_CONISTENCY_CHECK = OFF** 를 추가 매개 변수로 지정하는 경우 이 과정을 건너뛸 수 있습니다.  
  
### <a name="migrate-existing-tables-to-built-in-support"></a>기본 제공 지원으로 기존 테이블 마이그레이션  
 이 예제에서는 기본 제공 임시 지원에 대한 트리거를 기반으로 기존 솔루션을 마이그레이션하는 방법을 보여 줍니다. 이 예제에서는 현재 사용자 지정 솔루션이 두 개의 분리된 사용자 테이블(**ProjectTaskCurrent** 및 **ProjectTaskHistory**)에서 현재 및 기록 데이터를 분할한다고 가정합니다. 기존 솔루션이 단일 테이블을 사용하여 실제 및 기록 행을 저장하는 경우 이 예제와 같은 마이그레이션 단계 전에 데이터를 두 테이블로 분할해야 합니다.  
  
```  
/*Drop trigger on future temporal table*/   
DROP TRIGGER ProjectCurrent_OnUpdateDelete;   
/*Make sure that future period columns are non-nullable*/   
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidFrom] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidTo] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidFrom] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidTo] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskCurrent   
   ADD PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])   
ALTER TABLE ProjectTaskCurrent   
   SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON))   
;  
```  
  
#### <a name="important-remarks"></a>중요한 주의 사항  
  
-   **PERIOD** 정의에 기존 열을 참조하면 암시적으로 해당 열에 대해 generated_always_type을 **AS_ROW_START** 및 **AS_ROW_END** 로 변경합니다.  
  
-   **PERIOD** 를 추가하면 기간 열에 대한 기존 값이 유효한지 확인하기 위해 현재 테이블에 대해 데이터 일관성 검사를 수행합니다.  
  
-   기존 데이터에 대해 임시 일관성 검사를 적용하기 위해 **DATA_CONSISTENCY_CHECK = ON** 을 사용하여 **SYSTEM_VERSIONING** 을 설정하는 것이 좋습니다.  
  
## <a name="did-this-article-help-you-were-listening"></a>이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Creating%20a%20System-Versioned%20Temporal%20Table%20page)  
  
## <a name="see-also"></a>참고 항목  
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [시스템 버전 임시 테이블의 데이터 수정](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [시스템 버전 임시 테이블의 데이터 쿼리](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [시스템 버전 임시 테이블의 스키마 변경](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [시스템 버전 임시 테이블에서 시스템 버전 관리 중지](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  

