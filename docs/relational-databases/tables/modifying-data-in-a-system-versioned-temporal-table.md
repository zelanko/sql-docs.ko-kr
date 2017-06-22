---
title: "시스템 버전 임시 테이블의 데이터 수정 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5f398470-c531-47b5-84d5-7c67c27df6e5
caps.latest.revision: 8
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b3f59affdbe29e3dddf777b22322a5503e69caa1
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="modifying-data-in-a-system-versioned-temporal-table"></a>시스템 버전 임시 테이블의 데이터 수정
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  시스템 버전 임시 테이블의 데이터는 일반 DML 문을 사용하여 수정됩니다. 여기서 한가지 중요한 차이점은 기간 열 데이터를 직접 수정할 수 없다는 것입니다. 데이터가 업데이트되면 버전이 부여되며, 업데이트된 각 행의 이전 버전은 기록 테이블에 삽입됩니다. 데이터가 삭제되는 경우, 논리적으로 삭제되고 행이 현재 테이블에서 기록 테이블로 이동합니다. 영구적으로 삭제되지 않습니다.  
  
## <a name="inserting-data"></a>데이터 삽입  
 새 데이터를 삽입하면, **HIDDEN** 이(가) 아니면 **PERIOD**열을 설명해야 합니다. 시스템 버전 임시 테이블로 파티션 전환을 사용할 수도 있습니다.  
  
### <a name="insert-new-data-with-visible-period-columns"></a>표시되는 기간 열을 사용하여 새 데이터 삽입  
 다음과 같이 표시되는 **PERIOD** 열이 있으면 새 **PERIOD** 열을 설명하기 위해 **INSERT** 문을 구성할 수 있습니다.  
  
-   **INSERT** 문에 열 목록을 지정하면, 이 열에 대한 값이 시스템에서 자동으로 생성되기 때문에 **PERIOD** 열을 생략할 수 있습니다.  
  
    ```  
    --Insert with column list and without period columns   
    INSERT INTO [dbo].[Department] ([DeptID] ,[DeptName] ,[ManagerID] ,[ParentDeptID])   
    VALUES(10, 'Marketing', 101, 1);  
  
    ```  
  
-   **INSERT** 문의 열 목록에 **PERIOD** 열을 지정하면 해당 값으로 **DEFAULT** 을 지정해야 합니다.  
  
    ```  
    INSERT INTO [dbo].[Department] ([DeptID] ,[DeptName] ,[ManagerID] ,[ParentDeptID], SysStartTime, SysEndTime)   
    VALUES(11, 'Sales', 101, 1, default, default);  
  
    ```  
  
-   **INSERT** 문에 열 목록을 지정하지 않으면 **DEFAULT** 또는 **PERIOD** 열을 지정합니다.  
  
    ```  
    --Insert without  column list and DEFAULT values for period columns   
    INSERT INTO [dbo].[Department]    
    VALUES(12, 'Production', 101, 1, default, default);  
  
    ```  
  
### <a name="insert-data-into-a-table-with-hidden-period-columns"></a>HIDDEN 기간 열로 테이블에 데이터 삽입  
 **PERIOD** 열이 HIDDEN으로 지정되면 열 목록을 지정하지 않고 INSERT를 사용하는 경우에, 표시되는 열의 값만 지정하면 됩니다. **INSERT** 문에 새로운 **PERIOD** 열을 설명할 필요가 없습니다. 이러한 동작은 버전 관리를 활용하는 테이블에서 시스템 버전 관리를 활성화하는 경우 레거시 응용 프로그램이 계속 작동하도록 보장합니다.  
  
```  
CREATE TABLE [dbo].[CompanyLocation]  
(   
     [LocID] [int] IDENTITY(1,1) NOT NULL PRIMARY KEY  
   , [LocName] [varchar](50) NOT NULL  
   , [City] [varchar](50) NOT NULL  
   , [SysStartTime] [datetime2](0) GENERATED ALWAYS AS ROW START HIDDEN NOT NULL   
   , [SysEndTime] [datetime2](0) GENERATED ALWAYS AS ROW END HIDDEN NOT NULL   
PERIOD FOR SYSTEM_TIME ([SysStartTime], [SysEndTime])   
)    
WITH ( SYSTEM_VERSIONING = ON );   
GO   
INSERT INTO [dbo].[CompanyLocation]   
VALUES  ('Headquarters', 'New York');  
  
```  
  
