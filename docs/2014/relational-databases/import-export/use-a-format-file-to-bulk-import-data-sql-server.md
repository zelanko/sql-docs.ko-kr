---
title: 서식 파일을 사용하여 데이터 대량 가져오기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 772dbb86188bf164a2e135f7bb9b71a1cc030745
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011764"
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>서식 파일을 사용하여 데이터 대량 가져오기(SQL Server)
  이 항목에서는 대량 가져오기 작업에서 서식 파일을 사용하는 방법에 대해 설명합니다. 서식 파일은 데이터 파일의 필드를 테이블 열에 매핑합니다.  **bcp** 명령이나 BULK INSERT 또는 INSERT ...를 사용할 때 비 XML 서식 파일 또는 XML 서식 파일을 사용하여 데이터를 대량으로 가져올 수 있습니다. SELECT * FROM OPENROWSET(BULK...) [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 사용하는 경우 비 XML 또는 XML 형식 파일을 사용하여 데이터를 대량으로 가져올 수 있습니다.  
  
> [!IMPORTANT]  
>  유니코드 문자 데이터 파일에 서식 파일을 사용하려면 모든 입력 필드가 유니코드 텍스트 문자열(고정 크기 또는 문자 종료 유니코드 문자열)이어야 합니다.  
  
> [!NOTE]  
>  서식 파일을 사용 하 여 잘 모르는 경우 [비 XML 서식 파일 &#40;SQL Server&#41; ](xml-format-files-sql-server.md) 하 고 [XML 서식 파일 &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="format-file-options-for-bulk-import-commands"></a>대량 가져오기 명령의 서식 파일 옵션  
 다음 표에서는 대량 가져오기 명령 각각에 대한 서식 파일 옵션을 요약하여 보여 줍니다.  
  
|대량 로드 명령|서식 파일 옵션 사용|  
|------------------------|-----------------------------------|  
|BULK INSERT|FORMATFILE = '*format_file_path*'|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|FORMATFILE = '*format_file_path*'|  
|**bcp** ... **에서**|**-f** *format_file*|  
  
 자세한 내용은 [bcp 유틸리티](../../tools/bcp-utility.md), [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) 또는 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)를 참조하세요.  
  
> [!NOTE]  
>  SQLXML 데이터를 대량으로 내보내거나 가져오려면 서식 파일에서 다음 데이터 형식 중 하나를 사용합니다. SQLCHAR 또는 SQLVARYCHAR(데이터 정렬에 의해 포함된 코드 페이지나 클라이언트 코드 페이지로 데이터가 전송됨), SQLNCHAR 또는 SQLNVARCHAR(데이터가 유니코드로 전송됨), SQLBINARY 또는 SQLVARYBIN(데이터가 변환되지 않고 전송됨) 데이터 형식 중 하나를 사용합니다.  
  
## <a name="examples"></a>예  
 이 섹션의 예제에서는 **bcp** 명령과 BULK INSERT 및 INSERT ... SELECT * FROM OPENROWSET(BULK...) 문은 분할 뷰로 데이터를 대량 가져오는 것을 지원하지 않습니다. 대량 가져오기 예를 실행하려면 먼저 예제 테이블, 데이터 파일 및 서식 파일을 만들어야 합니다.  
  
### <a name="sample-table"></a>예제 테이블  
 이 예에서는 **dbo** 스키마의 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 예제 데이터베이스에 **myTestFormatFiles** 라는 테이블을 만들어야 합니다. 이 테이블을 만들려면 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestFormatFiles (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50),  
   Col4 nvarchar(50)  
   );  
GO  
```  
  
### <a name="sample-data-file"></a>예제 데이터 파일  
 예에서는 다음 레코드가 들어 있는 `myTestFormatFiles-c.Dat`예제 데이터 파일을 사용합니다. 데이터 파일을 만들려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
10,Field2,Field3,Field4  
15,Field2,Field3,Field4  
46,Field2,Field3,Field4  
58,Field2,Field3,Field4  
```  
  
### <a name="sample-format-files"></a>예제 서식 파일  
 이 섹션의 일부 예에서는 XML 서식 파일 `myTestFormatFiles-f-x-c.Xml`을 사용하고 다른 예에서는 비 XML 서식 파일을 사용합니다. 두 서식 파일은 모두 문자 데이터 형식과 비기본 필드 종결자(,)를 사용합니다.  
  
