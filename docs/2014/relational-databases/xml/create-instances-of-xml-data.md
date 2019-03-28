---
title: XML 데이터 인스턴스 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- type casting string instances [XML in SQL Server]
- XML [SQL Server], typed
- xml data type [SQL Server], generating instances
- casting string instances [XML in SQL Server]
- typed XML
- generating XML instances [SQL Server]
- XML [SQL Server], generating instances
- white space [XML in SQL Server]
ms.assetid: dbd6c06f-db6e-44a7-855a-6a55bf374907
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae842748d2d510c5c00f329f5e28cd49a0c86ef3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538625"
---
# <a name="create-instances-of-xml-data"></a>XML 데이터 인스턴스 만들기
  이 항목에서는 XML 인스턴스를 생성하는 방법에 대해 설명합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 다음과 같은 방법으로 XML 인스턴스를 생성할 수 있습니다.  
  
-   문자열 인스턴스의 형식 캐스팅  
  
-   SELECT 문에 FOR XML 절 사용  
  
-   상수 할당 사용  
  
-   대량 로드 사용  
  
## <a name="type-casting-string-and-binary-instances"></a>문자열 및 이진 인스턴스의 형식 캐스팅  
 중 하나를 구문 분석할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 같은 데이터 형식을 문자열 [**n**] [**var**]**char**를 **[n] 텍스트**,  **varbinary**, 및 **이미지**에 `xml` 데이터 형식 캐스팅 (CAST) 또는 (변환) 문자열을 변환할는 `xml` 데이터 형식입니다. 형식화되지 않은 XML의 형식이 올바른지 확인하기 위해 검사합니다. 관련 된 스키마 없는 경우는 `xml` 형식, 유효성 검사도 수행 됩니다. 자세한 내용은 [형식화된 XML과 형식화되지 않은 XML 비교](compare-typed-xml-to-untyped-xml.md)를 참조하세요.  
  
 XML 문서는 UTF-8, UTF-16, windows-1252 등과 같은 다른 인코딩 방식으로 인코딩할 수 있습니다. 다음은 문자열 및 이진 원본 유형이 XML 문서 인코딩과 상호 작용하는 방법 및 파서의 동작 방식에 대한 규칙을 대략적으로 설명한 것입니다.  
  
 **nvarchar** 에서는 UTF-16 또는 UCS-2와 같은 2바이트 유니코드 인코딩을 가정하므로 XML 파서는 문자열 값을 2바이트 유니코드로 인코딩된 XML 문서 또는 조각으로 취급합니다. 즉, XML 문서는 원본 데이터 형식과 호환되어야 할 뿐 아니라 2바이트 유니코드 인코딩으로 인코딩해야 합니다. UTF-16으로 인코딩된 XML 문서는 UTF-16 BOM(바이트 순서 표시)을 포함할 수 있지만 원본 유형의 컨텍스트에 2바이트 유니코드로 인코딩된 문서만 될 수 있다고 명시되어 있으므로 이 BOM을 반드시 포함할 필요는 없습니다.  
  
 **varchar** 문자열의 내용은 XML 파서에 의해 1바이트로 인코딩된 XML 문서/조각으로 취급됩니다. **varchar** 원본 문자열에는 연관된 코드 페이지가 있으므로 파서는 XML 자체에 명시적 인코딩이 지정되지 않은 경우 인코딩에 대해 해당 코드 페이지를 사용하고, XML 인스턴스에 BOM 또는 인코딩 선언이 있는 경우 BOM 또는 선언이 코드 페이지와 일치해야 합니다. 그렇지 않은 경우 파서는 오류를 보고합니다.  
  
 **varbinary** 의 내용은 XML 파서로 직접 전달되는 코드 포인트 스트림으로 취급됩니다. 따라서 XML 문서 또는 조각은 BOM 또는 기타 인코딩 정보를 인라인으로 제공해야 합니다. 파서는 이 스트림을 통해서만 인코딩을 파악합니다. 즉, UTF-16으로 인코딩된 XML은 UTF-16 BOM을 제공해야 하고 BOM 및 선언 인코딩이 없는 인스턴스는 UTF-8로 해석됩니다.  
  
 XML 문서의 인코딩을 미리 알지 못하고 데이터를 XML로 캐스팅하기 전에 데이터가 XML 데이터 대신 문자열이나 이진 데이터로 전달된 경우 해당 데이터를 **varbinary**로 취급하는 것이 좋습니다. 예를 들어 OpenRowset()을 사용하여 XML 파일에서 데이터를 읽을 때 다음과 같이 해당 데이터가 **varbinary(max)** 값으로 읽히도록 지정해야 합니다.  
  
