---
title: 서식 파일을 사용하여 데이터 필드 건너뛰기
description: 필드 수가 테이블 열보다 많은 데이터 파일에 대해 서식 파일을 사용할 수 있습니다. 테이블 열을 해당 데이터 필드에 매핑하고 추가 필드를 무시합니다.
ms.date: 09/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 3f936706a855e810eefc8749a6c9296e855a9d57
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80980655"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>서식 파일을 사용하여 데이터 필드 건너뛰기(SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
데이터 파일에는 테이블의 열 수보다 많은 필드를 둘 수 있습니다. 이 항목에서는 테이블 열을 해당 데이터 필드에 매핑하고 나머지 필드는 무시하는 방법으로 데이터 파일에 더 많은 필드를 수용하도록 비 XML 서식 파일과 XML 서식 파일 모두를 수정하는 방법에 대해 설명합니다.  추가 정보는 [서식 파일 만들기(SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) 를 검토하세요.

|윤곽선|
|---|
|[예제 테스트 조건](#etc)<br />&emsp;&#9679;&emsp;[샘플 테이블](#sample_table)<br />&emsp;&#9679;&emsp;[샘플 데이터 파일](#sample_data_file)<br />[서식 파일 만들기](#create_format_file)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일 만들기](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일 사용](#modify_nonxml_format_file)<br />&emsp;&#9679;&emsp;[XML 서식 파일 만들기](#xml_format_file)<br />&emsp;&#9679;&emsp;[XML 서식 파일 사용](#modify_xml_format_file)<br />[서식 파일을 사용하여 데이터를 가져와 데이터 필드 건너뛰기](#import_data)<br />&emsp;&#9679;&emsp;[bcp 및 비 XML 서식 파일 사용](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[bcp 및 비 XML 서식 파일 사용](#bcp_xml)<br />&emsp;&#9679;&emsp;[BULK INSERT 및 비 XML 서식 파일 사용](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[BULK INSERT 및 XML 서식 파일 사용](#bulk_xml)<br />&emsp;&#9679;&emsp;[OPENROWSET(BULK...) 및 비 XML 서식 파일 사용](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[OPENROWSET(BULK...) 및 XML 서식 파일 사용](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
> [!NOTE]
>  비 XML 서식 파일 또는 XML 서식 파일은 [bcp 유틸리티](../../tools/bcp-utility.md) 명령, [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 문 또는 INSERT... SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 문을 사용하여 데이터 파일을 테이블에 대량으로 가져오는데 사용될 수 있습니다. 자세한 내용은 [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)를 참조하세요.

## <a name="example-test-conditions"></a>예제 테스트 조건<a name="etc"></a>  
이 항목의 수정된 서식 파일의 예는 아래 정의된 테이블 및 데이터 파일을 기준으로 합니다.
  
### <a name="sample-table"></a>샘플 테이블<a name="sample_table"></a>
아래 스크립트에서는 테스트 데이터베이스와 `myTestSkipField`라는 테이블을 만듭니다.  Microsoft SSMS(SQL Server Management Studio)에서 다음 TRANSACT-SQL을 실행합니다.
 
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE myTestSkipField
   (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30)
   );
```
  
### <a name="sample-data-file"></a>샘플 데이터 파일<a name="sample_data_file"></a>
빈 파일 `D:\BCP\myTestSkipField.bcp` 을 만들고 다음 데이터를 삽입합니다. 
```
1,SkipMe,Anthony,Grosse
2,SkipMe,Alica,Fatnowna
3,SkipMe,Stella,Rosenhain
```
  
## <a name="creating-the-format-files"></a>서식 파일 만들기<a name="create_format_file"></a>
`myTestSkipField.bcp` 의 데이터를 `myTestSkipField` 테이블로 대량으로 가져오려면 서식 파일에서 다음과 같은 작업을 수행해야 합니다.
* 첫 번째 데이터 필드를 첫 번째 열인 `PersonID`에 매핑합니다.
* 두 번째 데이터 필드를 건너뜁니다.
* 세 번째 데이터 필드를 두 번째 열인 `FirstName`에 매핑합니다.
* 네 번째 데이터 필드를 세 번째 열인 `LastName`에 매핑합니다.  

서식 파일을 만드는 가장 간단한 방법은 [bcp 유틸리티](../../tools/bcp-utility.md)를 사용하는 것입니다.  먼저 기존 테이블에서 기본 서식 파일을 만듭니다.  그다음으로 실제 데이터 파일을 반영하도록 기본 서식 파일을 수정합니다.
  
### <a name="creating-a-non-xml-format-file"></a><a name="nonxml_format_file"></a>비 XML 서식 파일 만들기 
자세한 내용은 [비 XML 서식 파일(SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 을 검토하세요. 다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myTestSkipField.fmt`의 스키마를 기반으로 비 xml 서식 파일 `myTestSkipField`를 생성합니다.  또한 한정자 `c` 는 문자 데이터를 지정하고, `t,` 는 쉼표를 필드 종결자로 지정하며, `T` 는 통합 보안을 사용하여 신뢰할 수 있는 연결을 지정합니다.  명령 프롬프트에서 다음 명령을 입력합니다.

```
bcp TestDatabase.dbo.myTestSkipField format nul -c -f D:\BCP\myTestSkipField.fmt -t, -T
```

### <a name="modifying-the-non-xml-format-file"></a>비 XML 서식 파일 수정 <a name="modify_nonxml_format_file"></a>
용어는 [비 XML 서식 파일의 구조](../../relational-databases/import-export/non-xml-format-files-sql-server.md#Structure) 를 참조하세요. 메모장에서 `D:\BCP\myTestSkipField.fmt` 를 열고 다음과 같이 수정합니다.
1) `FirstName` 에 대한 전체 서식 파일 행을 복사하고 그다음 줄에 `FirstName` 뒤에 직접 붙여 넣습니다.
2) 행이 새로 생기거나 모든 후속 행의 경우 호스트 파일 필드 순서 값을 하나씩 늘립니다.
3) 데이터 파일에서 실제 필드 수 반영을 위해 열 개수 값을 늘립니다.
3) 두 번째 서식 파일 행에서 서버 열 순서를 `2` 에서 `0` 으로 수정합니다. 

