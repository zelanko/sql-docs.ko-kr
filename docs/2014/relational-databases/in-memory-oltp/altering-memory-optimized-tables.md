---
title: 메모리 액세스에 최적화된 테이블 변경 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d1ae35d9dae03292edf31cd2b06acf97dc0db0c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783237"
---
# <a name="altering-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블 변경
  메모리 최적화 테이블에 대한 ALTER 작업 수행은 지원되지 않습니다. 여기에는 bucket_count 변경, 인덱스 추가 또는 제거, 열 추가 또는 제거 등의 작업이 포함됩니다. 이 항목에서는 메모리 최적화 테이블을 업데이트하는 방법에 대한 지침을 제공합니다.  
  
## <a name="updating-the-definition-of-a-memory-optimized-table"></a>메모리 액세스에 최적화된 테이블의 정의 업데이트  
 메모리 최적화 테이블의 정의를 업데이트하려면 업데이트된 테이블 정의를 사용하여 새 테이블을 만들고 데이터를 새 테이블에 복사한 다음 새 테이블 사용을 시작해야 합니다. 테이블이 읽기 전용이 아닌 경우 이렇게 하려면 데이터 복사가 수행되는 동안 테이블이 변경되지 않도록 테이블에 대한 작업을 중지해야 합니다.  
  
 다음 절차에서는 테이블을 업데이트하는 데 필요한 단계를 대략적으로 설명합니다. 이 예제에서는 업데이트를 통해 인덱스를 추가합니다. 이 프로시저는 테이블의 이름을 유지 하며 두 개의 데이터 복사 작업 (임시 테이블에 한 번, 새 테이블에 한 번)을 요구 합니다. 인덱스의 bucket_count를 변경하거나 열을 추가 또는 제거하는 작업은 같은 방식으로 수행됩니다.  
  
1.  테이블에 대한 작업을 중지합니다.  
  
2.  테이블에 대한 스크립트를 생성하고 새 인덱스를 스크립트에 추가합니다.  
  
3.  T와 해당 사용 권한을 참조하는 스키마 바운드 개체(주로 고유하게 컴파일된 저장 프로시저)에 대한 스크립트를 생성합니다.  
  
     다음 쿼리를 사용하여 테이블을 참조하는 스키마 바운드 개체를 찾을 수 있습니다.  
  
    ```sql  
    declare @t nvarchar(255) = N'<table name>'  
  
    select r.referencing_schema_name, r.referencing_entity_name  
    from sys.dm_sql_referencing_entities (@t, 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
    where r.is_caller_dependent = 0 and m.is_schema_bound=1;  
    ```  
  
     다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 저장 프로시저의 사용 권한을 스크립팅할 수 있습니다.  
  
    ```sql  
    declare @sp nvarchar(255) = N'<procedure name>'  
    declare @permissions nvarchar(max) = N''  
  
    select @permissions += dp.state_desc + N' ' + dp.permission_name + N' ON ' +   
       quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) + N' TO ' +  
       quotename(u.name) + N'; ' + char(13)  
    from sys.database_permissions as dp  
  
    join sys.database_principals as u  
       on u.principal_id = dp.grantee_principal_id  
  
    join sys.objects as o  
       on o.object_id = dp.major_id  
    where dp.class = 1 /* object */  
       and dp.minor_id = 0 and o.object_id=object_id(@sp);  
  
    select @permissions  
    ```  
  
4.  테이블의 복사본을 생성하고 원래 테이블에서 테이블의 복사본으로 데이터를 복사합니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] <sup>1</sup>을 사용 하 여 복사본을 만들 수 있습니다.  
  
    ```sql  
    select * into dbo.T_copy from dbo.T  
    ```  
  
     사용 가능한 메모리가 충분 한 경우 메모리 `T_copy` 최적화 테이블을 사용 하 여 데이터 복사를 더 빠르게 수행할 수 있습니다. <sup>2</sup>  
  
5.  원래 테이블을 참조하는 스키마 바운드 개체를 삭제합니다.  
  
6.  원래 테이블을 삭제합니다.  
  
7.  새 인덱스가 포함된 스크립트를 사용하여 새 테이블(`T`)을 만듭니다.  
  
