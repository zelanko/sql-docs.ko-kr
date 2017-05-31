---
title: "서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 09/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping columns to fields during import [SQL Server]
- format files [SQL Server], mapping columns to fields
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d90982485ab979118f4f7b02881aa8ea53cc9818
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server"></a>서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑(SQL Server)
데이터 파일은 테이블의 해당 열에서 서로 다른 순서로 정렬된 필드를 포함할 수 있습니다. 이 항목에서는 테이블 열과 서로 다른 순서로 필드가 정렬된 데이터 파일에 맞게 수정된 비 XML 및 XML 서식 파일에 대해 설명합니다. 수정된 서식 파일은 데이터 필드를 해당 테이블 열로 매핑합니다.  추가 정보는 [서식 파일 만들기(SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) 를 검토하세요.

|윤곽선|
|---|
|[예제 테스트 조건](#etc)<br />&emsp;&#9679;&emsp;[샘플 테이블](#sample_table)<br />&emsp;&#9679;&emsp;[샘플 데이터 파일](#sample_data_file)<br />[서식 파일 만들기](#create_format_file)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일 만들기](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[비 XML 서식 파일 수정](#modify_nonxml_format_file)<br />&emsp;&#9679;&emsp;[XML 서식 파일 만들기](#xml_format_file)<br />&emsp;&#9679;&emsp;[XML 서식 파일 수정](#modify_xml_format_file)<br />[서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑](#import_data)<br />&emsp;&#9679;&emsp;[bcp 및 비 XML 서식 파일 사용](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[bcp 및 비 XML 서식 파일 사용](#bcp_xml)<br />&emsp;&#9679;&emsp;[BULK INSERT 및 비 XML 서식 파일 사용](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[BULK INSERT 및 XML 서식 파일 사용](#bulk_xml)<br />&emsp;&#9679;&emsp;[OPENROWSET(BULK...) 및 비 XML 서식 파일 사용](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[OPENROWSET(BULK...) 및 XML 서식 파일 사용](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|

> [!NOTE]  
>  비 XML 서식 파일 또는 XML 서식 파일은 [bcp 유틸리티](../../tools/bcp-utility.md) 명령, [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 문 또는 INSERT... SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 문을 사용하여 데이터 파일을 테이블에 대량으로 가져오는데 사용될 수 있습니다. 자세한 내용은 [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)를 참조하세요.  

## 예제 테스트 조건<a name="etc"></a>  
이 항목의 수정된 서식 파일의 예는 아래 정의된 테이블 및 데이터 파일을 기준으로 합니다.

### 샘플 테이블<a name="sample_table"></a>
아래 스크립트에서는 테스트 데이터베이스와 `myRemap`라는 테이블을 만듭니다.  Microsoft SSMS(SQL Server Management Studio)에서 다음 TRANSACT-SQL을 실행합니다.
```tsql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE myRemap
   (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   Gender char(1)
   );
```

### 샘플 데이터 파일<a name="sample_data_file"></a>
아래 데이터는 `FirstName` 및 `LastName` 을 나타내며 `myRemap`테이블에 표시된 순서와 반대입니다.  메모장을 사용하여 빈 파일 `D:\BCP\myRemap.bcp` 을 만들고 다음 데이터를 삽입합니다.
```
1,Grosse,Anthony,M
2,Fatnowna,Alica,F
3,Rosenhain,Stella,F
```

## 서식 파일 만들기<a name="create_format_file"></a>
`myRemap.bcp` 의 데이터를 `myRemap` 테이블로 대량으로 가져오려면 서식 파일에서 다음과 같은 작업을 수행해야 합니다.
* 첫 번째 데이터 필드를 첫 번째 열인 `PersonID`에 매핑합니다.
* 두 번째 데이터 필드를 세 번째 열인 `LastName`에 매핑합니다.
* 세 번째 데이터 필드를 두 번째 열인 `FirstName`에 매핑합니다.
* 네 번째 데이터 필드를 네 번째 열인 `Gender`에 매핑합니다.

서식 파일을 만드는 가장 간단한 방법은 [bcp 유틸리티](../../tools/bcp-utility.md)를 사용하는 것입니다.  먼저 기존 테이블에서 기본 서식 파일을 만듭니다.  그다음으로 실제 데이터 파일을 반영하도록 기본 서식 파일을 수정합니다.

### 비 XML 서식 파일 만들기<a name="nonxml_format_file"></a>
자세한 내용은 [비 XML 서식 파일(SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 을 검토하세요. 다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myRemap.fmt`의 스키마를 기반으로 비 XML 서식 파일 `myRemap`를 생성합니다.  또한 한정자 `c` 는 문자 데이터를 지정하고, `t,` 는 쉼표를 필드 종결자로 지정하며, `T` 는 통합 보안을 사용하여 신뢰할 수 있는 연결을 지정합니다.  명령 프롬프트에서 다음 명령을 입력합니다.
```
bcp TestDatabase.dbo.myRemap format nul -c -f D:\BCP\myRemap.fmt -t, -T
```
### 비 XML 서식 파일 수정 <a name="modify_nonxml_format_file"></a>
용어는 [비 XML 서식 파일의 구조](../../relational-databases/import-export/non-xml-format-files-sql-server.md#Structure) 를 참조하세요.  메모장에서 `D:\BCP\myRemap.fmt` 를 열고 다음과 같이 수정합니다.
1) 행이 `myRemap.bcp`의 데이터와 순서가 동일하도록 서식 파일 행 순서를 다시 정렬합니다.
2) 호스트 파일 필드 순서 값이 순차적인지 확인합니다.
3) 마지막 서식 파일 행 다음에 캐리지 리턴이 있는지 확인합니다.

변경 내용을 비교합니다.     
**이전**
```
13.0
4
1       SQLCHAR    0       7       ","      1     PersonID               ""
2       SQLCHAR    0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR    0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR    0       1       "\r\n"   4     Gender                 SQL_Latin1_General_CP1_CI_AS

```
**After**
```
13.0
4
1       SQLCHAR    0       7       ","      1     PersonID               ""
2       SQLCHAR    0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR    0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR    0       1       "\r\n"   4     Gender                 SQL_Latin1_General_CP1_CI_AS

```
수정된 서식 파일에 이제 다음 내용이 반영됩니다.
* `myRemap.bcp` 의 첫 번째 데이터 필드가 다음 첫 번째 열에 매핑됨: ` myRemap.. PersonID`
* `myRemap.bcp` 의 두 번째 데이터 필드가 다음 세 번째 열에 매핑됨: `myRemap.. LastName`
* `myRemap.bcp` 의 세 번째 데이터 필드가 다음 두 번째 열에 매핑됨: `myRemap.. FirstName`
* `myRemap.bcp` 의 네 번째 데이터 필드가 다음 네 번째 열에 매핑됨: ` myRemap.. Gender`

### XML 서식 파일 만들기 <a name="xml_format_file"></a>  
자세한 내용은 [XML 서식 파일(SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) 을 검토하세요.  다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myRemap.xml`의 스키마를 기반으로 XML 서식 파일 `myRemap`을 생성합니다.  또한 한정자 `c` 는 문자 데이터를 지정하고, `t,` 는 쉼표를 필드 종결자로 지정하며, `T` 는 통합 보안을 사용하여 신뢰할 수 있는 연결을 지정합니다.  `x` 한정자는 XML 기반 서식 파일을 생성하는 데 사용해야 합니다.  명령 프롬프트에서 다음 명령을 입력합니다.
```
bcp TestDatabase.dbo.myRemap format nul -c -x -f D:\BCP\myRemap.xml -t, -T
```
### XML 서식 파일 수정 <a name="modify_xml_format_file"></a>
용어는 [XML 서식 파일의 스키마 구문](../../relational-databases/import-export/xml-format-files-sql-server.md#StructureOfXmlFFs) 을 참조하세요.  메모장에서 `D:\BCP\myRemap.xml`를 열고 다음과 같이 수정합니다.
1) 서식 파일에서 \<FIELD> elements가 선언되는 순서는 이들 필드가 데이터 파일에 나열되는 순서로, ID 특성이 2이고 3인 \<FIELD> elements 순서와 반대가 됩니다.
2) \<필드 > ID 특성 값이 순차적인지 확인합니다.
3) \<ROW> 요소에서 \<COLUMN> 요소의 순서에 따라 대량 작업에서 반환되는 순서가 정의됩니다.  XML 서식 파일은 각 \<COLUMN> 요소에 대량 가져오기 작업의 대상 테이블에 있는 열과 관계가 없는 로컬 이름을 지정합니다.  \<COLUMN> 요소의 순서는 \<RECORD> 정의에 있는 \<FIELD> 요소의 순서와는 독립적입니다.  각 \<COLUMN> 요소는 ID가 \<COLUMN> 요소의 SOURCE 특성에서 지정되는 \<FIELD> 요소에 해당합니다.  따라서 \<COLUMN> SOURCE에 대한 값은 버전이 필요한 특성뿐입니다.  \<COLUMN> SOURCE 특성 2와 3에 대한 순서를 반대로 설정합니다.

변경 내용을 비교합니다.  
**이전**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="1" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="Gender" xsi:type="SQLCHAR"/>
 </ROW>
</BCPFORMAT>
```
**After**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="1" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="2" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="Gender" xsi:type="SQLCHAR"/>
 </ROW>
</BCPFORMAT>
```
수정된 서식 파일에 이제 다음 내용이 반영됩니다.
* 필드 1 - 열 1에 해당, 다음 첫 번째 테이블 열에 매핑: `myRemap.. PersonID`
* 필드 2 - 열 2에 해당, 다음 세 번째 테이블 열에 다시 매핑: `myRemap.. LastName`
* 필드 3 - 열 2에 해당, 다음 두 번째 테이블 열에 다시 매핑: `myRemap.. FirstName`
* 필드 4 - 열 4에 해당, 다음 네 번째 테이블 열에 매핑: `myRemap.. Gender`


## 서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑<a name="import_data"></a>
아래 예제에서는 위에서 만든 데이터베이스, 데이터 파일 및 서식 파일을 사용합니다.

### [bcp](../../tools/bcp-utility.md) 및 [비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bcp_nonxml"></a> 사용
명령 프롬프트에서 다음 명령을 입력합니다.
```
bcp TestDatabase.dbo.myRemap IN D:\BCP\myRemap.bcp -f D:\BCP\myRemap.fmt -T
```

### [bcp](../../tools/bcp-utility.md) 및 [XML 서식 파일](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bcp_xml"></a> 사용
명령 프롬프트에서 다음 명령을 입력합니다.
```
bcp TestDatabase.dbo.myRemap IN D:\BCP\myRemap.bcp -f D:\BCP\myRemap.xml -T
```

### [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bulk_nonxml"></a> 사용
Microsoft SSMS(SQL Server Management Studio)에서 다음 TRANSACT-SQL을 실행합니다.
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
BULK INSERT dbo.myRemap   
   FROM 'D:\BCP\myRemap.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myRemap.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [XML 서식 파일](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bulk_xml"></a> 사용
Microsoft SSMS(SQL Server Management Studio)에서 다음 TRANSACT-SQL을 실행합니다.
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
BULK INSERT dbo.myRemap   
   FROM 'D:\BCP\myRemap.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myRemap.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 및 [비 XML 서식 파일](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="openrowset_nonxml"></a> 사용    
Microsoft SSMS(SQL Server Management Studio)에서 다음 TRANSACT-SQL을 실행합니다.
```tsql
USE TestDatabase;
GO

TRUNCATE TABLE myRemap;
INSERT INTO dbo.myRemap
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myRemap.bcp',
        FORMATFILE = 'D:\BCP\myRemap.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 및 [XML 서식 파일](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="openrowset_xml"></a> 사용
Microsoft SSMS(SQL Server Management Studio)에서 다음 TRANSACT-SQL을 실행합니다.
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
INSERT INTO dbo.myRemap 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myRemap.bcp',
        FORMATFILE = 'D:\BCP\myRemap.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```


  
## <a name="see-also"></a>관련 항목:  
[bcp Utility](../../tools/bcp-utility.md)   
 [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  

