---
title: "유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 09/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: b38f5585ffa79fbfa5ba702d4fdc8acee9924c7c
ms.contentlocale: ko-kr
ms.lasthandoff: 10/13/2017

---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server)
확장/DBCS 문자를 포함하는 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 여러 인스턴스 간에 대량 데이터 전송을 수행하는 경우에는 유니코드 문자 형식을 사용하는 것이 좋습니다. 유니코드 문자 데이터 형식을 사용하면 작업을 수행 중인 클라이언트에서 사용되는 코드 페이지와 다른 코드 페이지를 사용하여 서버에서 데이터를 내보낼 수 있습니다. 이런 경우 유니코드 문자 형식을 사용하면 다음과 같은 이점이 있습니다.  
  
* 원본 및 대상 데이터가 유니코드 데이터 형식이면 유니코드 문자 형식을 사용하여 모든 문자 데이터를 보존할 수 있습니다.  
  
* 원본 및 대상 데이터가 유니코드 데이터 형식이 아니면 유니코드 문자 형식을 사용하여 원본 데이터에 있지만 대상에서 표현할 수 없는 확장 문자의 손실을 최소화할 수 있습니다.

|항목 내용|
|---|
|[유니코드 문자 형식 사용 시 고려 사항](#considerations)|
|[유니코드 문자 형식, bcp 및 서식 파일 사용 시 특별 고려 사항](#special_considerations)|
|[유니코드 문자 형식의 명령 옵션](#command_options)|
|[예제 테스트 조건](#etc)<br />&emsp;&#9679;&emsp;[샘플 테이블](#sample_table)<br />&emsp;&#9679;&emsp;[샘플 비 XML 서식 파일](#nonxml_format_file)|
|[예](#examples)<br />&emsp;&#9679;&emsp;[bcp 및 유니코드 문자 형식을 사용하여 데이터 내보내기](#bcp_widechar_export)<br />&emsp;&#9679;&emsp;[bcp 및 유니코드 문자 형식을 사용하여 서식 파일 없이 데이터 가져오기](#bcp_widechar_import)<br />&emsp;&#9679;&emsp;[bcp 및 유니코드 문자 형식을 사용하여 XML 이외의 서식 파일과 함께 데이터 가져오기](#bcp_widechar_import_fmt)<br />&emsp;&#9679;&emsp;[서식 파일 없이 BULK INSERT 및 유니코드 문자 형식 사용](#bulk_widechar)<br />&emsp;&#9679;&emsp;[XML 이외의 서식 파일과 함께 BULK INSERT 및 유니코드 문자 형식 사용하기](#bulk_widechar_fmt)<br />&emsp;&#9679;&emsp;[XML 이외의 서식 파일과 함께 OPENROWSET 및 유니코드 문자 형식 사용하기](#openrowset_widechar_fmt)|
|[관련 태스크](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|
 
## 유니코드 문자 형식 사용 시 고려 사항<a name="considerations"></a>
유니코드 문자 형식을 사용할 때 다음 사항을 고려하세요.  

* 기본적으로 [bcp 유틸리티](../../tools/bcp-utility.md)는 탭 문자로 문자 데이터 필드를 구분하며 줄 바꿈 문자로 레코드를 종료합니다.  다른 종결자를 지정하는 방법에 대한 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.

* 유니코드 문자 형식 데이터 파일에 저장되어 있는 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 데이터는 데이터가 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 데이터 대신 [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)로 저장된다는 것을 제외하면 문자 형식 데이터 파일과 같은 방식으로 작동합니다. 문자 형식에 대한 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하십시오.  

## 유니코드 문자 형식, bcp 및 서식 파일 사용 시 특별 고려 사항<a name="special_considerations"></a>
유니코드 문자 형식 데이터 파일은 유니코드 파일의 규칙을 따릅니다.  파일의 처음 두 바이트는 16진수 0xFFFE입니다.  이 두 바이트는 바이트 순서 표시(BOM)로서 제공되며 높은 순서 바이트가 파일의 처음에 저장될지 마지막에 저장될지를 지정합니다.  [bcp 유틸리티](../../tools/bcp-utility.md) 에서 BOM을 잘못 해석하여 가져오기 프로세스의 일부가 실패하고 다음과 유사한 오류 메시지가 표시될 수 있습니다.
```
Starting copy...
SQLState = 22005, NativeError = 0
Error = [Microsoft][ODBC Driver 13 for SQL Server]Invalid character value for cast specification
```

다음과 같은 경우 BOM이 잘못 해석될 수 있습니다.
* [bcp 유틸리티](../../tools/bcp-utility.md) 가 사용되고 **-w** 스위치를 사용하여 유니코드 문자를 나타내는 경우

* 서식 파일을 사용하는 경우

* 데이터 파일의 첫 번째 필드가 문자가 아닌 경우

해당하는 *특정* 상황에 다음 해결 방법을 사용할 수 있는지 고려하세요.
* 서식 파일을 사용하지 마세요.  이 해결 방법의 예제가 아래에 제공됩니다. [bcp 및 유니코드 문자 형식을 사용하여 서식 파일 없이 데이터 가져오기](#bcp_widechar_import)를 참조하세요.

* **-w** 대신 **-c**스위치를 사용합니다.

* 원시 형식을 사용하여 데이터를 다시 내보냅니다.

* [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 또는 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)를 사용합니다.  이러한 해결 방법의 예제가 아래에 제공됩니다. [XML 이외의 서식 파일과 함께 BULK INSERT 및 유니코드 문자 형식 사용하기](#bulk_widechar_fmt) 및 [XML 이외의 서식 파일과 함께 OPENROWSET 및 유니코드 문자 형식 사용하기](#openrowset_widechar_fmt)를 참조하세요.
 
* 대상 테이블에 첫 번째 레코드를 수동으로 삽입한 다음 **-F 2** 스위치를 사용하여 가져오기가 두 번째 레코드에서 시작되게 합니다.

* 데이터 파일에 첫 번째 더미 레코드를 수동으로 삽입한 다음 **-F 2** 스위치를 사용하여 가져오기가 두 번째 레코드에서 시작되게 합니다.  이 해결 방법의 예제가 아래에 제공됩니다. [bcp 및 유니코드 문자 형식을 사용하여 XML 이외의 서식 파일과 함께 데이터 가져오기](#bcp_widechar_import_fmt)를 참조하세요.

* 첫 번째 열이 문자 데이터 형식인 준비 테이블을 사용합니다.

* 데이터를 다시 내보내고 첫 번째 데이터 필드가 문자가 되도록 데이터 필드 순서를 변경합니다.  그런 다음 서식 파일을 사용하여 테이블에서 데이터 필드를 실제 순서로 다시 매핑합니다.  예제는 [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑(SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)을 참조하세요.
  
## 유니코드 문자 형식의 명령 옵션<a name="command_options"></a>  
[bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 또는 [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)를 사용하여 테이블로 유니코드 문자 형식 데이터를 가져올 수 있습니다.  [bcp](../../tools/bcp-utility.md) 명령 또는 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 문의 경우 문에서 데이터 형식을 지정할 수 있습니다.  [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 문의 경우 서식 파일에서 데이터 형식을 지정해야 합니다.  
  
다음 명령 옵션에서 유니코드 문자 형식을 사용할 수 있습니다.  
  
|Command|옵션|설명|  
|-------------|------------|-----------------|  
|bcp|**-w**|유니코드 문자 형식을 사용합니다.|  
|BULK INSERT|DATAFILETYPE **='widechar'**|대량으로 데이터를 가져올 때 유니코드 문자 형식을 사용합니다.|  
|OPENROWSET|해당 사항 없음|서식 파일을 사용해야 합니다.|
  
> [!NOTE]
>  서식 파일에서 필드 단위로 서식을 지정할 수도 있습니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)를 참조하세요.
  
## 예제 테스트 조건<a name="etc"></a>  
이 항목의 예제는 아래에 정의된 테이블 및 서식 파일을 기반으로 합니다.

### **샘플 테이블**<a name="sample_table"></a>
아래 스크립트는 테스트 데이터베이스인 `myWidechar` 라는 테이블을 만들고 테이블을 몇 가지 초기 값으로 채웁니다.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myWidechar ( 
    PersonID smallint NOT NULL,
    FirstName nvarchar(25) NOT NULL,
    LastName nvarchar(30) NOT NULL,
    BirthDate date,
    AnnualSalary money
);

-- Populate table
INSERT TestDatabase.dbo.myWidechar
VALUES 
(1, N'ϴAnthony', N'Grosse', '02-23-1980', 65000.00),
(2, N'❤Alica', N'Fatnowna', '11-14-1963', 45000.00),
(3, N'☎Stella', N'Rossenhain', '03-02-1992', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myWidechar;
```

### **샘플 비 XML 서식 파일**<a name="nonxml_format_file"></a>
SQL Server는 두 유형의 서식 파일, 즉 비 XML 서식 파일과 XML 서식 파일을 지원합니다.  비 XML 서식 파일은 이전 버전의 SQL Server에서 원래 지원했던 서식 파일입니다.  자세한 내용은 [비 XML 서식 파일(SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 을 검토하세요.  다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myWidechar.fmt`의 스키마를 기반으로 비 xml 서식 파일 `myWidechar`를 생성합니다.  [bcp](../../tools/bcp-utility.md) 명령을 사용하여 서식 파일을 만들려면 데이터 파일 경로 대신 **format** 인수를 지정하고 **nul** 을 사용합니다.  format 옵션에는 **-f** 옵션도 필요합니다.  또한 이 예제에서 한정자 **c** 는 문자 데이터를 지정하는 데 사용되고 **T** 는 통합된 보안을 사용하여 신뢰할 수 있는 연결을 지정하는 데 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.

```
bcp TestDatabase.dbo.myWidechar format nul -f D:\BCP\myWidechar.fmt -T -w

REM Review file
Notepad D:\BCP\myWidechar.fmt
```

> [!IMPORTANT]
> 비 XML 서식 파일이 캐리지 리턴\줄 바꿈으로 끝나는지 확인하세요.  그러지 않으면 다음과 같은 오류 메시지가 표시될 수 있습니다.
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`


## 예<a name="examples"></a>
아래 예제에서는 위에서 만든 데이터베이스와 서식 파일을 사용합니다.

### **bcp 및 유니코드 문자 형식을 사용하여 데이터 내보내기**<a name="bcp_widechar_export"></a>
**-w** 스위치 및 **OUT** 명령.  참고: 이 예제에서 만든 데이터 파일은 이후 나오는 모든 예제에서 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.
```
bcp TestDatabase.dbo.myWidechar OUT D:\BCP\myWidechar.bcp -T -w

REM Review results
NOTEPAD D:\BCP\myWidechar.bcp
```

### **bcp 및 유니코드 문자 형식을 사용하여 서식 파일 없이 데이터 가져오기**<a name="bcp_widechar_import"></a>
**-w** 스위치 및 **IN** 명령.  명령 프롬프트에서 다음 명령을 입력합니다.
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidechar;"

REM Import data
bcp TestDatabase.dbo.myWidechar IN D:\BCP\myWidechar.bcp -T -w

REM Review results is SSMS
```

### **bcp 및 유니코드 문자 형식을 사용하여 XML 이외의 서식 파일과 함께 데이터 가져오기**<a name="bcp_widechar_import_fmt"></a>
**-w** 및 **-f** 스위치와 **IN** 명령.  이 예제에는 bcp, 서식 파일, 유니코드 문자가 포함되고 데이터 파일의 첫 번째 데이터 필드가 문자가 아니므로 해결 방법을 사용해야 합니다.  위의 [유니코드 문자 형식, bcp 및 서식 파일 사용 시 특별 고려 사항](#special_considerations).  추가 레코드를 “더미” 레코드로 추가하여 데이터 파일 `myWidechar.bcp` 를 변경한 다음 `-F 2` 스위치를 사용하여 이 레코드를 건너뜁니다.

명령 프롬프트에서 다음 명령을 입력하고 수정 단계를 수행합니다.
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidechar;"

REM Open data file
Notepad D:\BCP\myWidechar.bcp
REM Copy first record and then paste as new first record.  This additional record is the "dummy" record.
REM Close file.

REM Import data instructing bcp to skip dummy record with the -F 2 switch.
bcp TestDatabase.dbo.myWidechar IN D:\BCP\myWidechar.bcp -f D:\BCP\myWidechar.fmt -T -F 2

REM Review results is SSMS

REM Return data file to original state for usage in other examples
bcp TestDatabase.dbo.myWidechar OUT D:\BCP\myWidechar.bcp -T -w
```
  
### **서식 파일 없이 BULK INSERT 및 유니코드 문자 형식 사용**<a name="bulk_widechar"></a>
**DATAFILETYPE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar; -- for testing
BULK INSERT TestDatabase.dbo.myWidechar
    FROM 'D:\BCP\myWidechar.bcp'
    WITH (
        DATAFILETYPE = 'widechar'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
  
### **XML 이외의 서식 파일과 함께 BULK INSERT 및 유니코드 문자 형식 사용하기**<a name="bulk_widechar_fmt"></a>
**FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar; -- for testing
BULK INSERT TestDatabase.dbo.myWidechar
   FROM 'D:\BCP\myWidechar.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myWidechar.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
  
### **XML 이외의 서식 파일과 함께 OPENROWSET 및 유니코드 문자 형식 사용하기**<a name="openrowset_widechar_fmt"></a>
**FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar;  -- for testing
INSERT INTO TestDatabase.dbo.myWidechar
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myWidechar.bcp', 
        FORMATFILE = 'D:\BCP\myWidechar.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
 
  
## 관련 작업<a name="RelatedTasks"></a>
대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [원시 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [데이터를 가져오거나 내보내기 위해 유니코드 원시 형식 사용&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  

