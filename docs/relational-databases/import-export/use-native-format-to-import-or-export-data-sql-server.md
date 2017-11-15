---
title: "네이티브 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 09/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 84119273dd16025dbb116c639dca688349e7e009
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>네이티브 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server)
확장/DBCS(더블바이트 문자 집합) 문자가 포함되어 있지 않은 데이터 파일을 사용하여 여러 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 데이터를 대량 전송할 때는 네이티브 형식을 사용하는 것이 바람직합니다.  

> [!NOTE]
>  확장 또는 DBCS 문자가 포함되어 있는 데이터 파일을 사용하여 여러 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 데이터를 대량 전송하려면 유니코드 네이티브 형식을 사용해야 합니다. 자세한 내용은 [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)을 참조하세요.

네이티브 형식은 데이터베이스의 원래 데이터 형식을 유지합니다. 네이티브 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 간에 데이터를 빠르게 전송하기 위한 형식입니다. 서식 파일을 사용할 경우 원본 및 대상 테이블의 형식이 동일할 필요가 없습니다. 데이터 전송은 두 단계로 이루어집니다.  
  
1.  원본 테이블에서 데이터 파일로 데이터 대량 내보내기  
  
2.  데이터 파일에서 대상 테이블로 데이터 대량 가져오기  
  
형식이 동일한 테이블에서는 네이티브 형식을 사용하여 문자 형식의 불필요한 변환을 없애고 시간과 공간을 절약할 수 있습니다. 이때 최적의 전송 속도를 얻기 위해 데이터 형식을 거의 검사하지 않습니다. 로드된 데이터와 관련된 문제를 방지하려면 다음 제한 사항 목록을 참조하십시오.  

