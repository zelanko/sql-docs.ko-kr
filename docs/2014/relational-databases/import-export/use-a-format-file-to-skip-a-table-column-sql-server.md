---
title: 서식 파일을 사용하여 테이블 열 건너뛰기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- skipping columns when importing
- format files [SQL Server], skipping columns
ms.assetid: 30e0e7b9-d131-46c7-90a4-6ccf77e3d4f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 80c5c5b2f4e6d4f691b7c3977ae2f715f5424e7f
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011685"
---
# <a name="use-a-format-file-to-skip-a-table-column-sql-server"></a>서식 파일을 사용하여 테이블 열 건너뛰기(SQL Server)
  이 항목에서는 서식 파일에 대해 설명합니다. 필드가 데이터 파일에 없는 경우 서식 파일을 사용하여 테이블 열 가져오기를 건너뛸 수 있습니다. 건너뛴 열이 Null을 허용하거나 기본값을 가질 경우에만 데이터 파일에 테이블의 열 수보다 적은 수의 필드가 있을 수 있습니다.  
  
## <a name="sample-table-and-data-file"></a>예제 테이블 및 데이터 파일  
 다음 예에서는 `myTestSkipCol` dbo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 스키마의 **예제 데이터베이스에** 이라는 테이블이 필요합니다. 이 테이블을 다음과 같이 만듭니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipCol   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) NULL,  
   Col3 nvarchar(50) not NULL  
   );  
GO  
```  
  
 다음 예에서는 해당 테이블에 3개의 열이 있지만 두 개의 필드만 있는 `myTestSkipCol2.dat`라는 예제 데이터 파일을 사용합니다.  
  
```  
1,DataForColumn3  
1,DataForColumn3  
1,DataForColumn3  
  
