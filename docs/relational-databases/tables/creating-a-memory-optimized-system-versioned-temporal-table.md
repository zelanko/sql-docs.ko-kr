---
title: "메모리 액세스에 최적화된 시스템 버전 임시 테이블 만들기 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c1fc682-bf5b-4096-a0ff-3235d71c205a
caps.latest.revision: 14
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 14
---
# 메모리 액세스에 최적화된 시스템 버전 임시 테이블 만들기
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  디스크 기반 기록 테이블을 만들 때와 마찬가지로 다양한 방식으로 메모리 액세스에 최적화된 임시 테이블을 만들 수 있습니다.  
  
> [!NOTE]  
>  메모리 액세스에 최적화된 테이블을 만들려면 먼저 [메모리 액세스에 최적화된 파일 그룹](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)을 만들어야 합니다.  
  
 이름 지정은 제어하면서 시스템이 기본 구성을 사용하여 기록 테이블을 만들도록 하려는 경우 기본 기록 테이블이 포함된 임시 테이블을 만들면 편리합니다. 아래 예제에서는 새 시스템 버전 메모리 액세스에 최적화된 임시 테이블을 새 디스크 기반 기록 테이블에 연결합니다.  
  
```  
CREATE SCHEMA History  
GO  
CREATE TABLE dbo.Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH   
    (  
        MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,  
            SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )   
    );  
```  
  
 사용자 지정 임시 솔루션을 기본 제공 지원으로 마이그레이션하려는 경우와 같이 기존 테이블을 사용하여 시스템 버전 관리 기능을 추가하려는 경우 기존 기록 테이블에 연결된 임시 테이블을 만들면 유용합니다. 아래 예제에서는 기존 기록 테이블에 연결된 새 임시 테이블을 만듭니다.  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (  
        SYSTEM_VERSIONING = ON  
            (  
                HISTORY_TABLE = dbo.Department_History  
                , DATA_CONSISTENCY_CHECK = ON   
            )  
        , MEMORY_OPTIMIZED = ON  
        , DURABILITY = SCHEMA_AND_DATA  
    );  
```  
  
## 이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Creating%20a%20Memory-Optimized%20System-Versioned%20Temporal%20Table%20page)으로 보내 주세요.  
  
## 참고 항목  
 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [메모리 액세스에 최적화된 시스템 버전 임시 테이블로 작업](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [메모리 액세스에 최적화된 시스템 버전 임시 테이블 모니터링](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [메모리 액세스에 최적화된 시스템 버전 임시 테이블 관련 성능 고려 사항](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)   
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  