---
title: "데이터 대량 가져오기 중 ID 값 유지(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 09/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 2a20a9d0b7b8cc5aa32863bc687f7095ce33623a
ms.contentlocale: ko-kr
ms.lasthandoff: 10/13/2017

---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>데이터 대량 가져오기 중 ID 값 유지(SQL Server)
ID 값이 들어 있는 데이터 파일을 Microsoft SQL Server 인스턴스로 대량으로 가져올 수 있습니다.  기본적으로 가져온 데이터 파일의 ID 열 값은 무시되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 자동으로 고유 값을 할당합니다.  고유 값은 테이블 작성 중에 지정된 초기 및 증분 값을 기준으로 합니다.

데이터 파일에 테이블의 ID 열에 대한 값이 없으면 서식 파일을 사용하여 데이터를 가져올 때 테이블의 ID 열을 건너뛰어야 함을 지정할 수 있습니다.  자세한 내용은 [서식 파일을 사용하여 테이블 열 건너뛰기(SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md) 를 참조하세요.

|윤곽선|
|---|
|[ID 값 유지](#keep_identity)<br />[예제 테스트 조건](#etc)<br />&emsp;&#9679;&emsp;[샘플 테이블](#sample_table)<br />&emsp;&#9679;&emsp;[샘플 데이터 파일](#sample_data_file)<br />&emsp;&#9679;&emsp;[샘플 비 XML 서식 파일](#nonxml_format_file)<br />[예](#examples)<br />&emsp;&#9679;&emsp;[서식 파일 없이 bcp 사용 및 ID 값 유지](#bcp_identity)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 bcp 사용 및 ID 값 유지](#bcp_identity_fmt)<br />&emsp;&#9679;&emsp;[서식 파일 없이 bcp 및 생성된 ID 값 사용](#bcp_default)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 bcp 및 생성된 ID 값 사용](#bcp_default_fmt)<br />&emsp;&#9679;&emsp;[서식 파일 없이 BULK INSERT 사용 및 ID 값 유지](#bulk_identity)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 BULK INSERT 사용 및 ID 값 유지](#bulk_identity_fmt)<br />&emsp;&#9679;&emsp;[서식 파일 없이 BULK INSERT 및 생성된 ID 값 사용](#bulk_default)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 BULK INSERT 및 생성된 ID 값 사용](#bulk_default_fmt)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 OPENROWSET 사용 및 ID 값 유지](#openrowset_identity_fmt)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일과 함께 OPENROWSET 및 생성된 ID 값 사용](#openrowset_default_fmt)<br /><p>                                                                                                                                                                                                                  </p>|

## ID 값 유지 <a name="keep_identity"></a>  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 ID 값을 할당하지 않으면서 테이블에 데이터 행을 대량으로 가져오려면 적절한 ID 유지 명령 한정자를 사용합니다.  ID 유지 한정자를 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 데이터 파일의 ID 값을 사용합니다.  이러한 한정자는 다음과 같습니다.

|Command|ID 유지 한정자|한정자 유형|  
|-------------|------------------------------|--------------------|  
|bcp|-E|스위치|  
|BULK INSERT|KEEPIDENTITY|인수|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|KEEPIDENTITY|테이블 힌트|  
   
 자세한 내용은 [bcp 유틸리티](../../tools/bcp-utility.md), [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md), [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md), [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md) 및 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  

> [!NOTE]
>  여러 테이블에서 사용할 수 있거나 테이블을 참조하지 않고 응용 프로그램에서 호출할 수 있는 자동으로 증가하는 번호를 만들려면 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)를 참조하세요.
 
## 예제 테스트 조건<a name="etc"></a>  
이 항목의 예제는 아래에 정의된 테이블, 데이터 파일 및 서식 파일을 기반으로 합니다.

### **샘플 테이블**<a name="sample_table"></a>
아래 스크립트에서는 테스트 데이터베이스와 `myIdentity`라는 테이블을 만듭니다.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myIdentity ( 
   PersonID smallint IDENTITY(1,1) NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date
   );
```
 
### **샘플 데이터 파일**<a name="sample_data_file"></a>
메모장을 사용하여 빈 파일 `D:\BCP\myIdentity.bcp` 를 만들고 아래 데이터를 삽입합니다.  
```
3,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
1,Stella,Rosenhain,1992-03-02
4,Miller,Dylan,1954-01-05
```
  
또는 다음 PowerShell 스크립트를 실행하여 데이터 파일을 만들고 채울 수 있습니다.
```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = $dir + 'myIdentity.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '3,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '1,Stella,Rosenhain,1992-03-02';
Add-Content -Path $bcpFile -Value '4,Miller,Dylan,1954-01-05';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```

### **샘플 비 XML 서식 파일**<a name="nonxml_format_file"></a>
SQL Server는 두 유형의 서식 파일, 즉 비 XML 서식 파일과 XML 서식 파일을 지원합니다.  비 XML 서식 파일은 이전 버전의 SQL Server에서 원래 지원했던 서식 파일입니다.  자세한 내용은 [비 XML 서식 파일(SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 을 검토하세요.  다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myIdentity.fmt`의 스키마를 기반으로 비 xml 서식 파일 `myIdentity`를 생성합니다.  [bcp](../../tools/bcp-utility.md) 명령을 사용하여 서식 파일을 만들려면 데이터 파일 경로 대신 **format** 인수를 지정하고 **nul** 을 사용합니다.  format 옵션에는 **-f** 옵션도 필요합니다.  또한 이 예제에서 한정자 **c** 는 문자 데이터를 지정하는 데 사용되고, **t,** 는 쉼표를 [필드 종결자](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)로 지정하는 데 사용되며, **T** 는 통합된 보안을 사용하여 신뢰할 수 있는 연결을 지정하는 데 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.
  
```
bcp TestDatabase.dbo.myIdentity format nul -c -f D:\BCP\myIdentity.fmt -t, -T

REM Review file
Notepad D:\BCP\myIdentity.fmt
```
 
> [!IMPORTANT]
> 비 XML 서식 파일이 캐리지 리턴\줄 바꿈으로 끝나는지 확인하세요.  그러지 않으면 다음과 같은 오류 메시지가 표시될 수 있습니다.
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## 예<a name="examples"></a>
아래 예제에서는 위에서 만든 데이터베이스, 데이터 파일 및 서식 파일을 사용합니다.
  
### **서식 파일 없이 [bcp](../../tools/bcp-utility.md) 사용 및 ID 값 유지**<a name="bcp_identity"></a>
**-E** 스위치.  명령 프롬프트에서 다음 명령을 입력합니다.
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -T -c -t, -E

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```

### **[비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)과 함께 [bcp](../../tools/bcp-utility.md) 사용 및 ID 값 유지**<a name="bcp_identity_fmt"></a>
**-E** 및 **-f** 스위치.  명령 프롬프트에서 다음 명령을 입력합니다.
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -f D:\BCP\myIdentity.fmt -T -E

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
 
### **서식 파일 없이 [bcp](../../tools/bcp-utility.md) 및 생성된 ID 값 사용**<a name="bcp_default"></a>
기본값 사용.  명령 프롬프트에서 다음 명령을 입력합니다.
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -T -c -t,

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
  
### **Using [bcp](../../tools/bcp-utility.md) and Generated Identity Values with a [Non-XML Format File](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_default_fmt"></a>
기본값 및 **-f** 스위치 사용.  명령 프롬프트에서 다음 명령을 입력합니다.
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -f D:\BCP\myIdentity.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
  
### **서식 파일 없이 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 사용 및 ID 값 유지**<a name="bulk_identity"></a>
**KEEPIDENTITY** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity; -- for testing
BULK INSERT dbo.myIdentity
    FROM 'D:\BCP\myIdentity.bcp'
    WITH (
        DATAFILETYPE = 'char',  
        FIELDTERMINATOR = ',',  
        KEEPIDENTITY
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Using [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) and Keeping Identity Values with a [Non-XML Format File](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_identity_fmt"></a>
**KEEPIDENTITY** 및 **FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity; -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myIdentity.fmt',
        KEEPIDENTITY
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **서식 파일 없이 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 생성된 ID 값 사용**<a name="bulk_default"></a>
기본값 사용.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ','
      );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **[비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)과 함께 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 생성된 ID 값 사용**<a name="bulk_default_fmt"></a>
기본값 및 **FORMATFILE** 인수 사용.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myIdentity.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **[비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)과 함께 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 사용 및 ID 값 유지**<a name="openrowset_identity_fmt"></a>
**KEEPIDENTITY** 테이블 힌트 및 **FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
INSERT INTO dbo.myIdentity
WITH (KEEPIDENTITY) 
(PersonID, FirstName, LastName, BirthDate)
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myIdentity.bcp', 
        FORMATFILE = 'D:\BCP\myIdentity.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
 
### **Using [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) and Generated Identity Values with a [Non-XML Format File](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_default_fmt"></a>
기본값 및 **FORMATFILE** 인수 사용.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
INSERT INTO dbo.myIdentity
(FirstName, LastName, BirthDate)
    SELECT FirstName, LastName, BirthDate
    FROM OPENROWSET (
        BULK 'D:\BCP\myIdentity.bcp', 
        FORMATFILE = 'D:\BCP\myIdentity.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
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
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **bcp를 사용할 때 데이터 형식의 호환 가능성을 지정하려면**  
  
1.  [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
2.  [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [bcp를 사용하여 파일 저장 유형 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
[데이터를 가져오거나 내보내기 위한 서식 파일(SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  