### <a name="inserting-data-using-partition-switch"></a>PARTITION SWITCH를 사용하여 데이터 삽입  
 현재 테이블이 분할되어 있다면 빈 파티션으로 데이터를 로드하거나 여러 파티션에 병렬로 로드하는 효율적인 메커니즘으로 PARTITION SWITCH를 사용할 수 있습니다.   
시스템 버전 임시 테이블과 함께 **PARTITION SWITCH IN** 문에 사용되는 준비 테이블에는 **SYSTEM_TIME PERIOD** 정의가 필요하지만 시스템 버전 임시 테이블일 필요는 없습니다.    
이렇게 하면 준비 테이블로 데이터를 삽입하거나 미리 채워진 준비 테이블에 SYSTEM_TIME 기간이 추가되는 동안 임시 일관성 검사가 수행되도록 합니다.  
  
```  
/*Create staging table with period definition for SWITCH IN temporal table*/   
CREATE TABLE [dbo].[Staging_Department_Partition2]  
(   
     [DeptID] [int] NOT NULL  
   , [DeptName] [varchar](50)  NOT NULL  
   , [ManagerID] [int] NULL  
   , [ParentDeptID] [int] NULL  
   , [SysStartTime] [datetime2](7) GENERATED ALWAYS AS ROW START NOT NULL  
   , [SysEndTime] [datetime2](7) GENERATED ALWAYS AS ROW END NOT NULL  
   , PERIOD FOR SYSTEM_TIME ( [SysStartTime], [SysEndTime] )   
) ON [PRIMARY]   
  
/*Create aligned primary key*/   
ALTER TABLE [dbo].[Staging_Department_Partition2]    
ADD CONSTRAINT [Staging_Department_Partition2_PK]  
   PRIMARY KEY CLUSTERED  
   (  [DeptID] ASC )     
   ON [PRIMARY]   
  
/*   
Create and enforce constraints for partition boundaries.   
Partition 2 contains rows with DeptID > 100 and DeptID <=200   
*/   
ALTER TABLE [dbo].[Staging_Department_Partition2]      
   WITH CHECK ADD  CONSTRAINT [chk_staging_Department_partition_2]     
   CHECK  ([DeptID]>N'100' AND [DeptID]<=N'200')   
ALTER TABLE [dbo].[Staging_Department_Partition2]    
   CHECK CONSTRAINT [chk_staging_Department_partition_2]   
  
/*Load data into staging table*/   
INSERT INTO [dbo].[staging_Department] ([DeptID],[DeptName],[ManagerID],[ParentDeptID])   
VALUES (101,'D101',1,NULL)  
  
/*Use PARTITION SWITCH IN to efficiently add data to current table */    
ALTER TABLE [Staging_Department]    
SWITCH TO [dbo].[Department] PARTITION 2;  
  
```  
  
 기간을 정의하지 않고 테이블에서 PARTITION SWITCH를 수행하려고 하면 오류 메시지가 표시됩니다. `Msg 13577, Level 16, State 1, Line 25    ALTER TABLE SWITCH statement failed on table 'MyDB.dbo.Staging_Department_2015_09_26' because target table has SYSTEM_TIME PERIOD while source table does not have it.`  
  
## <a name="updating-data"></a>데이터 업데이트  
 일반 **UPDATE** 문으로 현재 테이블의 데이터를 업데이트합니다. 기록 테이블의 현재 테이블 데이터를 "oops" 시나리오용으로 업데이트할 수 있습니다. 하지만 **PERIOD** 열을 업데이트할 수 없으며 **SYSTEM_VERSIONING = ON**상태에서 기록 테이블의 데이터를 직접 업데이트할 수 없습니다.   
**SYSTEM_VERSIONING = OFF** 를 설정하고 현재 및 기록 테이블의 행을 업데이트합니다. 다만 시스템에 변경 기록이 보존되지 않는다는 것에 유의합니다.  
  
