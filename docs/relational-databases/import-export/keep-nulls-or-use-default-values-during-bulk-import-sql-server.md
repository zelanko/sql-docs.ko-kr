---
title: 대량 가져오기 수행 중 Null 유지 또는 기본값 사용(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 09/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 567817abd46fa23ba304bc3cd2cdbb0b5a0e20fc
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39552763"
---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>대량 가져오기 수행 중 Null 유지 또는 기본값 사용(SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

기본적으로 데이터를 테이블로 가져올 때 [bcp](../../tools/bcp-utility.md) 명령 및 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 문은 해당 테이블의 열에 대해 정의된 기본값을 유지합니다.  예를 들어 데이터 파일에 null 필드가 있으면 열의 기본값이 대신 로드됩니다.  [bcp](../../tools/bcp-utility.md) 명령 및 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 문을 사용하면 Null 값을 유지하도록 지정할 수 있습니다.

반대로 일반 INSERT 문은 기본값을 삽입하는 대신 Null 값을 유지합니다. INSERT ... SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 문은 일반 INSERT와 같은 기본 동작을 제공하지만 기본값 삽입에 대한 [테이블 힌트](../../t-sql/queries/hints-transact-sql-table.md)를 추가로 지원합니다.

|윤곽선|
|---|
|[Null 값 유지](#keep_nulls)<br />[INSERT ... SELECT * FROM OPENROWSET(BULK...)에서 기본값 사용](#keep_default)<br />[예제 테스트 조건](#etc)<br />&emsp;&#9679;&emsp;[샘플 테이블](#sample_table)<br />&emsp;&#9679;&emsp;[샘플 데이터 파일](#sample_data_file)<br />&emsp;&#9679;&emsp;[샘플 비 XML 서식 파일](#nonxml_format_file)<br />[대량 가져오기 수행 중 Null 유지 또는 기본값 사용](#import_data)<br />&emsp;&#9679;&emsp;[서식 파일 없이 bcp 사용 및 Null 값 유지](#bcp_null)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 bcp 사용 및 Null 값 유지](#bcp_null_fmt)<br />&emsp;&#9679;&emsp;[서식 파일 없이 bcp 사용 및 기본값 사용](#bcp_default)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 bcp 사용 및 기본값 사용](#bcp_default_fmt)<br />&emsp;&#9679;&emsp;[서식 파일 없이 BULK INSERT 사용 및 Null 값 유지](#bulk_null)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 BULK INSERT 사용 및 Null 값 유지](#bulk_null_fmt)<br />&emsp;&#9679;&emsp;[서식 파일 없이 BULK INSERT 사용 및 기본값 사용](#bulk_default)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 BULK INSERT 사용 및 기본값 사용](#bulk_default_fmt)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 OPENROWSET(BULK...) 사용 및 Null 값 유지](#openrowset__null_fmt)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 OPENROWSET(BULK...) 사용 및 기본값 사용](#openrowset__default_fmt)

## Null 값 유지<a name="keep_nulls"></a>  
다음 한정자는 대량 가져오기 작업 중 테이블 열에 대한 기본값(있는 경우)을 상속하기보다는 데이터 파일의 빈 필드에 Null 값을 유지하도록 지정합니다.  [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)의 경우 기본적으로 대량 로드 작업에 지정되지 않은 열은 NULL로 설정됩니다.
  
|Command|한정자|한정자 유형|  
|-------------|---------------|--------------------|  
|bcp|-k|스위치|  
|BULK INSERT|KEEPNULLS**\***|인수|  
|INSERT ... 로 기본 값 사용|해당 사항 없음|해당 사항 없음|  
  
**\*** [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)의 경우 기본값을 사용할 수 없으면 null 값을 허용하도록 테이블 열을 정의해야 합니다. 
  
> [!NOTE]
> 이러한 한정자는 대량 가져오기 명령을 통해 테이블에서 DEFAULT 정의 확인을 비활성화합니다.  그러나 동시 INSERT 문의 경우 DEFAULT 정의가 있어야 합니다.
 
## INSERT ... SELECT * FROM OPENROWSET(BULK...) SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)<a name="keep_default"></a>  
데이터 파일의 빈 필드의 경우 해당 테이블 열에서 기본값(있는 경우)을 사용하도록 지정할 수 있습니다.  기본값을 사용하려면 테이블 힌트 [KEEPDEFAULTS](../../t-sql/queries/hints-transact-sql-table.md)를 사용하세요.
 
> [!NOTE]
>  자세한 내용은 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md), [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md) 및 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.

## 예제 테스트 조건<a name="etc"></a>  
이 항목의 예제는 아래에 정의된 테이블, 데이터 파일 및 서식 파일을 기반으로 합니다.

### **샘플 테이블**<a name="sample_table"></a>
아래 스크립트에서는 테스트 데이터베이스와 `myNulls`라는 테이블을 만듭니다.  네 번째 테이블 열 `Kids`는 기본값을 갖습니다.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myNulls ( 
   PersonID smallint not null,
   FirstName varchar(25),
   LastName varchar(30),
   Kids varchar(13) DEFAULT 'Default Value',
   BirthDate date
   );
```

### **샘플 데이터 파일**<a name="sample_data_file"></a>
메모장을 사용하여 빈 파일 `D:\BCP\myNulls.bcp` 를 만들고 아래 데이터를 삽입합니다.  세 번째 레코드, 네 번째 열에는 값이 없습니다.

```
1,Anthony,Grosse,Yes,1980-02-23
2,Alica,Fatnowna,No,1963-11-14
3,Stella,Rosenhain,,1992-03-02
```

또는 다음 PowerShell 스크립트를 실행하여 데이터 파일을 만들고 채울 수 있습니다.

```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = $dir + 'MyNulls.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,Yes,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,No,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```
  
### **샘플 비 XML 서식 파일**<a name="nonxml_format_file"></a>
SQL Server는 두 유형의 서식 파일, 즉 비 XML 서식 파일과 XML 서식 파일을 지원합니다.  비 XML 서식 파일은 이전 버전의 SQL Server에서 원래 지원했던 서식 파일입니다.  자세한 내용은 [비 XML 서식 파일(SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 을 검토하세요.  다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myNulls.fmt`의 스키마를 기반으로 비 xml 서식 파일 `myNulls`를 생성합니다.  [bcp](../../tools/bcp-utility.md) 명령을 사용하여 서식 파일을 만들려면 데이터 파일 경로 대신 **format** 인수를 지정하고 **nul** 을 사용합니다.  format 옵션에는 **-f** 옵션도 필요합니다.  또한 이 예제에서 한정자 **c** 는 문자 데이터를 지정하는 데 사용되고, **t,** 는 쉼표를 [필드 종결자](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)로 지정하는 데 사용되며, **T** 는 통합된 보안을 사용하여 신뢰할 수 있는 연결을 지정하는 데 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
bcp TestDatabase.dbo.myNulls format nul -c -f D:\BCP\myNulls.fmt -t, -T

REM Review file
Notepad D:\BCP\myNulls.fmt
```

> [!IMPORTANT]
> 비 XML 서식 파일이 캐리지 리턴\줄 바꿈으로 끝나는지 확인하세요.  그러지 않으면 다음과 같은 오류 메시지가 표시될 수 있습니다.
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

 서식 파일을 만드는 방법은 [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)를 사용하세요.  
  
## 대량 가져오기 수행 중 Null 유지 또는 기본값 사용<a name="import_data"></a>
아래 예제에서는 위에서 만든 데이터베이스, 데이터 파일 및 서식 파일을 사용합니다.

### **서식 파일 없이 [bcp](../../tools/bcp-utility.md) 사용 및 Null 값 유지**<a name="bcp_null"></a>

**-k** 스위치.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -c -t, -T -k

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```
  
### **서식 파일 없이 [bcp](../../tools/bcp-utility.md) 함께 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_null_fmt"></a>
**-k** 및 **-f** 스위치. 명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -f D:\BCP\myNulls.fmt -T -k

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```

### **서식 파일 없이 [bcp](../../tools/bcp-utility.md) 사용 및 기본값 사용**<a name="bcp_default"></a>
명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -c -t, -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```
  
### **서식 파일 없이 [bcp](../../tools/bcp-utility.md) 과 함께 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_default_fmt"></a>
**-f** 스위치.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -f D:\BCP\myNulls.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```

### **서식 파일 없이 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 사용 및 Null 값 유지**<a name="bulk_null"></a>
**KEEPNULLS** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
USE TestDatabase;
GO
TRUNCATE TABLE dbo.myNulls; -- for testing
BULK INSERT dbo.myNulls
    FROM 'D:\BCP\myNulls.bcp'
    WITH (
        DATAFILETYPE = 'char',  
        FIELDTERMINATOR = ',',  
        KEEPNULLS
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **서식 파일 없이 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 함께 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_null_fmt"></a>
**KEEPNULLS** 및 **FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls; -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNulls.fmt',
        KEEPNULLS
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **서식 파일 없이 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 사용 및 기본값 사용**<a name="bulk_default"></a>
Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ','
      );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **서식 파일 없이 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 과 함께 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_default_fmt"></a>
**FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNulls.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **서식 파일 없이 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 함께 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset__null_fmt"></a>
**FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
INSERT INTO dbo.myNulls
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNulls.bcp', 
        FORMATFILE = 'D:\BCP\myNulls.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **서식 파일 없이 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 과 함께 [bcp](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset__default_fmt"></a>
**KEEPDEFAULTS** 테이블 힌트 및 **FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
INSERT INTO dbo.myNulls
WITH (KEEPDEFAULTS) 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNulls.bcp', 
        FORMATFILE = 'D:\BCP\myNulls.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [대량 내보내기 또는 가져오기를 위한 데이터 준비&#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **서식 파일을 사용하려면**  
  
-   [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면**  
  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **bcp를 사용할 때 데이터 형식의 호환 가능성을 지정하려면**  
  
-   [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [bcp를 사용하여 파일 저장 유형 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