|항목 내용|
|---|
|[제한 사항](#restrictions)|
|[bcp의 네이티브 형식 데이터 처리 방법](#considerations)|
|[네이티브 형식의 명령 옵션](#command_options)|
|[예제 테스트 조건](#etc)<br /><br />&emsp;&#9679;&emsp;[샘플 테이블](#sample_table)<br />&emsp;&#9679;&emsp;[샘플 비 XML 서식 파일](#nonxml_format_file)|
|[예](#examples)<br />&emsp;&#9679;&emsp;[bcp 및 원시 형식을 사용하여 데이터 내보내기](#bcp_native_export)<br />&emsp;&#9679;&emsp;[bcp 및 원시 형식을 사용하여 서식 파일 없이 데이터 가져오기](#bcp_native_import)<br />&emsp;&#9679;&emsp;[bcp 및 원시 형식을 사용하여 XML 이외의 서식 파일과 함께 데이터 가져오기](#bcp_native_import_fmt)<br />&emsp;&#9679;&emsp;[서식 파일 없이 BULK INSERT 및 원시 형식 사용](#bulk_native)<br />&emsp;&#9679;&emsp;[XML 이외의 서식 파일과 함께 BULK INSERT 및 원시 형식 사용하기](#bulk_native_fmt)<br />&emsp;&#9679;&emsp;[XML 이외의 서식 파일과 함께 OPENROWSET 및 원시 형식 사용하기](#openrowset_native_fmt)|
|[관련 태스크](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|

## 제한 사항<a name="restrictions"></a>  
데이터를 네이티브 형식으로 가져오려면 다음 사항을 확인하십시오.  
  
-   데이터 파일이 네이티브 형식인지 여부  
  
-   대상 테이블이 데이터 파일과 호환되는지 여부(예: 올바른 열 수, 데이터 형식, 길이, NULL 상태 등). 호환되지 않을 경우 각 필드를 해당 열에 매핑하기 위해 서식 파일을 사용해야 합니다.  
  
    > [!NOTE]
    >  대상 테이블과 형식이 일치하지 않는 파일의 데이터를 가져오면 가져오기 작업에 성공하더라도 대상 테이블에 삽입된 데이터 값이 올바르지 않을 가능성이 높습니다. 이는 파일의 데이터가 대상 테이블의 서식을 사용하여 해석되기 때문입니다. 따라서 형식이 일치하지 않으면 잘못된 값이 삽입됩니다. 하지만 어떤 경우에도 이러한 불일치가 데이터베이스와의 논리적 또는 물리적 불일치를 유발하지는 않습니다.  
  
     서식 파일 사용에 대한 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)을 참조하세요.  
  
 데이터를 성공적으로 가져온 경우 대상 테이블은 손상되지 않습니다.  
  
## bcp의 네이티브 형식 데이터 처리 방법<a name="considerations"></a>
 이 섹션에서는 **bcp** 유틸리티가 데이터를 네이티브 형식으로 내보내고 가져오는 방법에 대한 특별한 고려 사항에 대해 설명합니다.  
  
-   문자가 아닌 데이터  
  
     [bcp 유틸리티](../../tools/bcp-utility.md) 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 이진 데이터 형식을 사용하여 문자가 아닌 테이블의 데이터를 데이터 파일에 기록합니다.  
  
-   [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 또는 [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) 데이터  
  
     [bcp](../../t-sql/data-types/char-and-varchar-transact-sql.md) 는 각 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 또는 [varchar](../../tools/bcp-utility.md) 필드의 처음 부분에 접두사 길이를 추가합니다.  
  
    > [!IMPORTANT]
    >  기본 모드를 사용하면 기본적으로 [bcp 유틸리티](../../tools/bcp-utility.md) 가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 문자를 데이터 파일에 복사하기 전에 OEM 문자로 변환합니다. 반대로 데이터 파일의 문자를 [테이블에 대량으로 가져올 때는](../../tools/bcp-utility.md) bcp 유틸리티 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 문자를 ANSI 문자로 변환합니다. 이러한 변환 과정에서 확장 문자 데이터가 손실될 수 있습니다. 확장 문자의 경우 유니코드 네이티브 형식을 사용하거나 코드 페이지를 지정하십시오.
  
-   [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 데이터  
  
     [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 데이터가 네이티브 형식 데이터 파일에 SQLVARIANT로 저장되면 해당 데이터는 그 특성을 모두 유지합니다. 각 데이터 값의 데이터 형식을 기록하는 메타데이터는 데이터 값과 함께 저장됩니다. 이 메타데이터는 대상 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 열에 동일한 데이터 형식을 가진 데이터 값을 다시 만드는 데 사용됩니다.  
  
     대상 열의 데이터 형식이 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)가 아닌 경우 기본적인 암시적 데이터 변환 규칙에 따라 각 데이터 값이 대상 열의 데이터 형식으로 변환됩니다. 데이터 변환 중에 오류가 발생하면 현재 일괄 처리가 롤백됩니다. [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 열 간에 전송되는 모든 [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 및 [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) 값에는 코드 페이지 변환 문제가 있을 수 있습니다.  
  
     데이터 변환에 대한 자세한 내용은 [데이터 형식 변환&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)을 참조하세요.  
  
## 네이티브 형식의 명령 옵션<a name="command_options"></a>  
[bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 또는 [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)를 사용하여 테이블로 유니코드 문자 형식 데이터를 가져올 수 있습니다.  [bcp](../../tools/bcp-utility.md) 명령 또는 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 문의 경우 문에서 데이터 형식을 지정할 수 있습니다.  [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 문의 경우 서식 파일에서 데이터 형식을 지정해야 합니다.  

원시 형식에 대해 지원되는 명령 옵션은 다음과 같습니다.  

|Command|옵션|설명|  
|-------------|------------|-----------------|  
|bcp|**-n**|bcp 유틸리티가 원시 데이터 형식을 사용하도록 합니다.*|  
|BULK INSERT|DATAFILETYPE **='native'**|데이터의 네이티브 또는 와이드 네이티브 데이터 형식을 사용합니다. 서식 파일로 데이터 형식을 지정하면 DATAFILETYPE은 필요하지 않습니다.|  
|OPENROWSET|해당 사항 없음|서식 파일을 사용해야 합니다.|

  
 \*네이티브(**-n**) 데이터를 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트와 호환되는 형식으로 로드하려면 **-V** 스위치를 사용합니다. 자세한 내용은 [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)를 참조하세요.  
  
> [!NOTE]
>  서식 파일에서 필드 단위로 서식을 지정할 수도 있습니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)를 참조하세요.
  

## 예제 테스트 조건<a name="etc"></a>  
이 항목의 예제는 아래에 정의된 테이블 및 서식 파일을 기반으로 합니다.

### **샘플 테이블**<a name="sample_table"></a>
아래 스크립트는 테스트 데이터베이스인 `myNative` 라는 테이블을 만들고 테이블을 몇 가지 초기 값으로 채웁니다.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myNative ( 
   PersonID smallint NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date,
   AnnualSalary money
   );

-- Populate table
INSERT TestDatabase.dbo.myNative
VALUES 
(1, 'Anthony', 'Grosse', '1980-02-23', 65000.00),
(2, 'Alica', 'Fatnowna', '1963-11-14', 45000.00),
(3, 'Stella', 'Rossenhain', '1992-03-02', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myNative;
```

### **샘플 비 XML 서식 파일**<a name="nonxml_format_file"></a>
SQL Server는 두 유형의 서식 파일, 즉 비 XML 서식 파일과 XML 서식 파일을 지원합니다.  비 XML 서식 파일은 이전 버전의 SQL Server에서 원래 지원했던 서식 파일입니다.  자세한 내용은 [비 XML 서식 파일(SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 을 검토하세요.  다음 명령은 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 `myNative.fmt`의 스키마를 기반으로 비 xml 서식 파일 `myNative`를 생성합니다.  [bcp](../../tools/bcp-utility.md) 명령을 사용하여 서식 파일을 만들려면 데이터 파일 경로 대신 **format** 인수를 지정하고 **nul** 을 사용합니다.  format 옵션에는 **-f** 옵션도 필요합니다.  또한 이 예제에서 한정자 **c** 는 문자 데이터를 지정하는 데 사용되고 **T** 는 통합된 보안을 사용하여 신뢰할 수 있는 연결을 지정하는 데 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
bcp TestDatabase.dbo.myNative format nul -f D:\BCP\myNative.fmt -T -n 

REM Review file
Notepad D:\BCP\myNative.fmt
```

> [!IMPORTANT]
> 비 XML 서식 파일이 캐리지 리턴\줄 바꿈으로 끝나는지 확인하세요.  그러지 않으면 다음과 같은 오류 메시지가 표시될 수 있습니다.
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## 예<a name="examples"></a>
아래 예제에서는 위에서 만든 데이터베이스와 서식 파일을 사용합니다.

### **bcp 및 원시 형식을 사용하여 데이터 내보내기**<a name="bcp_native_export"></a>
**-n** 스위치 및 **OUT** 명령.  참고: 이 예제에서 만든 데이터 파일은 이후 나오는 모든 예제에서 사용됩니다.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
bcp TestDatabase.dbo.myNative OUT D:\BCP\myNative.bcp -T -n

REM Review results
NOTEPAD D:\BCP\myNative.bcp
```

### **bcp 및 원시 형식을 사용하여 서식 파일 없이 데이터 가져오기**<a name="bcp_native_import"></a>
**-n** 스위치 및 **IN** 명령.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNative;"

REM Import data
bcp TestDatabase.dbo.myNative IN D:\BCP\myNative.bcp -T -n

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNative;"
```

### **bcp 및 원시 형식을 사용하여 XML 이외의 서식 파일과 함께 데이터 가져오기**<a name="bcp_native_import_fmt"></a>
**-n** 열 간에 전송되는 모든 **-f** 스위치와 **IN** 명령.  명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNative;"

REM Import data
bcp TestDatabase.dbo.myNative IN D:\BCP\myNative.bcp -f D:\BCP\myNative.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNative;"
```

### **서식 파일 없이 BULK INSERT 및 원시 형식 사용**<a name="bulk_native"></a>
**DATAFILETYPE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative; -- for testing
BULK INSERT TestDatabase.dbo.myNative
    FROM 'D:\BCP\myNative.bcp'
    WITH (
        DATAFILETYPE = 'native'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```

### **XML 이외의 서식 파일과 함께 BULK INSERT 및 원시 형식 사용하기**<a name="bulk_native_fmt"></a>
**FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative; -- for testing
BULK INSERT TestDatabase.dbo.myNative
   FROM 'D:\BCP\myNative.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNative.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```

### **XML 이외의 서식 파일과 함께 OPENROWSET 및 원시 형식 사용하기**<a name="openrowset_native_fmt"></a>
**FORMATFILE** 인수.  Microsoft SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 다음 Transact-SQL을 실행합니다.

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative;  -- for testing
INSERT INTO TestDatabase.dbo.myNative
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNative.bcp', 
        FORMATFILE = 'D:\BCP\myNative.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```
  
## 관련 작업<a name="RelatedTasks"></a>
대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면 
  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [sql_variant&#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)   
 [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
