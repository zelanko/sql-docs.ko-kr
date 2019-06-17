---
title: XML 문서 대량 가져오기 및 내보내기 예제(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- field terminators [SQL Server]
- bulk importing [SQL Server], data formats
- row terminators [SQL Server]
- OPENROWSET function, XML bulk load
- terminators [SQL Server]
- bulk exporting [SQL Server], data formats
- XML bulk load [SQL Server]
ms.assetid: dff99404-a002-48ee-910e-f37f013d946d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d60518f64bd44b9b2498c9d27711d47753b04cf9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011967"
---
# <a name="examples-of-bulk-import-and-export-of-xml-documents-sql-server"></a>XML 문서 대량 가져오기 및 내보내기 예(SQL Server)
    
##  <a name="top"></a> XML 문서 대량 수를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스 또는 대량 내보내기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 이 항목에서는 이 두 가지 경우에 대한 예를 제공합니다.  
  
 다음을 사용하여 데이터 파일의 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 또는 분할되지 않은 뷰로 대량 가져올 수 있습니다.  
  
-   **bcp** 유틸리티  
  
     **bcp** 유틸리티를 사용하면 분할된 뷰를 포함하여 SELECT 문이 작동하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 모든 위치에서 데이터를 내보낼 수도 있습니다.  
  
-   BULK INSERT  
  
-   INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
 자세한 내용은 [bcp 유틸리티를 사용 하 여 대량 데이터 내보내기 및 가져오기 &#40;SQL Server&#41; ](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md) 하 고 [BULK INSERT 또는 OPENROWSET 대량 데이터 가져오기&#40;대량... &#41; &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)합니다.  
  
## <a name="examples"></a>예  
 다음과 같은 예가 제공됩니다.  
  
-   1\. [XML 데이터를 이진 바이트 스트림으로 대량 가져오기](#binary_byte_stream)  
  
-   2\. [기존 행에 XML 데이터 대량 가져오기](#existing_row)  
  
-   3\. [XML 데이터 대량 가져오기 dtd가 포함 된 파일](#file_contains_dtd)  
  
-   4\. [서식 파일을 사용 하 여 명시적으로 필드 종결자 지정](#field_terminator_in_format_file)  
  
-   5\. [XML 데이터 대량 내보내기](#bulk_export_xml_data)  
  
###  <a name="binary_byte_stream"></a> 1. XML 데이터를 이진 바이트 스트림으로 대량 가져오기  
 적용할 인코딩 선언이 있는 파일에서 XML 데이터를 대량으로 가져오는 경우 OPENROWSET(BULK…) 절에 SINGLE_BLOB 옵션을 지정합니다. SINGLE_BLOB 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 XML 파서가 XML 선언에 지정된 인코딩 체계에 따라 데이터를 가져오도록 합니다.  
  
#### <a name="sample-table"></a>예제 테이블  
 예 1을 테스트하려면 `T`예제 테이블을 만들어야 합니다.  
  
```  
USE tempdb  
CREATE TABLE T (IntCol int, XmlCol xml);  
GO  
```  
  
#### <a name="sample-data-file"></a>예제 데이터 파일  
 예제 A를 실행하려면 먼저`C:\SampleFolder\SampleData3.txt`인코딩 체계를 지정하는 다음 예제 인스턴스가 포함된 UTF-8 인코딩 파일( `UTF-8` )을 만들어야 합니다.  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
<Root>  
          <ProductDescription ProductModelID="5">  
             <Summary>Some Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-a"></a>예 1  
 이 예에서는 `SINGLE_BLOB` 문에 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 옵션을 사용하여 `SampleData3.txt` 라는 파일에서 데이터를 가져오고 단일 열 테이블( `T`예제 테이블)에 XML 인스턴스를 삽입합니다.  
  
```  
INSERT INTO T(XmlCol)  
SELECT * FROM OPENROWSET(  
   BULK 'c:\SampleFolder\SampleData3.txt',  
   SINGLE_BLOB) AS x;  
```  
  
#### <a name="remarks"></a>Remarks  
 이 경우 SINGLE_BLOB을 사용하면 XML 인코딩 선언에 지정된 XML 문서의 인코딩과 서버가 적용한 문자열 코드 페이지 간 불일치를 피할 수 있습니다.  
  
 NCLOB 또는 CLOB 데이터 형식을 사용할 경우 코드 페이지 또는 인코딩 충돌이 발생하면 다음 중 하나를 수행해야 합니다.  
  
-   XML 데이터 파일의 내용을 성공적으로 가져오기 위해 XML 선언을 제거합니다.  
  
-   XML 선언에 사용된 인코딩 체계와 일치하는 쿼리의 CODEPAGE 옵션에 코드 페이지를 지정합니다.  
  
-   데이터베이스 데이터 정렬 설정을 비유니코드 XML 인코딩 체계에 맞추거나 불일치를 해결합니다.  
  
 [&#91;맨 위로 이동&#93;](#top)  
  
###  <a name="existing_row"></a> 2. 기존 행에 XML 데이터 대량 가져오기  
 이 예에서는 `OPENROWSET` 대량 행 집합 공급자를 사용하여 `T`예제 테이블의 기존 행에 XML 인스턴스를 추가합니다.  
  
> [!NOTE]  
>  이 예를 실행하려면 예 1에서 제공한 테스트 스크립트를 먼저 완료해야 합니다. 해당 예는 `tempdb.dbo.T` 테이블을 만들고 `SampleData3.txt`에서 데이터를 대량으로 가져옵니다.  
  
#### <a name="sample-data-file"></a>예제 데이터 파일  
 예 2에서는 앞의 예에서 사용된 `SampleData3.txt` 예제 데이터 파일의 수정된 버전을 사용합니다. 이 예를 실행하려면 다음과 같이 이 파일의 내용을 수정합니다.  
  
```  
<Root>  
          <ProductDescription ProductModelID="10">  
             <Summary>Some New Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-b"></a>예 2  
  
```  
-- Query before update shows initial state of XmlCol values.  
SELECT * FROM T  
UPDATE T  
SET XmlCol =(  
SELECT * FROM OPENROWSET(  
   BULK 'C:\SampleFolder\SampleData3.txt',  
           SINGLE_BLOB  
) AS x  
)  
WHERE IntCol = 1;  
GO  
```  
  
 [&#91;맨 위로 이동&#93;](#top)  
  
###  <a name="file_contains_dtd"></a> 3. DTD가 포함된 파일에 있는 XML 데이터 대량 가져오기  
  
> [!IMPORTANT]  
>  XML 환경에서 반드시 필요한 경우가 아니면 DTD(문서 유형 정의)에 대한 지원을 설정하지 않는 것이 좋습니다. DTD 지원을 설정하면 서버가 공격 받을 수 있는 노출 영역이 증가하며 서비스 거부 공격에 노출될 수 있습니다. DTD 지원을 설정해야 할 경우에는 신뢰할 수 있는 XML 문서만 처리하여 이러한 보안 위험을 줄일 수 있습니다.  
  
 [bcp](../../tools/bcp-utility.md) 명령을 사용하여 DTD가 들어 있는 파일에서 XML 데이터를 가져오려고 하면 다음과 유사한 오류가 발생할 수 있습니다.  
  
 "SQLState = 42000, NativeError = 6359"  
  
 "오류 = [Microsoft][SQL Server Native Client][ SQL Server]내부 하위 집합 DTD를 사용하여 XML 구문 분석을 수행할 수 없습니다. CONVERT에 스타일 옵션 2를 사용하여 제한된 내부 하위 집합 DTD 지원을 활성화하십시오."  
  
 "BCP 복사 %s이(가) 실패했습니다."  
  
 이 문제를 해결하려면 `OPENROWSET(BULK...)` 함수를 사용한 다음, 명령의 `CONVERT` 절에 `SELECT` 옵션을 지정하여 DTD가 포함된 데이터 파일에서 XML 데이터를 가져올 수 있습니다. 명령의 기본 구문은 다음과 같습니다.  
  
 `INSERT ... SELECT CONVERT(...) FROM OPENROWSET(BULK...)`  
  
#### <a name="sample-data-file"></a>예제 데이터 파일  
 이 대량 가져오기 예를 테스트하려면 먼저 다음 예제 인스턴스를 포함하는 파일(`C:\temp\Dtdfile.xml`)을 만들어야 합니다.  
  
```  
<!DOCTYPE DOC [<!ATTLIST elem1 attr1 CDATA "defVal1">]><elem1>January</elem1>  
```  
  
#### <a name="sample-table"></a>예제 테이블  
 예 3에서는 다음 `T1` 문에 의해 생성된 `CREATE TABLE` 예제 테이블을 사용합니다.  
  
```  
USE tempdb;  
CREATE TABLE T1(XmlCol xml);  
GO  
```  
  
#### <a name="example-c"></a>예 3  
 이 예에서는 `OPENROWSET(BULK...)` 을 사용하고 `CONVERT` 절에 `SELECT` 옵션을 지정하여 `Dtdfile.xml` 의 XML 데이터를 `T1`예제 테이블로 가져옵니다.  
  
```  
INSERT T1  
  SELECT CONVERT(xml, BulkColumn, 2) FROM   
    OPENROWSET(Bulk 'c:\temp\Dtdfile.xml', SINGLE_BLOB) [rowsetresults];  
```  
  
 `INSERT` 문을 실행하면 XML에서 DTD가 잘리고 `T1` 테이블에 저장됩니다.  
  
 [&#91;맨 위로 이동&#93;](#top)  
  
###  <a name="field_terminator_in_format_file"></a> 4. 서식 파일을 사용하여 명시적으로 필드 종결자 지정  
 다음 예에서는 XML 문서 `Xmltable.dat`를 대량으로 가져오는 방법을 보여 줍니다.  
  
#### <a name="sample-data-file"></a>예제 데이터 파일  
 `Xmltable.dat` 의 문서에는 두 개의 XML 값이 있으며 각 행마다 하나의 XML 값을 갖습니다. 첫 번째 XML 값은 UTF-16으로 인코딩되고 두 번째 값은 UTF-8로 인코딩됩니다.  
  
 이 데이터 파일의 내용은 다음과 같은 16진수 덤프로 표시됩니다.  
  
```  
FF FE 3C 00 3F 00 78 00-6D 00 6C 00 20 00 76 00  *..<.?.x.m.l. .v.*  
65 00 72 00 73 00 69 00-6F 00 6E 00 3D 00 22 00  *e.r.s.i.o.n.=.".*  
31 00 2E 00 30 00 22 00-20 00 65 00 6E 00 63 00  *1...0.". .e.n.c.*  
6F 00 64 00 69 00 6E 00-67 00 3D 00 22 00 75 00  *o.d.i.n.g.=.".u.*  
74 00 66 00 2D 00 31 00-36 00 22 00 3F 00 3E 00  *t.f.-.1.6.".?.>.*  
3C 00 72 00 6F 00 6F 00-74 00 3E 00 A2 4F 9C 76  *<.r.o.o.t.>..O.v*  
0C FA 77 E4 80 00 89 00-00 06 90 06 91 2E 9B 2E  *..w.............*  
99 34 A2 34 86 00 83 02-92 20 7F 02 4E C5 E4 A3  *.4.4..... ..N...*  
34 B2 B7 B3 B7 FE F8 FF-F8 00 3C 00 2F 00 72 00  *4.........<./.r.*  
6F 00 6F 00 74 00 3E 00-00 00 00 00 7A EF BB BF  *o.o.t.>.....z...*  
3C 3F 78 6D 6C 20 76 65-72 73 69 6F 6E 3D 22 31  *<?xml version="1*  
2E 30 22 20 65 6E 63 6F-64 69 6E 67 3D 22 75 74  *.0" encoding="ut*  
66 2D 38 22 3F 3E 3C 72-6F 6F 74 3E E4 BE A2 E7  *f-8"?><root>....*  
9A 9C EF A8 8C EE 91 B7-C2 80 C2 89 D8 80 DA 90  *................*  
E2 BA 91 E2 BA 9B E3 92-99 E3 92 A2 C2 86 CA 83  *................*  
E2 82 92 C9 BF EC 95 8E-EA 8F A4 EB 88 B4 EB 8E  *................*  
B7 EF BA B7 EF BF B8 C3-B8 3C 2F 72 6F 6F 74 3E  *.........</root>*  
00 00 00 00 7A                                   *....z*  
```  
  
#### <a name="sample-table"></a>예제 테이블  
 XML 문서를 대량으로 가져오거나 내보낼 때는 문서에 나타날 가능성이 없는 [필드 종결자](specify-field-and-row-terminators-sql-server.md) 를 사용해야 합니다. 예를 들어 다음과 같이`\0`: `z`문자 앞에 오는 일련의 Null( `\0\0\0\0z`) 4개를 사용할 수 있습니다.  
  
 이 예에서는 `xTable` 예제 테이블에 대해 이 필드 종결자를 사용하는 방법을 보여 줍니다. 이 예제 테이블을 만들려면 다음 `CREATE TABLE` 문을 사용합니다.  
  
```  
USE tempdb;  
CREATE TABLE xTable (xCol xml);  
GO  
```  
  
#### <a name="sample-format-file"></a>예제 서식 파일  
 필드 종결자는 서식 파일에 지정해야 합니다. 예 4에서는 다음을 포함하는 `Xmltable.fmt` 라는 비 XML 서식 파일을 사용합니다.  
  
```  
9.0  
1  
1       SQLBINARY     0       0       "\0\0\0\0z"    1     xCol         ""  
```  
  
 이 서식 파일을 사용하면 `xTable` 명령이나 `bcp` 또는 `BULK INSERT` 문을 사용하여 XML 문서를 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 테이블로 대량 가져올 수 있습니다.  
  
#### <a name="example-d"></a>예 4  
 이 예에서는 `Xmltable.fmt` 문에 `BULK INSERT` 서식 파일을 사용하여 `Xmltable.dat`라는 XML 데이터 파일의 내용을 가져옵니다.  
  
```  
BULK INSERT xTable   
FROM 'C:\Xmltable.dat'  
WITH (FORMATFILE = 'C:\Xmltable.fmt');  
GO  
```  
  
 [&#91;맨 위로 이동&#93;](#top)  
  
###  <a name="bulk_export_xml_data"></a> 5. XML 데이터 대량 내보내기  
 다음 예에서는 `bcp` 를 사용하여 동일한 XML 서식 파일로 앞의 예에서 만든 테이블에서 XML 데이터를 대량으로 내보냅니다. 다음 `bcp` 명령에서 `<server_name>` 및 `<instance_name>` 은 적절한 값으로 바꿔야 하는 자리 표시자를 나타냅니다.  
  
```  
bcp bulktest..xTable out a-wn.out -N -T -S<server_name>\<instance_name>  
```  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 XML 데이터가 데이터베이스에 유지되면 XML 인코딩을 저장하지 않습니다. 그러므로 XML 필드의 원래 인코딩은 XML 데이터를 내보내면 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 XML 데이터를 내보낼 때 UTF-16 인코딩을 사용합니다.  
  
 [&#91;맨 위로 이동&#93;](#top)  
  
## <a name="see-also"></a>관련 항목  
 [INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [SELECT 절&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-clause-transact-sql)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