```  
select CAST(x as XML)   
from OpenRowset(BULK 'filename.xml', SINGLE_BLOB) R(x)  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 내부적으로 UTF-16 인코딩을 사용하는 효율적인 이진 표현으로 XML을 나타냅니다. 사용자가 제공한 인코딩은 유지되지 않지만 구문 분석 프로세스 중에 고려됩니다.  
  
### <a name="type-casting-clr-user-defined-types"></a>CLR 사용자 정의 형식 캐스팅  
 CLR 사용자 정의 형식에 XML 직렬화가 지정되면 명시적으로 해당 형식의 인스턴스를 XML 데이터 형식으로 캐스팅할 수 있습니다. CLR 사용자 정의 형식의 XML 직렬화에 대한 자세한 내용은 [CLR 데이터베이스 개체에서 XML 직렬화](../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md)를 참조하세요.  
  
### <a name="white-space-handling-in-typed-xml"></a>형식화된 XML에서 공백 처리  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 요소 내용 내에 있는 공백은 시작 또는 끝 태그처럼 마크업으로 구분된 공백 전용 문자 데이터 시퀀스 내에 있을 경우와 엔터티화되지 않은 경우 불필요한 것으로 간주됩니다. CDATA 섹션은 무시됩니다. 이러한 공백을 처리하는 방식은 W3C(World Wide Web Consortium)에서 게시한 XML 1.0 사양에 설명된 방법과 다릅니다. 그 이유는 XML 1.0에 설명된 대로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 XML 파서가 제한된 개수의 DTD 하위 집합만 인식하기 때문입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원하는 제한된 DTD 하위 집합에 대한 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)를 참조하세요.  
  
 기본적으로 XML 파서는 문자열 데이터를 XML로 변환할 때 다음 중 하나에 해당하면 불필요한 공백을 무시합니다.  
  
-   `The xml:space` 특성이 한 요소 또는 한 요소의 상위 항목 요소에 정의되어 있지 않습니다.  
  
-   한 요소 또는 한 요소의 상위 항목 요소 중 하나에 적용된 `xml:space` 특성에 기본값이 있습니다.  
  
 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
declare @x xml  
set @x = '<root>      <child/>     </root>'  
select @x   
```  
  
 다음은 결과입니다.  
  
```  
<root><child/></root>  
```  
  
 그러나 이 동작을 변경할 수 있습니다. xml DT 인스턴스에 대한 공백을 유지하려면 CONVERT 연산자 및 값 1로 설정된 해당 옵션 *style* 매개 변수를 사용합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
SELECT CONVERT(xml, N'<root>      <child/>     </root>', 1)  
```  
  
 *style* 매개 변수가 사용되지 않거나 해당 값이 0으로 설정된 경우 xml DT 인스턴스의 변환에 대해 불필요한 공백이 유지되지 않습니다. 문자열 데이터를 xml DT 인스턴스로 변환할 때 CONVERT 연산자 및 해당 *style* 매개 변수를 사용하는 방법은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)를 참조하세요.  
  
### <a name="example-cast-a-string-value-to-typed-xml-and-assign-it-to-a-column"></a>예: 문자열 값을 형식화된 xml로 캐스팅하여 열에 할당  
 다음 예에서는 XML 조각을 포함 하는 문자열 변수를 캐스팅 합니다 `xml` 데이터 형식으로 저장 된 `xml` 형식 열:  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
go  
DECLARE  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
```  
  
 다음 삽입 작업은 암시적으로 문자열로 변환 된 `xml` 형식:  
  
```  
INSERT INTO T VALUES (3, @s)   
```  
  
 캐스팅할 수 있습니다 명시적으로 문자열을 `xml` 형식:  
  
```  
INSERT INTO T VALUES (3, cast (@s as xml))  
```  
  
 또는 다음과 같이 convert()를 사용할 수 있습니다.  
  
```  
INSERT INTO T VALUES (3, convert (xml, @s))   
```  
  
### <a name="example-convert-a-string-to-typed-xml-and-assign-it-to-a-variable"></a>예: 문자열을 형식화된 xml로 변환하여 변수에 할당  
 문자열로 변환한 다음 예에서 `xml` 입력 하 고 변수에 할당 된 `xml` 데이터 형식:  
  
```  
declare @x xml  
declare  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
set @x =convert (xml, @s)  
select @x  
```  
  
