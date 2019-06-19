---
title: 문자 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 09/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d129c6d0efb5659c0e10aa1c131b6e99a930896d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64946398"
---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>문자 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
다른 프로그램에서 사용할 텍스트 파일로 데이터를 대량으로 내보내거나 다른 프로그램에서 생성한 텍스트 파일에서 데이터를 대량으로 가져오는 경우 문자 형식을 사용하는 것이 좋습니다.  

문자 형식은 모든 열에 문자 데이터 형식을 사용합니다. 스프레드시트 등의 다른 프로그램에서 데이터를 사용하거나 Oracle 등의 다른 데이터베이스의 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 복사할 때는 문자 형식으로 정보를 저장하십시오.  
  
> [!NOTE]
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 유니코드 문자 데이터는 포함하지만 확장 문자 또는 DBCS(더블바이트 문자 집합) 문자는 포함하지 않는 데이터 파일 간에 데이터를 대량 전송하는 경우에는 유니코드 문자 형식을 사용하세요. 자세한 내용은 [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.
  
|항목 내용|
|---|
|[문자 형식 사용 시 고려 사항](#considerations)|
|[문자 형식의 명령 옵션](#command_options)|
|[예제 테스트 조건](#etc)<br />&emsp;&#9679;&emsp;[샘플 테이블](#sample_table)<br />&emsp;&#9679;&emsp;[샘플 비 XML 서식 파일](#nonxml_format_file)<br />|
|[예](#examples)<br />&emsp;&#9679;&emsp;[bcp 및 문자 형식을 사용하여 데이터 내보내기](#bcp_char_export)<br />&emsp;&#9679;&emsp;[bcp 및 문자 형식을 사용하여 서식 파일 없이 데이터 가져오기](#bcp_char_import)<br />&emsp;&#9679;&emsp;[bcp 및 문자 형식을 사용하여 XML 이외의 서식 파일과 함께 데이터 가져오기](#bcp_char_import_fmt)<br />&emsp;&#9679;&emsp;[서식 파일 없이 BULK INSERT 및 문자 형식 사용](#bulk_char)<br />&emsp;&#9679;&emsp;[XML 이외의 서식 파일과 함께 BULK INSERT 및 문자 형식 사용하기](#bulk_char_fmt)<br />&emsp;&#9679;&emsp;[XML 이외의 서식 파일과 함께 OPENROWSET 및 문자 형식 사용하기](#openrowset_char_fmt)|
|[관련 작업](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|


  
## 문자 형식 사용 시 고려 사항<a name="considerations"></a>
문자 형식을 사용할 때 다음 사항을 고려하십시오.  
  
-   기본적으로 [bcp 유틸리티](../../tools/bcp-utility.md) 는 탭 문자로 문자 데이터 필드를 구분하며 줄 바꿈 문자로 레코드를 종료합니다.  다른 종결자를 지정하는 방법에 대한 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.  
  
-   기본적으로 문자 모드의 데이터를 대량으로 내보내거나 대량으로 가져오기 전에 다음 변환이 수행됩니다.  
  
    |대량 작업의 방향|변환|  
    |---------------------------------|----------------|  
    |내보내기|데이터를 문자 표시로 변환합니다. 명시적으로 요청한 경우 문자 열에 요청한 코드 페이지로 데이터를 변환합니다. 코드 페이지를 지정하지 않으면 클라이언트 컴퓨터의 OEM 코드 페이지를 사용하여 문자 데이터를 변환합니다.|  
    |가져오기|필요한 경우 먼저 문자 데이터를 네이티브 표시로 변환하고 클라이언트의 코드 페이지에서 대상 열의 코드 페이지로 문자 데이터를 변환합니다.|  
  
-   변환 작업 중에 확장 문자가 손실되는 것을 방지하려면 유니코드 문자 형식을 사용하거나 코드 페이지를 지정하십시오.  
  
-   문자 서식 파일로 저장되는 모든 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 데이터는 메타데이터 없이 저장됩니다. 각 데이터 값은 암시적 데이터 변환 규칙에 따라 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 로 변환되며 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 열로 데이터를 가져오는 경우 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md)로 변환됩니다. [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 이외의 데이터 형식으로 열에 가져오는 경우 해당 데이터는 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md)에서 암시적 변환을 거칩니다. 데이터 변환에 대한 자세한 내용은 [데이터 형식 변환&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)을 참조하세요.  
  
-   [bcp 유틸리티](../../tools/bcp-utility.md)가 문자 형식 데이터 파일로서 [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) 값을 내보낼 때는 소수점 이하 4자리만 표시하며 쉼표 구분자 등 숫자 구분 기호는 사용하지 않습니다. 예를 들어 1,234,567.123456이라는 값을 포함하는 [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) 열을 데이터 파일로 대량 내보내면 1234567.1235라는 문자열이 됩니다.  
  
## 문자 형식의 명령 옵션<a name="command_options"></a>  
[bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 또는 [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)를 사용하여 테이블로 유니코드 문자 형식 데이터를 가져올 수 있습니다. [bcp](../../tools/bcp-utility.md) 명령 또는 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 문의 경우 문에서 데이터 형식을 지정할 수 있습니다.  [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 문의 경우 서식 파일에서 데이터 형식을 지정해야 합니다.  
  
문자 형식에 대해 지원되는 명령 옵션은 다음과 같습니다.  
  
|Command|옵션|설명|  
|-------------|------------|-----------------|  
|bcp|**-c**|bcp 유틸리티가 문자 데이터를 사용하도록 합니다.\*|  
|BULK INSERT|DATAFILETYPE **='char'**|데이터를 대량 가져올 때 문자 형식을 사용합니다.|  
|OPENROWSET|해당 사항 없음|서식 파일을 사용해야 합니다.|
  
 \*문자( **-c**) 데이터를 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트와 호환되는 형식으로 로드하려면 **-V** 스위치를 사용하세요. 자세한 내용은 [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)를 참조하세요.  
   
> [!NOTE]
>  서식 파일에서 필드 단위로 서식을 지정할 수도 있습니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)를 참조하세요.

## 예제 테스트 조건<a name="etc"></a>  
이 항목의 예제는 아래에 정의된 테이블 및 서식 파일을 기반으로 합니다.

### **샘플 테이블**<a name="sample_table"></a>
아래 스크립트는 테스트 데이터베이스인 `myChar` 라는 테이블을 만들고 테이블을 몇 가지 초기 값으로 채웁니다.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myChar ( 
   PersonID smallint NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date,
   AnnualSalary money
   );

-- Populate table
INSERT TestDatabase.dbo.myChar
VALUES 
(1, 'Anthony', 'Grosse', '1980-02-23', 65000.00),
(2, 'Alica', 'Fatnowna', '1963-11-14', 45000.00),
(3, 'Stella', 'Rossenhain', '1992-03-02', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myChar;
```

### **샘플 비 XML 서식 파일**<a name="nonxml_format_file"></a>
SQL Server는 두 유형의 서식 파일, 즉 비 XML 서식 파일과 XML 서식 파일을 지원합니다.  비 XML 서식 파일은 이전 버전의 SQL Server에서 원래 지원했던 서식 파일입니다.  자세한 내용은 [비 XML 서식 파일(SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 을 검토하세요.  다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myChar.fmt`의 스키마를 기반으로 비 xml 서식 파일 `myChar`를 생성합니다.  [bcp](../../tools/bcp-utility.md) 명령을 사용하여 서식 파일을 만들려면 데이터 파일 경로 대신 **format** 인수를 지정하고 **nul** 을 사용합니다.  format 옵션에는 **-f** 옵션도 필요합니다.  또한 이 예제에서 한정자 **c** 는 문자 데이터를 지정하는 데 사용되고 **T** 는 통합된 보안을 사용하여 신뢰할 수 있는 연결을 지정하는 데 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
bcp TestDatabase.dbo.myChar format nul -f D:\BCP\myChar.fmt -T -c 

REM Review file
Notepad D:\BCP\myChar.fmt
```

> [!IMPORTANT]
> 비 XML 서식 파일이 캐리지 리턴\줄 바꿈으로 끝나는지 확인하세요.  그러지 않으면 다음과 같은 오류 메시지가 표시될 수 있습니다.
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## 예<a name="examples"></a>
아래 예제에서는 위에서 만든 데이터베이스와 서식 파일을 사용합니다.

### **bcp 및 문자 형식을 사용하여 데이터 내보내기**<a name="bcp_char_export"></a>
**-c** 스위치 및 **OUT** 명령.  참고: 이 예제에서 만든 데이터 파일은 이후 나오는 모든 예제에서 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
bcp TestDatabase.dbo.myChar OUT D:\BCP\myChar.bcp -T -c

REM Review results
NOTEPAD D:\BCP\myChar.bcp
```

### **bcp 및 문자 형식을 사용하여 서식 파일 없이 데이터 가져오기**<a name="bcp_char_import"></a>
**-c** 스위치 및 **IN** 명령.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myChar;"

REM Import data
bcp TestDatabase.dbo.myChar IN D:\BCP\myChar.bcp -T -c

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myChar;"
```

### **bcp 및 문자 형식을 사용하여 XML 이외의 서식 파일과 함께 데이터 가져오기**<a name="bcp_char_import_fmt"></a>
**-c** 및 **-f** 스위치와 **IN** 명령.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myChar;"

REM Import data
bcp TestDatabase.dbo.myChar IN D:\BCP\myChar.bcp -f D:\BCP\myChar.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myChar;"
```

### **서식 파일 없이 BULK INSERT 및 문자 형식 사용**<a name="bulk_char"></a>
**DATAFILETYPE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar; -- for testing
BULK INSERT TestDatabase.dbo.myChar
    FROM 'D:\BCP\myChar.bcp'
    WITH (
        DATAFILETYPE = 'Char'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```

### **XML 이외의 서식 파일과 함께 BULK INSERT 및 문자 형식 사용하기**<a name="bulk_char_fmt"></a>
**FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar; -- for testing
BULK INSERT TestDatabase.dbo.myChar
   FROM 'D:\BCP\myChar.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myChar.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```

### **XML 이외의 서식 파일과 함께 OPENROWSET 및 문자 형식 사용하기**<a name="openrowset_char_fmt"></a>
**FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar;  -- for testing
INSERT INTO TestDatabase.dbo.myChar
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myChar.bcp', 
        FORMATFILE = 'D:\BCP\myChar.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```
  
## 관련 작업<a name="RelatedTasks"></a>  
대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면 
  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  