변경 내용을 비교합니다.  
**이전**
```
13.0
3
1       SQLCHAR 0       7       ","      1     PersonID     ""
2       SQLCHAR 0       25      ","      2     FirstName    SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       30      "\r\n"   3     LastName     SQL_Latin1_General_CP1_CI_AS
```
**이후**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID     ""
2       SQLCHAR 0       25      ","      0     FirstName    SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       25      ","      2     FirstName    SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       50      "\r\n"   3     LastName     SQL_Latin1_General_CP1_CI_AS

```

수정된 서식 파일에 이제 다음 내용이 반영됩니다.
* 4개의 데이터 필드
* `myTestSkipField.bcp` 의 첫 번째 데이터 필드가 다음 첫 번째 열에 매핑됨: `myTestSkipField.. PersonID`
* `myTestSkipField.bcp` 의 두 번째 데이터 필드가 어떤 열에도 매핑되지 않음
* `myTestSkipField.bcp` 의 세 번째 데이터 필드가 다음 두 번째 열에 매핑됨: `myTestSkipField.. FirstName`
* `myTestSkipField.bcp` 의 네 번째 데이터 필드가 다음 세 번째 열에 매핑됨: `myTestSkipField.. LastName`

### <a name="creating-an-xml-format-file"></a>XML 서식 파일 만들기 <a name="xml_format_file"></a>  
자세한 내용은 [XML 서식 파일(SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) 을 검토하세요.  다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myTestSkipField.xml`의 스키마를 기반으로 XML 서식 파일 `myTestSkipField`을 생성합니다.  또한 한정자 `c` 는 문자 데이터를 지정하고, `t,` 는 쉼표를 필드 종결자로 지정하며, `T` 는 통합 보안을 사용하여 신뢰할 수 있는 연결을 지정합니다.  `x` 한정자는 XML 기반 서식 파일을 생성하는 데 사용해야 합니다.  명령 프롬프트에서 다음 명령을 입력합니다.

```
bcp TestDatabase.dbo.myTestSkipField format nul -c -x -f D:\BCP\myTestSkipField.xml -t, -T
```