```  
  
 `myTestSkipCol2.dat` 의 데이터를 `myTestSkipCol` 테이블로 대량 가져오려면 서식 파일이 첫 번째 데이터 필드를 `Col1`에 매핑하고 `Col3`는 건너뛴 채 두 번째 필드를 `Col2`에 매핑해야 합니다.  
  
## <a name="using-a-non-xml-format-file"></a>비 XML 서식 파일 사용  
 비 XML 서식 파일을 수정하여 테이블 열을 건너뛸 수 있습니다. 이렇게 하려면 일반적으로 **bcp** 유틸리티를 사용하여 기본 비 XML 서식 파일을 만들고 텍스트 편집기에서 기본 파일을 수정해야 합니다. 수정된 서식 파일은 기존의 각 필드를 해당하는 테이블 열로 매핑하고 건너뛸 테이블 열을 나타내야 합니다. 기본 비 XML 데이터 파일을 수정할 수 있는 두 가지 다른 방법이 있습니다. 각 방법은 데이터 필드가 데이터 파일에 없고 데이터가 해당 테이블 열에 삽입되지 않음을 나타냅니다.  
  
### <a name="creating-a-default-non-xml-format-file"></a>기본 비 XML 서식 파일 만들기  
 이 항목에서는 다음 `myTestSkipCol` bcp **명령을 사용하여** 예제 테이블에 대해 생성된 기본 비 XML 서식 파일을 사용합니다.  
  
```  
bcp AdventureWorks2012..myTestSkipCol format nul -f myTestSkipCol_Default.fmt -c -T  
```  
  
 위 명령은 `myTestSkipCol_Default.fmt`라는 비 XML 서식 파일을 만듭니다. 이 서식 파일은 *bcp* 에서 생성되는 형식이므로 **기본 서식 파일**이라고 합니다. 일반적으로 기본 서식 파일은 데이터 파일 필드와 테이블 열 간의 일 대 일 대응을 나타내는 파일입니다.  
  
> [!IMPORTANT]  
>  연결할 서버 인스턴스의 이름을 지정해야 할 수 있으며 사용자 이름과 암호를 지정해야 할 수도 있습니다. 자세한 내용은 [bcp Utility](../../tools/bcp-utility.md)을(를) 참조하세요.  
  
 다음 그림에서는 이 예제 기본 서식 파일의 값을 보여 주며 각 서식 파일 필드의 이름도 보여 줍니다.  
  
 ![myTestSkipCol의 기본 비 XML 형식 파일](../../database-engine/media/mytestskipcol-f-c-default-fmt.gif "default non-XML format file for myTestSkipCol")  
  
> [!NOTE]  
>  서식 파일 필드에 대한 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)을 참조하세요.  
  
### <a name="methods-for-modifying-a-non-xml-format-file"></a>비 XML 서식 파일 수정 방법  
 테이블 열을 건너뛰려면 기본 비 XML 서식 파일을 편집하고 다음 방법 중 하나를 사용하여 해당 파일을 수정합니다.  
  
-   일반적인 방법에는 3가지 기본 단계가 있습니다. 먼저 데이터 파일에서 누락된 필드를 나타내는 모든 서식 파일 행을 삭제합니다. 그런 다음 삭제된 행 뒤에 오는 각 서식 파일 행의 "호스트 파일 필드 순서" 값을 줄입니다. 목표는 데이터 파일에서 각 데이터 필드의 실제 위치를 반영하는 1부터 *n*까지의 순차적인 "호스트 파일 필드 순서" 값을 얻는 것입니다. 마지막으로 데이터 파일의 실제 필드 수를 반영하도록 "열 수" 필드의 값을 줄입니다.  
  
     다음 예는 이 항목의 앞부분에 나오는 "기본 비 XML 서식 파일 만들기"에서 생성된 `myTestSkipCol` 테이블에 대한 기본 서식 파일을 기반으로 합니다. 수정된 이 서식 파일은 첫 번째 데이터 필드를 `Col1`에 매핑하고 `Col2`를 건너뛴 다음 두 번째 데이터 필드를 `Col3`에 매핑합니다. `Col2` 의 행은 삭제되었습니다. 기타 수정 내용은 굵게 표시되어 있습니다.  
  
    ```  
    9.0  
    2  
    1       SQLCHAR       0       7       "\t"     1     Col1         ""  
    2       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
    ```  
  
-   테이블 열을 건너뛰기 위해 테이블 열에 해당하는 서식 파일 행의 정의를 수정할 수도 있습니다. 이 서식 파일 행에서 "접두사 길이", "호스트 파일 데이터 길이" 및 "서버 열 순서" 값은 0으로 설정해야 하며 "종결자" 및 "열 데이터 정렬" 필드는 ""(NULL)로 설정해야 합니다.  
  
     "실제 열 이름이 필요하지 않더라도 "서버 열 이름" 값에는 공백이 아닌 문자열이 필요합니다. 나머지 서식 필드에는 해당 기본값이 필요합니다.  
  
     다음 예도 `myTestSkipCol` 테이블에 대한 기본 서식 파일에서 파생된 것입니다. 0 또는 NULL이어야 하는 값은 굵게 표시되어 있습니다.  
  
    ```  
    9.0  
    3  
    1       SQLCHAR       0       7       "\t"     1     Col1         ""  
    2       SQLCHAR       00""0     Col2         ""  
    3       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
    ```  
  
### <a name="examples"></a>예  
 다음 예도 이 항목의 앞부분에 나오는 "예제 테이블 및 데이터 파일"에서 생성된 `myTestSkipCol` 예제 테이블과 `myTestSkipCol2.dat` 예제 데이터 파일을 기반으로 합니다.  
  
#### <a name="using-bulk-insert"></a>BULK INSERT 사용  
 이 예는 이 항목의 앞부분에 나오는 "비 XML 서식 파일 수정 방법"에서 생성된 수정 비 XML 서식 파일 중 하나를 사용하여 작동합니다. 이 예에서 수정된 서식 파일의 이름은 `C:\myTestSkipCol2.fmt`입니다. `BULK INSERT` 를 사용하여 `myTestSkipCol2.dat` 데이터 파일을 대량으로 가져오려면 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음 코드를 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestSkipCol   
   FROM 'C:\myTestSkipCol2.dat'   
   WITH (FORMATFILE = 'C:\myTestSkipCol2.fmt');  
GO  
SELECT * FROM myTestSkipCol;  
GO  
```  
  