### <a name="updating-the-current-table"></a>현재 테이블 업데이트  
 이 예제에서는 DeptID = 10인 행에 대해 ManagerID 열이 업데이트됩니다. **PERIOD** 은 어떤 방식으로든 참조되지 않습니다.  
  
```  
UPDATE [dbo].[Department] SET [ManagerID] = 501 WHERE [DeptID] = 10  
```  
  
 하지만 **PERIOD** 열을 업데이트할 수 없으며 기록 테이블을 업데이트할 수 없습니다.  이 예제에서는 **PERIOD** 열을 업데이트하려는 시도로 인해 오류가 발생합니다.  
  
```  
UPDATE [dbo].[Department]    
SET SysStartTime = '2015-09-23 23:48:31.2990175'    
WHERE DeptID = 10 ;  
  
Msg 13537, Level 16, State 1, Line 3   
Cannot update GENERATED ALWAYS columns in table 'TmpDev.dbo.Department'.  
  
```  
  
### <a name="updating-the-current-table-from-the-history-table"></a>기록 테이블에서 현재 테이블 업데이트  
 현재 테이블에 **UPDATE** 를 사용하여 실제 행 상태를 과거 특정 지점의 유효한 상태로 되돌릴 수 있습니다(“마지막으로 알려진 행 버전”으로 되돌리기). 다음 예제에서는 기록 테이블의 값으로, DeptID = 10인 2015-04-25으로 되돌리는 것을 보여줍니다.  
  
```  
UPDATE Department   
SET DeptName = History.DeptName   
FROM Department    
FOR SYSTEM_TIME AS OF '2015-04-25' AS History   
WHERE History.DeptID  = 10   
AND Department.DeptID = 10 ;  
  
```  
  
## <a name="deleting-data"></a>데이터 삭제  
 일반 **DELETE** 문으로 현재 테이블의 데이터를 삭제합니다. 삭제된 행의 종료 기간 열은 기본 트랜잭션의 시작 시간으로 채워집니다.   
**SYSTEM_VERSIONING = ON**상태이면 기록 테이블에서 행을 직접 삭제할 수 없습니다.   
**SYSTEM_VERSIONING = OFF** 를 설정하고 현재 및 기록 테이블의 행을 삭제합니다. 다만 시스템에 변경 기록이 보존되지 않는다는 것에 유의합니다.   
현재 테이블 및**SWITCH PARTITION OUT**, **TRUNCATE** , **SWITCH PARTITION OUT** 은 **SYSTEM_VERSIONING = ON**상태에서는 지원되지 않습니다.  
  
## <a name="using-merge-to-modify-data-in-temporal-table"></a>MERGE를 사용하여 임시 테이블의 데이터 수정  
 **MERGE** 연산은 **PERIOD** 열에 대한 **INSERT** 및 **UPDATE** 문의 제한 사항과 같은 제한 사항으로 지원됩니다.  
  
```  
CREATE TABLE DepartmentStaging (DeptId INT, DeptName varchar(50));   
GO   
INSERT INTO DepartmentStaging VALUES (1, 'Company Management');   
INSERT INTO DepartmentStaging VALUES (10, 'Science & Research');   
INSERT INTO DepartmentStaging VALUES (15, 'Process Management');   
  
MERGE dbo.Department AS target   
USING (SELECT DeptId, DeptName FROM DepartmentStaging) AS source (DeptId, DeptName)   
ON (target.DeptId = source.DeptId)   
WHEN MATCHED THEN    
    UPDATE   
   SET DeptName = source.DeptName   
WHEN NOT MATCHED THEN   
   INSERT (DeptName)   
   VALUES (source.DeptName);  
  
```  
  
## <a name="did-this-article-help-you-were-listening"></a>이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Modifying%20Data%20in%20a%20System-Versioned%20Temporal%20Table%20page)  
  
## <a name="see-also"></a>참고 항목  
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [시스템 버전 임시 테이블 만들기](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [시스템 버전 임시 테이블의 데이터 쿼리](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [시스템 버전 임시 테이블의 스키마 변경](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [시스템 버전 임시 테이블에서 시스템 버전 관리 중지](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  