## <a name="using-the-select-statement-with-a-for-xml-clause"></a>SELECT 문에 FOR XML 절 사용  
 SELECT 문에 FOR XML 절을 사용하여 결과를 XML로 반환할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = (SELECT Column1, Column2  
               FROM   Table1, Table2  
               WHERE   Some condition  
               FOR XML AUTO)  
 ...  
```  
  
 SELECT 문에서 할당 하는 동안 구문 분석 되는 텍스트 XML 조각을 반환 합니다 `xml` 데이터 형식 변수입니다.  
  
 사용할 수도 있습니다는 [TYPE 지시어](type-directive-in-for-xml-queries.md) 직접 FOR XML 쿼리 결과 반환 하는 FOR XML 절의 `xml` 형식:  
  
```  
Declare @xmlDoc xml  
SET @xmlDoc = (SELECT ProductModelID, Name  
               FROM   Production.ProductModel  
               WHERE  ProductModelID=19  
               FOR XML AUTO, TYPE)  
SELECT @xmlDoc  
```  
  
 다음은 결과입니다.  
  
```  
<Production.ProductModel ProductModelID="19" Name="Mountain-100" />...  
```  
  
 다음 예제에서는 형식화 된 `xml` FOR XML 쿼리의 결과에 삽입 되는 `xml` 형식 열:  
  
```  
CREATE TABLE T1 (c1 int, c2 xml)  
go  
INSERT T1(c1, c2)  
SELECT 1, (SELECT ProductModelID, Name  
           FROM Production.ProductModel  
           WHERE ProductModelID=19  
           FOR XML AUTO, TYPE)  
SELECT * FROM T1  
go  
```  
  
 FOR XML에 대한 자세한 내용은 [FOR XML&#40;SQL Server&#41;](for-xml-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 TYPE 지시어를 사용하는 FOR XML 쿼리와 같은 여러 서버 생성 결과로 클라이언트에 `xml` 데이터 형식 인스턴스를 반환합니다. 또는 `xml` 데이터 형식을 사용하여 SQL 열, 변수 및 출력 매개 변수로부터 XML을 반환합니다. 클라이언트 응용 프로그램 코드에서 ADO.NET 공급자는 이 `xml` 데이터 형식 정보가 서버로부터 이진 인코딩으로 전송되도록 요청합니다. 하지만 TYPE 지시어 없이 FOR XML을 사용하는 경우 XML 데이터는 문자열 형식으로 반환됩니다. 클라이언트 공급자는 항상 두 XML 유형 중 하나를 처리할 수 있습니다.  
  
## <a name="using-constant-assignments"></a>상수 할당 사용  
 여기서의 인스턴스는 문자열 상수를 사용할 수는 `xml` 데이터 형식이 필요 합니다. 이것은 문자열을 XML로 암시적 캐스팅하는 것과 같습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
-- Or  
SET @xmlDoc = N'<?xml version="1.0" encoding="ucs-2"?><doc/>'  
```  
  
 앞의 예제에는 암시적으로 문자열을 변환 합니다 `xml` 데이터 형식으로 할당 하는 `xml` 형식 변수.  
  
 다음 예제에서는 상수 문자열을 삽입 한 `xml` 형식 열:  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
INSERT INTO T VALUES (3, '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>')   
```  
  
> [!NOTE]  
>  형식화된 XML의 경우 지정된 스키마에 대해 XML의 유효성이 검사됩니다. 자세한 내용은 [형식화된 XML과 형식화되지 않은 XML 비교](compare-typed-xml-to-untyped-xml.md)를 참조하세요.  
  
## <a name="using-bulk-load"></a>대량 로드 사용  
 향상된 [OPENROWSET(Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql) 기능을 사용하면 데이터베이스의 XML 문서를 대량 로드할 수 있습니다. 파일에서 로드 XML 인스턴스를 대량 수는 `xml` 데이터베이스의 열을 입력 합니다. 작업 샘플은 [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](../import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)를 참조하세요. XML 문서 로드에 대한 자세한 내용은 [XML 데이터 로드](load-xml-data.md)를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[XML 데이터 검색 및 쿼리](retrieve-and-query-xml-data.md)|XML 인스턴스가 데이터베이스에 저장될 때 보존되지 않는 인스턴스의 일부분에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [형식화된 XML과 형식화되지 않은 XML 비교](compare-typed-xml-to-untyped-xml.md)   
 [xml 데이터 형식 메서드](/sql/t-sql/xml/xml-data-type-methods)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](/sql/t-sql/xml/xml-data-modification-language-xml-dml)   
 [XML 데이터&#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