#### <a name="the-sample-non-xml-format-file"></a>예제 비 XML 서식 파일  
 다음 예에서는 **bcp** 를 사용하여 `myTestFormatFiles` 테이블에서 XML 서식 파일을 생성합니다. `myTestFormatFiles.Fmt` 파일은 다음 정보를 포함합니다.  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       100     ","      2     Col2         SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      3     Col3         SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   4     Col4         SQL_Latin1_General_CP1_CI_AS  
```  
  
 **bcp** 에 **format** 옵션을 사용하여 이러한 서식 파일을 만들려면 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -f myTestFormatFiles.Fmt -T  
  
```  
  
 서식 파일을 만드는 방법은 [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)를 참조하세요.  
  
#### <a name="the-sample-xml-format-file"></a>예제 XML 서식 파일  
 다음 예에서는 **bcp** 를 사용하여 `myTestFormatFiles` 테이블에서 XML 서식 파일을 만듭니다. `myTestFormatFiles.Xml` 파일은 다음 정보를 포함합니다.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 **bcp** 에 **format** 옵션을 사용하여 이러한 서식 파일을 만들려면 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -x -f myTestFormatFiles.Xml -T  
```  
  
### <a name="using-bcp"></a>bcp 사용  
 다음 예에서는 **bcp** 을 사용하여 `myTestFormatFiles-c.Dat` 데이터 파일에서 예제 데이터베이스의 `HumanResources.myTestFormatFiles` 테이블로 데이터를 대량으로 가져옵니다. 이 예에서는 XML 서식 파일인 `MyTestFormatFiles.Xml`을 사용합니다. 또한 데이터 파일을 가져오기 전에 기존 테이블 행을 모두 삭제합니다.  
  
 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks2012..myTestFormatFiles in C:\myTestFormatFiles-c.Dat -f C:\myTestFormatFiles.Xml -T  
```  
  
> [!NOTE]  
>  이 명령에 대한 자세한 내용은 [bcp 유틸리티](../../tools/bcp-utility.md)를 참조하세요.  
  
### <a name="using-bulk-insert"></a>BULK INSERT 사용  
 다음 예에서는 BULK INSERT를 사용하여 `myTestFormatFiles-c.Dat` 데이터 파일에서 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 예제 데이터베이스의 `HumanResources.myTestFormatFiles` 테이블로 데이터를 대량으로 가져옵니다. 이 예에서는 비 XML 서식 파일인 `MyTestFormatFiles.Fmt`를 사용합니다. 또한 데이터 파일을 가져오기 전에 기존 테이블 행을 모두 삭제합니다.  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DELETE myTestFormatFiles;  
GO  
BULK INSERT myTestFormatFiles   
   FROM 'C:\myTestFormatFiles-c.Dat'   
   WITH (FORMATFILE = 'C:\myTestFormatFiles.Fmt');  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
> [!NOTE]  
>  이 문에 대한 자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)를 참조하세요.  
  
### <a name="using-the-openrowset-bulk-rowset-provider"></a>OPENROWSET 대량 행 집합 공급자 사용  
 다음 예에서는 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 을 사용하여 `myTestFormatFiles-c.Dat` 데이터 파일에서 `HumanResources.myTestFormatFiles` 예제 데이터베이스의 `AdventureWorks` 테이블로 데이터를 대량으로 가져옵니다. 이 예에서는 XML 서식 파일인 `MyTestFormatFiles.Xml`을 사용합니다. 또한 데이터 파일을 가져오기 전에 기존 테이블 행을 모두 삭제합니다.  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks2012;  
DELETE myTestFormatFiles;  
GO  
INSERT INTO myTestFormatFiles  
    SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestFormatFiles-c.Dat',  
      FORMATFILE='C:\myTestFormatFiles.Xml'       
      ) as t1 ;  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
 예제 테이블의 사용을 완료하면 다음 문을 사용하여 해당 테이블을 삭제할 수 있습니다.  
  
```  
DROP TABLE myTestFormatFiles  
```  
  
> [!NOTE]  
>  OPENROWSET BULK 절에 대한 자세한 내용은 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)를 참조하세요.  
  
## <a name="additional-examples"></a>추가 예  
 [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
 [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
 [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [비 XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)   
 [XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)  
  
  
