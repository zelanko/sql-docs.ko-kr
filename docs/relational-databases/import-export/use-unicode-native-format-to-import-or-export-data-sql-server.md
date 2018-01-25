---
title: "데이터를 가져오거나 내보내기 위해 유니코드 네이티브 형식 사용(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 09/30/2016
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
- Unicode [SQL Server], bulk importing and exporting
- data formats [SQL Server], Unicode native
ms.assetid: a6213308-f3d5-406e-9029-19d8bb3367f3
caps.latest.revision: "32"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7b3217ebde3a1d9b3424b2fcb9c53954504a853a
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="use-unicode-native-format-to-import-or-export-data-sql-server"></a>데이터를 가져오거나 내보내기 위해 유니코드 네이티브 형식 사용(SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 유니코드 네이티브 형식은 한 곳의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에서 다른 설치로 정보를 복사해야 하는 경우 유용합니다. 비문자 형식의 데이터에 네이티브 형식을 사용하면 문자 형식과 다른 데이터 형식 간의 불필요한 변환을 막고 시간을 절약할 수 있습니다. 모든 문자 형식의 데이터에 유니코드 문자 형식을 사용하면 다른 코드 페이지를 사용하는 서버 간에 데이터를 대량 로드할 때 확장 문자의 손실을 방지할 수 있습니다. 유니코드 네이티브 형식의 데이터 파일은 어떤 대량 가져오기 방법으로도 읽을 수 있습니다.  
  
 확장 또는 DBCS 문자를 포함하는 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 여러 인스턴트 사이에 대량의 데이터를 전송하는 경우 유니코드 네이티브 형식을 사용하는 것이 좋습니다. 비문자 데이터의 경우 유니코드 네이티브 형식은 네이티브(데이터베이스) 데이터 형식을 사용합니다. [char](../../t-sql/data-types/char-and-varchar-transact-sql.md), [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md), [nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md), [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)및 [ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)등의 문자 데이터의 경우 유니코드 네이티브 형식에서는 유니코드 문자 데이터 형식을 사용합니다.  
  
 유니코드 원시 형식의 데이터 파일에 SQLVARIANT로 저장된 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 데이터는 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 및 [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) 값이 [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) 및 [nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)로 변환되어 영향을 받은 열에 두 배의 저장 공간이 필요하다는 점을 제외하고 네이티브 형식의 데이터 파일과 같은 방법으로 작동합니다. 테이블 열로 대량 가져오기를 수행하면 원래의 메타데이터는 유지되고 값은 원래의 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 및 [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) 데이터 형식으로 다시 변환됩니다.  
 
 |항목 내용|
|---|
|[유니코드 네이티브 형식의 명령 옵션](#command_options)|
|[예제 테스트 조건](#etc)<br />&emsp;&#9679;&emsp;[샘플 테이블](#sample_table)<br />&emsp;&#9679;&emsp;[샘플 비 XML 서식 파일](#nonxml_format_file)|
|[예](#examples)<br />&emsp;&#9679;&emsp;[bcp 및 유니코드 원시 형식을 사용하여 데이터 내보내기](#bcp_widenative_export)<br />&emsp;&#9679;&emsp;[bcp 및 유니코드 원시 형식을 사용하여 서식 파일 없이 데이터 가져오기](#bcp_widenative_import)<br />&emsp;&#9679;&emsp;[bcp 및 유니코드 원시 형식을 사용하여 XML 이외의 서식 파일과 함께 데이터 가져오기](#bcp_widenative_import_fmt)<br />&emsp;&#9679;&emsp;[서식 파일 없이 BULK INSERT 및 유니코드 원시 형식 사용](#bulk_widenative)<br />&emsp;&#9679;&emsp;[XML 이외의 서식 파일과 함께 BULK INSERT 및 유니코드 원시 형식 사용하기](#bulk_widenative_fmt)<br />&emsp;&#9679;&emsp;[XML 이외의 서식 파일과 함께 OPENROWSET 및 유니코드 원시 형식 사용하기](#openrowset_widenative_fmt)|
|[관련 태스크](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|
  
## 유니코드 네이티브 형식의 명령 옵션<a name="command_options"></a>  
[bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 또는 [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)를 사용하여 테이블로 유니코드 문자 형식 데이터를 가져올 수 있습니다.  [bcp](../../tools/bcp-utility.md) 명령 또는 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 문의 경우 문에서 데이터 형식을 지정할 수 있습니다.  [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 문의 경우 서식 파일에서 데이터 형식을 지정해야 합니다.  
  
유니코드 원시 형식에 대해 지원되는 명령 옵션은 다음과 같습니다.  
  
|Command|옵션|Description|  
|-------------|------------|-----------------|  
|bcp|**-N**|**bcp** 유틸리티가 유니코드 원시 형식을 사용하게 합니다. 즉, 모든 비문자 데이터에 네이티브(데이터베이스) 데이터 형식을 사용하고 모든 문자(**char**, **nchar**, **varchar**, **nvarchar**, **text**, 및 **ntext**) 데이터에 유니코드 문자 데이터 형식을 사용합니다.|  
|BULK INSERT|DATAFILETYPE **='widenative'**|데이터를 대량으로 가져올 때 유니코드 원시 형식을 사용합니다.|  
|OPENROWSET|해당 사항 없음|서식 파일을 사용해야 합니다.|
    
> [!NOTE]
>  서식 파일에서 필드 단위로 서식을 지정할 수도 있습니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)를 참조하세요.
  
## 예제 테스트 조건<a name="etc"></a>  
이 항목의 예제는 아래에 정의된 테이블 및 서식 파일을 기반으로 합니다.

### **샘플 테이블**<a name="sample_table"></a>
아래 스크립트는 테스트 데이터베이스인 `myWidenative` 라는 테이블을 만들고 테이블을 몇 가지 초기 값으로 채웁니다.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myWidenative ( 
    PersonID smallint NOT NULL,
    FirstName nvarchar(25) NOT NULL,
    LastName nvarchar(30) NOT NULL,
    BirthDate date,
    AnnualSalary money
);

-- Populate table
INSERT TestDatabase.dbo.myWidenative
VALUES 
(1, N'ϴAnthony', N'Grosse', '02-23-1980', 65000.00),
(2, N'❤Alica', N'Fatnowna', '11-14-1963', 45000.00),
(3, N'☎Stella', N'Rossenhain', '03-02-1992', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myWidenative;
```

### **샘플 비 XML 서식 파일**<a name="nonxml_format_file"></a>
SQL Server는 두 유형의 서식 파일, 즉 비 XML 서식 파일과 XML 서식 파일을 지원합니다.  비 XML 서식 파일은 이전 버전의 SQL Server에서 원래 지원했던 서식 파일입니다.  자세한 내용은 [비 XML 서식 파일(SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 을 검토하세요.  다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myWidenative.fmt`의 스키마를 기반으로 비 xml 서식 파일 `myWidenative`를 생성합니다.  [bcp](../../tools/bcp-utility.md) 명령을 사용하여 서식 파일을 만들려면 데이터 파일 경로 대신 **format** 인수를 지정하고 **nul** 을 사용합니다.  format 옵션에는 **-f** 옵션도 필요합니다.  또한 이 예제에서 한정자 **c** 는 문자 데이터를 지정하는 데 사용되고 **T** 는 통합된 보안을 사용하여 신뢰할 수 있는 연결을 지정하는 데 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.

```
bcp TestDatabase.dbo.myWidenative format nul -f D:\BCP\myWidenative.fmt -T -N

REM Review file
Notepad D:\BCP\myWidenative.fmt
```

> [!IMPORTANT]
> 비 XML 서식 파일이 캐리지 리턴\줄 바꿈으로 끝나는지 확인하세요.  그러지 않으면 다음과 같은 오류 메시지가 표시될 수 있습니다.
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## 예<a name="examples"></a>
아래 예제에서는 위에서 만든 데이터베이스와 서식 파일을 사용합니다.

### **bcp 및 유니코드 원시 형식을 사용하여 데이터 내보내기**<a name="bcp_widenative_export"></a>
**-N** 스위치 및 **OUT** 명령.  참고: 이 예제에서 만든 데이터 파일은 이후 나오는 모든 예제에서 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.
```
bcp TestDatabase.dbo.myWidenative OUT D:\BCP\myWidenative.bcp -T -N

REM Review results
NOTEPAD D:\BCP\myWidenative.bcp
```

### **bcp 및 유니코드 원시 형식을 사용하여 서식 파일 없이 데이터 가져오기**<a name="bcp_widenative_import"></a>
**-N** 스위치 및 **IN** 명령.  명령 프롬프트에서 다음 명령을 입력합니다.
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidenative;"

REM Import data
bcp TestDatabase.dbo.myWidenative IN D:\BCP\myWidenative.bcp -T -N

REM Review results is SSMS
```

### **bcp 및 유니코드 원시 형식을 사용하여 XML 이외의 서식 파일과 함께 데이터 가져오기**<a name="bcp_widenative_import_fmt"></a>
**-N** 및 **-f** 스위치와 **IN** 명령.  명령 프롬프트에서 다음 명령을 입력합니다.
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidenative;"

REM Import data
bcp TestDatabase.dbo.myWidenative IN D:\BCP\myWidenative.bcp -f D:\BCP\myWidenative.fmt -T

REM Review results is SSMS
```

### **서식 파일 없이 BULK INSERT 및 유니코드 원시 형식 사용**<a name="bulk_widenative"></a>
**DATAFILETYPE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidenative; -- for testing
BULK INSERT TestDatabase.dbo.myWidenative
    FROM 'D:\BCP\myWidenative.bcp'
    WITH (
        DATAFILETYPE = 'widenative'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidenative;
```

### **XML 이외의 서식 파일과 함께 BULK INSERT 및 유니코드 원시 형식 사용하기**<a name="bulk_widenative_fmt"></a>
**FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidenative; -- for testing
BULK INSERT TestDatabase.dbo.myWidenative
   FROM 'D:\BCP\myWidenative.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myWidenative.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidenative;
```

### **XML 이외의 서식 파일과 함께 OPENROWSET 및 유니코드 원시 형식 사용하기**<a name="openrowset_widenative_fmt"></a>
**FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidenative;  -- for testing
INSERT INTO TestDatabase.dbo.myWidenative
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myWidenative.bcp', 
        FORMATFILE = 'D:\BCP\myWidenative.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myWidenative;
```

## 관련 작업<a name="RelatedTasks"></a>
대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
