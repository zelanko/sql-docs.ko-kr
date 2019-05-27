---
title: 서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- mapping columns to fields during import [SQL Server]
- format files [SQL Server], mapping columns to fields
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fd08aaa50f307d107a55c838395677e5692914ba
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011737"
---
# <a name="use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server"></a>서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑(SQL Server)
  데이터 파일은 테이블의 해당 열에서 서로 다른 순서로 정렬된 필드를 포함할 수 있습니다. 이 항목에서는 테이블 열과 서로 다른 순서로 필드가 정렬된 데이터 파일에 맞게 수정된 비 XML 및 XML 서식 파일에 대해 설명합니다. 수정된 서식 파일은 데이터 필드를 해당 테이블 열로 매핑합니다.  
  
> [!NOTE]  
>  비 XML 서식 파일 또는 XML 서식 파일은 **bcp** 명령, BULK INSERT 문 또는 INSERT ... SELECT * FROM OPENROWSET(BULK...) 문을 사용하여 데이터 파일을 테이블로 대량으로 가져오는 데 사용할 수 있습니다. 자세한 내용은 [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)를 참조하세요.  
  
## <a name="sample-table-and-data-file"></a>예제 테이블 및 데이터 파일  
 이 항목의 수정된 서식 파일의 예는 다음 테이블 및 데이터 파일을 기준으로 합니다.  
  
### <a name="sample-table"></a>예제 테이블  
 이 항목의 예에서는 `myTestOrder` 스키마의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스에 생성된 `dbo` 라는 테이블이 필요하며 이 테이블을 만들려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음 코드를 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestOrder   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) ,  
   Col3 nvarchar(50) ,   
   Col4 nvarchar(50)   
   );  
GO  
  
```  
  
### <a name="data-file"></a>데이터 파일  
 `myTestOrder-c.txt`데이터 파일에는 다음 레코드가 포함됩니다.  
  
```  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
  
```  
  
 `myTestSkipCol2-c.dat`에서 `myTestSkipCol` 테이블로 데이터를 대량으로 가져오려면 서식 파일은 첫 번째 데이터 필드를 `Col3`으로, 두 번째 데이터 필드를 `Col2`로, 세 번째 데이터 필드를 `Col1`로, 네 번째 데이터 필드를 `Col4`로 매핑해야 합니다.  
  
## <a name="using-a-non-xml-format-file"></a>비 XML 서식 파일 사용  
 해당 데이터 필드의 위치를 나타내는 열의 순서 값을 변경하면 열 매핑 순서를 변경할 수 있습니다.  
  
 다음 비 XML 서식 파일 예제에서는 `myTestOrder.fmt`의 필드를 `myTestOrder-c.txt` 테이블의 열에 매핑하는 `myTestOrder` 서식 파일을 보여 줍니다. 데이터 파일 및 테이블을 만드는 방법은 이 항목의 앞부분에 나오는 "예제 테이블 및 데이터 파일"을 참조하십시오. 서식 파일은 문자 데이터 형식을 사용합니다.  
  
 서식 파일에는 다음 정보가 포함됩니다.  
  
```  
9.0  
4  
1       SQLCHAR       0       100     ","     3     Col3               SQL_Latin1_General_CP1_CI_AS  
2       SQLCHAR       0       100     ","     2     Col2               SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       7       ","     1     Col1               ""  
4       SQLCHAR       0       100     "\r\n"  4     Col4               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  비 XML 서식 파일의 레이아웃에 대한 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)을 참조하세요.  
  
### <a name="example"></a>예제  
 다음 예에서는 `BULK INSERT` 문에서 비 XML 서식 파일인 `myTestOrder-c.txt`를 사용하여 `myTestOrder` 데이터 파일에서 `myTestOrder.fmt` 예제 테이블로 데이터를 대량으로 가져옵니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestOrder  
FROM 'C:\myTestOrder-c.txt'   
WITH (formatfile='C:\myTestOrder.fmt');  
GO  
  
```  
  
## <a name="using-an-xml-format-file"></a>XML 서식 파일 사용  
 다음 비 XML 서식 파일 예제에서는 `myTestOrder.xml`의 필드를 `myTestOrder-c.txt` 테이블의 열에 매핑하는 서식 파일인 `myTestOrder`을 보여 줍니다. 데이터 파일 및 테이블을 만드는 방법은 이 항목의 앞부분에 나오는 "예제 테이블 및 데이터 파일"을 참조하십시오.  
  
 `myTestOrder.xml` 서식 파일에는 다음 정보가 포함됩니다.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="3" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="1" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
  
```  
  
> [!NOTE]  
>  XML 스키마의 구문 및 추가 XML 서식 파일 예제에 대한 내용은 [XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)를 참조하세요.  
  
### <a name="example"></a>예제  
 다음 예에서는 `OPENROWSET` 대량 행 집합 공급자에서 XML 서식 파일인 `myTestOrder-c.txt` 을 사용하여 `myTestOrder` 데이터 파일에서 `myTestOrder.xml` 예제 테이블로 데이터를 대량으로 가져옵니다. `INSERT... SELECT` 문은 SELECT 목록에서 열 목록을 지정합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음 코드를 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestOrder   
  SELECT Col1, Col2, Col3, Col4  
      FROM  OPENROWSET(BULK  'C:\myTestOrder-c.txt',  
      FORMATFILE='C:\myTestOrder.Xml'    
       ) AS t1;  
GO  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  