## <a name="using-an-xml-format-file"></a>XML 서식 파일 사용  
 XML 서식 파일을 사용하면 **bcp** 명령이나 BULK INSERT 문을 사용하여 테이블로 데이터를 직접 가져올 때 열을 건너뛸 수 없습니다. 그러나 테이블의 마지막 열을 제외하고 모든 열로 가져올 수 있습니다. 마지막 열을 제외하고 모든 열을 건너뛰어야 하는 경우 데이터 파일에 있는 열만 포함된 대상 테이블의 뷰를 만들어야 합니다. 그런 다음 해당 파일의 데이터를 뷰로 대량 가져오기를 수행할 수 있습니다.  
  
 XML 서식 파일을 통해 OPENROWSET(BULK...)을 사용하여 테이블 열을 건너뛰려면 SELECT 목록과 대상 테이블에 있는 명시적인 열 목록을 다음과 같이 제공해야 합니다.  
  
 INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...)  
  
### <a name="creating-a-default-xml-format-file"></a>기본 XML 서식 파일 만들기  
 수정된 서식 파일의 예는 이 항목의 앞부분에 나오는 "예제 테이블 및 데이터 파일"에서 생성된 `myTestSkipCol` 예제 테이블과 데이터 파일을 기반으로 합니다. 다음 **bcp** 명령은 `myTestSkipCol` 테이블에 대한 기본 XML 서식 파일을 만듭니다.  
  
```  
bcp AdventureWorks2012..myTestSkipCol format nul -f myTestSkipCol_Default.xml -c -x -T  
```  
  
 결과로 생성된 기본 비 XML 서식 파일은 다음과 같이 데이터 파일 필드와 테이블 열 간의 일 대 일 대응을 나타냅니다.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  XML 서식 파일의 구조에 대한 자세한 내용은 [XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)을 참조하세요.  
  
### <a name="examples"></a>예  
 이 섹션의 예에서는 이 섹션의 예에서는 이 항목의 앞부분에 나오는 "예제 테이블 및 데이터 파일"에서 생성된 `myTestSkipCol` 예제 테이블과 `myTestSkipCol2.dat` 예제 데이터 파일을 사용합니다. `myTestSkipCol2.dat` 의 데이터를 `myTestSkipCol` 테이블로 가져오기 위해 이 예에서는 수정된 XML 서식 파일인 `myTestSkipCol2-x.xml`을 사용합니다. 이 예는 이 항목의 앞부분에 나오는 "기본 XML 서식 파일 만들기"에서 생성된 서식 파일을 기반으로 합니다.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
#### <a name="using-openrowsetbulk"></a>OPENROWSET(BULK...) 사용  
 다음 예에서는 `OPENROWSET` 대량 행 집합 공급자와 `myTestSkipCol2.xml` 서식 파일을 사용합니다. 또한 `myTestSkipCol2.dat` 데이터 파일을 `myTestSkipCol` 테이블로 대량 가져옵니다. 이 문에는 필요에 따라 SELECT 목록과 대상 테이블의 명시적인 열 목록이 있습니다.  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음 코드를 실행합니다.  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipCol  
  (Col1,Col3)  
    SELECT Col1,Col3  
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',  
      FORMATFILE='C:\myTestSkipCol2.Xml'    
       ) as t1 ;  
GO  
```  
  
#### <a name="using-bulk-import-on-a-view"></a>뷰에서 BULK IMPORT 사용  
 다음 예에서는 `v_myTestSkipCol` 테이블에 `myTestSkipCol` 을 만듭니다. 이 뷰는 두 번째 테이블 열인 `Col2`를 건너뜁니다. 그런 다음 이 예에서는 `BULK INSERT` 를 사용하여 `myTestSkipCol2.dat` 데이터 파일을 이 뷰로 가져옵니다.  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음 코드를 실행합니다.  
  
```  
CREATE VIEW v_myTestSkipCol AS  
    SELECT Col1,Col3  
    FROM myTestSkipCol;  
GO  
  
USE AdventureWorks2012;  
GO  
BULK INSERT v_myTestSkipCol  
FROM 'C:\myTestSkipCol2.dat'  
WITH (FORMATFILE='C:\myTestSkipCol2.xml');  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
  