### <a name="modifying-the-xml-format-file"></a>XML 서식 파일 수정 <a name="modify_xml_format_file"></a>
용어는 [XML 서식 파일의 스키마 구문](../../relational-databases/import-export/xml-format-files-sql-server.md#StructureOfXmlFFs) 을 참조하세요.  메모장에서 `D:\BCP\myTestSkipField.xml` 를 열고 다음과 같이 수정합니다.
1) 전체 두 번째 필드를 복사하고 그다음 줄에서 두 번째 필드 뒤에 직접 붙여 넣습니다.
2) 새 필드 및 각 후속 필드에 대해 "FIELD ID" 값을 하나씩 늘립니다.
3) `FirstName`및 `LastName` 에 대해 "COLUMN SOURCE" 값을 하나씩 늘려 수정된 매핑을 반영합니다.

변경 내용을 비교합니다.  
**이전**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
 </ROW>
</BCPFORMAT>
```

**이후**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLVARYCHAR"/>
 </ROW>
</BCPFORMAT>
```

수정된 서식 파일에 이제 다음 내용이 반영됩니다.
* 4개의 데이터 필드
* 필드 1 - 열 1에 해당, 다음 첫 번째 테이블 열에 매핑: `myTestSkipField.. PersonID`
* 필드 1 - 어떤 열에도 해당되지 않음, 따라서 어떤 테이블 열에도 매핑되지 않음
* 필드 3 - 열 3에 해당, 다음 두 번째 테이블 열에 매핑: `myTestSkipField.. FirstName`
* 필드 4 - 열 4에 해당, 다음 세 번째 테이블 열에 매핑: `myTestSkipField.. LastName`

## <a name="importing-data-with-a-format-file-to-skip-a-data-field"></a>서식 파일을 사용하여 데이터를 가져와 데이터 필드 건너뛰기<a name="import_data"></a>
아래 예제에서는 위에서 만든 데이터베이스, 데이터 파일 및 서식 파일을 사용합니다.

### <a name="using-bcp-and-non-xml-format-file"></a>[bcp](../../tools/bcp-utility.md) 및 [비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bcp_nonxml"></a> 사용
명령 프롬프트에서 다음 명령을 입력합니다.
```
bcp TestDatabase.dbo.myTestSkipField IN D:\BCP\myTestSkipField.bcp -f D:\BCP\myTestSkipField.fmt -T
```

### <a name="using-bcp-and-xml-format-file"></a>[bcp](../../tools/bcp-utility.md) 및 [XML 서식 파일](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bcp_xml"></a> 사용
명령 프롬프트에서 다음 명령을 입력합니다.
```
bcp TestDatabase.dbo.myTestSkipField IN D:\BCP\myTestSkipField.bcp -f D:\BCP\myTestSkipField.xml -T
```

### <a name="using-bulk-insert-and-non-xml-format-file"></a>[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bulk_nonxml"></a> 사용
Microsoft SSMS(SQL Server Management Studio)에서 다음 TRANSACT-SQL을 실행합니다.
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
BULK INSERT dbo.myTestSkipField   
   FROM 'D:\BCP\myTestSkipField.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myTestSkipField.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### <a name="using-bulk-insert-and-xml-format-file"></a>[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [XML 서식 파일](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bulk_xml"></a> 사용
Microsoft SSMS(SQL Server Management Studio)에서 다음 TRANSACT-SQL을 실행합니다.
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
BULK INSERT dbo.myTestSkipField   
   FROM 'D:\BCP\myTestSkipField.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myTestSkipField.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### <a name="using-openrowsetbulk-and-non-xml-format-file"></a>[OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 및 [비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="openrowset_nonxml"></a> 사용    
Microsoft SSMS(SQL Server Management Studio)에서 다음 TRANSACT-SQL을 실행합니다.
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myTestSkipField;
INSERT INTO dbo.myTestSkipField
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myTestSkipField.bcp',
        FORMATFILE = 'D:\BCP\myTestSkipField.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### <a name="using-openrowsetbulk-and-xml-format-file"></a>[OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 및 [XML 서식 파일](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="openrowset_xml"></a> 사용
Microsoft SSMS(SQL Server Management Studio)에서 다음 TRANSACT-SQL을 실행합니다.
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
INSERT INTO dbo.myTestSkipField 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myTestSkipField.bcp',
        FORMATFILE = 'D:\BCP\myTestSkipField.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

  
## <a name="see-also"></a>참고 항목  
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