8.  `T_copy`에서 `T`로 데이터를 복사합니다.  
  
9. 스키마 바운드 개체 참조를 다시 만들고 사용 권한을 적용합니다.  
  
10. `T`에 대한 작업을 시작합니다.  
  
 <sup>1</sup> `T_copy` 은이 예제에서 디스크에 유지 됩니다. `T`의 백업을 사용할 수 있는 경우 `T_copy`는 임시 또는 비 영속성 테이블일 수 있습니다.  
  
 <sup>2</sup> 에는 충분 한 `T_copy`메모리가 있어야 합니다. 메모리는 `DROP TABLE`에서 즉시 비워지지 않습니다. `T_copy`가 메모리 액세스에 최적화된 경우 `T`의 추가 복사본 두 개에 대한 충분한 메모리가 있어야 합니다. `T_copy`가 디스크 기반 테이블인 경우 기존 버전의 `T`를 삭제한 후 따라 잡아야 하는 가비지 수집기로 인해 `T`의 추가 복사본 하나에 대해 충분한 메모리만 있으면 됩니다.  
  
## <a name="changing-schema-powershell"></a>스키마 변경(PowerShell)  
 다음 PowerShell 스크립트는 테이블 및 연결된 사용 권한을 스크립팅하여 스키마 변경을 준비하고 생성합니다.  
  
```powershell
prepare_schema_change.ps1 <serverName> <databaseName> <schemaName> <tableName>
```
  
 이 스크립트는 테이블을 인수로 사용하고, 현재 폴더에서 개체 및 해당 사용 권한과 참조 스키마 바운드 개체 및 해당 사용 권한을 스크립팅합니다. 입력 테이블의 스키마를 업데이트하기 위해 총 7개의 스크립트가 생성됩니다.  
  
-   데이터를 임시 테이블(힙)에 복사합니다.  
  
-   테이블을 참조하는 스키마 바운드 개체를 삭제합니다.  
  
-   테이블을 삭제합니다.  
  
-   새 스키마를 사용하여 테이블을 다시 만들고 사용 권한을 다시 적용합니다.  
  
-   임시 테이블에서 새로 만든 테이블로 데이터를 복사합니다.  
  
-   테이블을 참조하는 스키마 바운드 개체와 해당 사용 권한을 다시 만듭니다.  
  
-   임시 테이블을 삭제합니다.  
  
 원하는 스키마 변경을 반영하도록 4단계에 대한 스크립트를 업데이트해야 합니다. 테이블 열을 변경한 경우 필요에 따라 5단계(임시 테이블에서 데이터 복사)와 6단계(저장 프로시저 다시 만들기)에 대한 스크립트를 업데이트해야 합니다.  
  
