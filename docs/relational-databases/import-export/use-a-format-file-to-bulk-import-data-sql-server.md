---
title: "서식 파일을 사용하여 데이터 대량 가져오기(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 09/20/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
caps.latest.revision: "45"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 71a54504c92921cc16abfa1342a5c3452ebadda8
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>서식 파일을 사용하여 데이터 대량 가져오기(SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

이 항목에서는 대량 가져오기 작업에서 서식 파일을 사용하는 방법에 대해 설명합니다.  서식 파일은 데이터 파일의 필드를 테이블의 열에 매핑합니다.  추가 정보는 [서식 파일 만들기(SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) 를 검토하세요.

|윤곽선|
|---|
|[시작하기 전에](#begin)<br />[예제 테스트 조건](#etc)<br />&emsp;&#9679;&emsp;[샘플 테이블](#sample_table)<br />&emsp;&#9679;&emsp;[샘플 데이터 파일](#sample_data_file)<br />[서식 파일 만들기](#create_format_file)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일 만들기](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[XML 서식 파일 만들기](#xml_format_file)<br />[서식 파일을 사용하여 데이터를 대량으로 가져오기](#import_data)<br />&emsp;&#9679;&emsp;[bcp 및 비 XML 서식 파일 사용](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[bcp 및 비 XML 서식 파일 사용](#bcp_xml)<br />&emsp;&#9679;&emsp;[BULK INSERT 및 비 XML 서식 파일 사용](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[BULK INSERT 및 XML 서식 파일 사용](#bulk_xml)<br />&emsp;&#9679;&emsp;[OPENROWSET(BULK...) 및 비 XML 서식 파일 사용](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[OPENROWSET(BULK...) 및 XML 서식 파일 사용](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
## 시작하기 전에<a name="begin"></a>
* 유니코드 문자 데이터 파일에 서식 파일을 사용하려면 모든 입력 필드가 유니코드 텍스트 문자열(즉, 고정 크기 또는 문자 종료 유니코드 문자열)이어야 합니다.
* [SQLXML](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md) 데이터를 대량으로 내보내거나 가져오려면 서식 파일에서 다음 데이터 형식 중 하나를 사용합니다.
  * SQLCHAR 또는 SQLVARYCHAR(데이터를 클라이언트 코드 페이지나 데이터 정렬에 포함된 코드 페이지로 보냅니다.)
  * SQLNCHAR 또는 SQLNVARCHAR(데이터를 유니코드로 보냅니다.)
  * SQLBINARY 또는 SQLVARYBIN(데이터를 변환하지 않고 보냅니다.)
* Azure SQL Database 및 Azure SQL Data Warehouse는 [bcp](../../tools/bcp-utility.md)만 지원합니다.  자세한 내용은 다음을 참조하세요.
  * [Azure SQL Data Warehouse에 데이터 로드](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-load/)
  * [SQL Server에서 Azure SQL Data Warehouse로 데이터 로드(플랫 파일)](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-from-sql-server-with-bcp/)
  * [데이터 마이그레이션](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-migrate-data/)

## 예제 테스트 조건<a name="etc"></a>  
이 항목의 서식 파일 예제는 아래 정의된 테이블 및 데이터 파일을 기반으로 합니다.

### **샘플 테이블**<a name="sample_table"></a>
아래 스크립트에서는 테스트 데이터베이스와 `myFirstImport`라는 테이블을 만듭니다.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.MyFirstImport (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   BirthDate Date
   );
```

### **샘플 데이터 파일**<a name="sample_data_file"></a>
메모장을 사용하여 빈 파일 `D:\BCP\myFirstImport.bcp` 을 만들고 다음 데이터를 삽입합니다.
```
1,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
3,Stella,Rosenhain,1992-03-02
```

또는 다음 PowerShell 스크립트를 실행하여 데이터 파일을 만들고 채울 수 있습니다.
```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = Join-Path -Path $dir -ChildPath 'MyFirstImport.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```

## 서식 파일 만들기<a name="create_format_file"></a>
SQL Server는 두 유형의 서식 파일, 즉 비 XML 서식 파일과 XML 서식 파일을 지원합니다.  비 XML 서식 파일은 이전 버전의 SQL Server에서 원래 지원했던 서식 파일입니다.

### **비 XML 서식 파일 만들기**<a name="nonxml_format_file"></a>
자세한 내용은 [비 XML 서식 파일(SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 을 검토하세요.  다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myFirstImport.fmt`의 스키마를 기반으로 비 xml 서식 파일 `myFirstImport`를 생성합니다.  bcp 명령을 사용하여 서식 파일을 만들려면 데이터 파일 경로 대신 **format** 인수를 지정하고 **nul** 을 사용합니다.  format 옵션에는 **-f** 옵션도 필요합니다.  또한 이 예제에서 한정자 **c** 는 문자 데이터를 지정하는 데 사용되고, **t,** 는 쉼표를 [필드 종결자](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)로 지정하는 데 사용되며, **T** 는 통합된 보안을 사용하여 신뢰할 수 있는 연결을 지정하는 데 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -f D:\BCP\myFirstImport.fmt -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.fmt
```

비 XML 서식 파일 `D:\BCP\myFirstImport.fmt` 는 다음과 같이 표시됩니다.
```
13.0
4
1       SQLCHAR             0       7       ","      1     PersonID               ""
2       SQLCHAR             0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR             0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR             0       11      "\r\n"   4     BirthDate              ""
```

> [!IMPORTANT]
> 비 XML 서식 파일이 캐리지 리턴\줄 바꿈으로 끝나는지 확인하세요.  그러지 않으면 다음과 같은 오류 메시지가 표시될 수 있습니다.
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

### **XML 서식 파일 만들기**<a name="xml_format_file"></a>  
자세한 내용은 [XML 서식 파일(SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) 을 검토하세요.  다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myFirstImport.xml`의 스키마를 기반으로 XML 서식 파일 `myFirstImport`을 생성합니다. bcp 명령을 사용하여 서식 파일을 만들려면 데이터 파일 경로 대신 **format** 인수를 지정하고 **nul** 을 사용합니다.  서식 옵션에는 항상 **-f** 옵션이 필요하며 XML 서식 파일을 만들려면 **-x** 옵션도 지정해야 합니다.  또한 이 예제에서 한정자 **c** 는 문자 데이터를 지정하는 데 사용되고, **t,** 는 쉼표를 [필드 종결자](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)로 지정하는 데 사용되며, **T** 는 통합된 보안을 사용하여 신뢰할 수 있는 연결을 지정하는 데 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.
```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -x -f D:\BCP\myFirstImport.xml -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.xml
```

XML 서식 파일 `D:\BCP\myFirstImport.xml` 은 다음과 같이 표시됩니다.
```xml
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="11"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="BirthDate" xsi:type="SQLDATE"/>
 </ROW>
</BCPFORMAT>
```

## 서식 파일을 사용하여 데이터를 대량으로 가져오기<a name="import_data"></a>
아래 예제에서는 위에서 만든 데이터베이스, 데이터 파일 및 서식 파일을 사용합니다.

### **[bcp](../../tools/bcp-utility.md) 및 [비 XML 서식 파일 사용](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_nonxml"></a>
명령 프롬프트에서 다음 명령을 입력합니다.
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport"
```


### **[bcp](../../tools/bcp-utility.md) 및 [XML 서식 파일 사용](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="bcp_xml"></a>
명령 프롬프트에서 다음 명령을 입력합니다.
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.xml -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport;"
```


### **[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_nonxml"> 사용</a>
Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [XML 서식 파일](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="bulk_xml"> 사용</a>
Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **[OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 및 [비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_nonxml"> 사용</a>    
Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **[OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 및 [XML 서식 파일](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="openrowset_xml"> 사용</a>
Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```
  
## <a name="more-examples"></a>추가 예제  
 [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
 [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
 [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
 [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>관련 항목:  
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)  
  [데이터를 가져오거나 내보내기 위한 서식 파일(SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)
  
