---
title: 서식 파일을 사용하여 데이터 필드 건너뛰기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b7a68881bf5609e3a5ab3036b17f4a38faf875cd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37225243"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>서식 파일을 사용하여 데이터 필드 건너뛰기(SQL Server)
  데이터 파일에는 테이블의 열 수보다 많은 필드를 둘 수 있습니다. 이 항목에서는 테이블 열을 해당 데이터 필드에 매핑하고 나머지 필드는 무시하는 방법으로 데이터 파일에 더 많은 필드를 수용하도록 비 XML 서식 파일과 XML 서식 파일 모두를 수정하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  비 XML 서식 파일 또는 XML 서식 파일은 **bcp** 명령, BULK INSERT 문 또는 INSERT ...를 사용하여 데이터 파일을 테이블에 대량으로 가져오는데 사용될 수 있습니다. SELECT * FROM OPENROWSET(BULK...) 문을 사용하여 데이터 파일을 테이블로 대량으로 가져오는 데 사용할 수 있습니다. 자세한 내용은 [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)를 참조하세요.  
  
## <a name="sample-data-file-and-table"></a>예제 데이터 파일 및 테이블  
 이 항목의 수정된 서식 파일의 예는 다음 테이블 및 데이터 파일을 기준으로 합니다.  
  
### <a name="sample-table"></a>예제 테이블  
 이 예에서는 `myTestSkipField` 스키마의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스에 생성된 `dbo` 라는 테이블이 필요하며 이 테이블을 만들려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음 코드를 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipField   
   (  
   PersonID smallint,  
   FirstName nvarchar(50) ,  
   LastName nvarchar(50)   
   );  
GO  
```  
  
### <a name="sample-data-file"></a>예제 데이터 파일  
 `myTestSkipField-c.dat`데이터 파일에는 다음 레코드가 포함됩니다.  
  
```  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
```  
  
 `myTestSkipField-c.dat` 의 데이터를 `myTestSkipField` 테이블로 대량으로 가져오려면 서식 파일에서 다음과 같은 작업을 수행해야 합니다.  
  
-   첫 번째 데이터 필드를 첫 번째 열인 `PersonID`에 매핑합니다.  
  
-   두 번째 데이터 필드를 건너뜁니다.  
  
-   세 번째 데이터 필드를 두 번째 열인 `FirstName`에 매핑합니다.  
  
-   네 번째 데이터 필드를 세 번째 열인 `LastName`에 매핑합니다.  
  
## <a name="non-xml-format-file-for-more-data-fields"></a>더 많은 데이터 필드에 사용되는 비 XML 서식 파일  
 다음 `myTestSkipField.fmt` 서식 파일은 `myTestSkipField-c.dat`의 필드를 `myTestSkipField` 테이블의 열로 매핑합니다. 서식 파일은 문자 데이터 형식을 사용합니다. 이때 열 매핑을 건너뛰려면 해당 서식 파일의 `ExtraField` 열에서와 같이 열 순서 값을 0으로 변경해야 합니다.  
  
 `myTestSkipField.fmt` 서식 파일에는 다음 정보가 포함됩니다.  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     PersonID               ""  
2       SQLCHAR       0       100       ","    0     ExtraField             SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   3     LastName               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  비 XML 서식 파일 구문에 대한 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)을 참조하세요.  
  
### <a name="examples"></a>예  
 다음 예에서는 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 서식 파일을 사용하는 `myTestSkipField.fmt` 을 사용합니다. 또한 `myTestSkipField-c.dat` 데이터 파일을 `myTestSkipField` 테이블로 대량 가져옵니다. 예제 테이블 및 데이터 파일을 만들려면 이 항목의 앞부분에 나오는 "예제 데이터 파일 및 테이블"을 참조하십시오.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음 코드를 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
   SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.fmt'    
       ) AS t1;  
GO   
```  
  
## <a name="xml-format-file-for-more-data-fields"></a>더 많은 데이터 필드에 사용되는 XML 서식 파일  
 이 예에서 제공하는 서식 파일은 `myTestSkipField.xml`이라는 다른 서식 파일을 기반으로 합니다. 이 서식 파일은 문자 데이터 형식 전체를 사용하며 해당 필드는 `myTestSkipField` 테이블 열의 수와 순서에 정확히 일치합니다. 서식 파일의 내용을 보려면 [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)를 참조하세요.  
  
 다음 `myTestSkipField.xml` 서식 파일은 `myTestSkipField-c.dat`의 필드를 `myTestSkipField` 테이블의 열로 매핑합니다. 서식 파일은 문자 데이터 형식을 사용합니다.  
  
 `myTestSkipField.xml` 서식 파일에는 다음 정보가 포함됩니다.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
### <a name="examples"></a>예  
 다음 예에서는 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 서식 파일을 사용하는 `myTestSkipField.Xml` 을 사용합니다. 또한 `myTestSkipField-c.dat` 데이터 파일을 `myTestSkipField` 테이블로 대량 가져옵니다. 예제 테이블 및 데이터 파일을 만들려면 이 항목의 앞부분에 나오는 "예제 데이터 파일 및 테이블"을 참조하십시오.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음 코드를 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
  SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.xml'    
       ) AS t1;  
GO  
  
```  
  
> [!NOTE]  
>  XML 스키마의 구문 및 추가 XML 서식 파일 예제에 대한 내용은 [XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