```powershell
# Prepare for schema changes by scripting out the table, as well as associated permissions
# Usage: prepare_schema_change.ps1 server_name db_name schema_name table_name  
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage prepare_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
$object_heap = "$object$(Get-Random)"  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | Out-Null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$scripter = New-Object ("Microsoft.SqlServer.Management.SMO.Scripter") ($server)  
  
## initialize table variable  
$tableUrn = $server.Databases[$database].Tables[$object, $schema]  
if($tableUrn.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
## initialize scripting object  
$scriptingOptions = New-Object ("Microsoft.SqlServer.Management.SMO.ScriptingOptions")
$scriptingOptions.Permissions = $True  
$scriptingOptions.ScriptDrops = $True  
  
$scripter.Options = $scriptingOptions;  
  
Write-Host "(1) Scripting SELECT INTO $object_heap for table [$object] to 1_copy_to_heap_for_$schema`_$object.sql"  
Echo "SELECT * INTO $schema.$object_heap FROM $schema.$object WITH (SNAPSHOT)" | Out-File "1_copy_to_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(2) Scripting DROP for procs schema-bound to [$object] 2_drop_procs_$schema`_$object.sql"  
## query referencing schema-bound objects  
$dt = $server.Databases[$database].ExecuteWithResults("select r.referencing_schema_name, r.referencing_entity_name  
from sys.dm_sql_referencing_entities ('$schema.$object', 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
where r.is_caller_dependent = 0 and m.is_schema_bound=1;")  
  
## initialize out file  
Echo "" | Out-File "2_drop_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
ForEach ($t In $dt.Tables)  
{    
   ForEach ($r In $t.Rows)  
   {    
      ## script object   
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      $scripter.Script($so) | Out-File -Append "2_drop_procs_$schema`_$object.sql"  
   }  
}  
Write-Host "--done--"  
Write-Host ""  
Write-Host "(3) Scripting DROP table for [$object] to 3_drop_table_$schema`_$object.sql"
$scripter.Script($tableUrn) | Out-File "3_drop_table_$schema`_$object.sql";
Write-Host "--done--"  
Write-Host ""  
  
## now script creates  
$scriptingOptions.ScriptDrops = $False  
  
Write-Host "(4) Scripting CREATE table and permissions for [$object] to !please_edit_4_create_table_$schema`_$object.sql"  
Write-Host "***** rename this script to 4_create_table.sql after completing the updates to the schema"
$scripter.Script($tableUrn) | Out-File "!please_edit_4_create_table_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(5) Scripting INSERT INTO table from heap and UPDATE STATISTICS for [$object] to 5_copy_from_heap_$schema`_$object.sql"  
Write-Host "[update this script if columns are added to or removed from the table]"  
Echo "INSERT INTO [$schema].[$object] SELECT * FROM [$schema].[$object_heap]; UPDATE STATISTICS [$schema].[$object] WITH FULLSCAN, NORECOMPUTE" | Out-File "5_copy_from_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(6) Scripting CREATE PROC and permissions for procedures schema-bound to [$object] to 6_create_procs_$schema`_$object.sql"  
Write-Host "[update the procedure definitions if columns are renamed or removed]"  
## initialize out file  
Echo "" | Out-File "6_create_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
ForEach ($t In $dt.Tables)  
{    
   ForEach ($r In $t.Rows)  
   {    
      ## script the schema-bound object  
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      ForEach($s In $scripter.Script($so))  
        {  
            Echo $s | Out-File -Append "6_create_procs_$schema`_$object.sql"  
            Echo "GO" | Out-File -Append "6_create_procs_$schema`_$object.sql"  
        }  
   }  
}  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(7) Scripting DROP $object_heap to 7_drop_heap_$schema`_$object.sql"  
Echo "DROP TABLE $schema.$object_heap" | Out-File "7_drop_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
```  
  
 다음 PowerShell 스크립트는 이전 예제에서 스크립팅된 스키마 변경 내용을 실행합니다. 이 스크립트는 테이블을 인수로 사용하고, 해당 테이블 및 연결된 저장 프로시저에 대해 생성된 스키마 변경 스크립트를 실행합니다.  
  
 사용법: execute_schema_change. ps1 *server_name * * db_name`schema_name`table_name*  
  
```powershell
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage execute_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | Out-Null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$database = $server.Databases[$database]  
$table = $database.Tables[$object, $schema]  
if($table.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
$1 = Get-Item "1_copy_to_heap_$schema`_$object.sql"  
$2 = Get-Item "2_drop_procs_$schema`_$object.sql"  
$3 = Get-Item "3_drop_table_$schema`_$object.sql"  
$4 = Get-Item "4_create_table_$schema`_$object.sql"  
$5 = Get-Item "5_copy_from_heap_$schema`_$object.sql"  
$6 = Get-Item "6_create_procs_$schema`_$object.sql"  
$7 = Get-Item "7_drop_heap_$schema`_$object.sql"  
  
Write-Host "(1) Running SELECT INTO heap for table [$object] from 1_copy_to_heap_for_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $1.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(2) Running DROP for procs schema-bound from [$object] 2_drop_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $2.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(3) Running DROP table for [$object] to 4_drop_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $3.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(4) Running CREATE table and permissions for [$object] from 4_create_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $4.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(5) Running INSERT INTO table from heap for [$object] and UPDATE STATISTICS from 5_copy_from_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $5.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(6) Running CREATE PROC and permissions for procedures schema-bound to [$object] from 6_create_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $6.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(7) Running DROP heap from 7_drop_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $7.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화 된 테이블](memory-optimized-tables.md)  
