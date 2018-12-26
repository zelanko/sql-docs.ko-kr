---
title: 계산 열을 사용하여 자주 사용되는 XML 값 승격 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- promoting properties [XML in SQL Server]
- property promotion [XML in SQL Server]
ms.assetid: f5111896-c2fd-4209-b500-f2baa45489ad
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d9be4170345ea7aab0d7d1a7dc848291e776e27d
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51665572"
---
# <a name="promote-frequently-used-xml-values-with-computed-columns"></a>계산 열을 사용하여 자주 사용되는 XML 값 승격
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  쿼리가 주로 적은 수의 요소 및 특성 값으로 작성된 경우 이러한 수량을 관계형 열로 승격시킬 수 있습니다. 이 방식은 전체 XML 인스턴스를 검색하는 동안 XML 데이터의 일부에 대해서 쿼리가 실행된 경우에 유용합니다. XML 열에 XML 인덱스를 만들 필요는 없습니다. 대신 승격된 열을 인덱싱할 수 있습니다. 승격된 열을 사용하도록 쿼리를 작성해야 합니다. 즉, 쿼리 최적화 프로그램은 XML 열에 있는 쿼리를 승격된 열로 다시 대상화하지 않습니다.  
  
 승격된 열은 같은 테이블에 있는 계산 열이거나 테이블에서 사용자가 유지 관리하는 별개의 열일 수 있습니다. 각 XML 인스턴스로부터 단일 항목 값이 승격되는 경우에는 이것으로 충분합니다. 하지만 다중 값 속성의 경우 다음 섹션의 설명과 같이 속성에 대해 별개의 테이블을 만들어야 합니다.  
  
## <a name="computed-column-based-on-the-xml-data-type"></a>xml 데이터 형식에 따른 계산 열  
 계산 열은 **xml** 데이터 형식 메서드를 호출하는 사용자 정의 함수를 사용하여 만들 수 있습니다. 계산 열의 유형은 XML을 포함하는 모든 SQL 유형일 수 있습니다. 다음 예에서 확인할 수 있습니다.  
  
### <a name="example-computed-column-based-on-the-xml-data-type-method"></a>예: xml 데이터 형식 메서드에 따른 계산 열  
 책 ISBN 번호에 대한 사용자 정의 함수를 만듭니다.  
  
```  
CREATE FUNCTION udf_get_book_ISBN (@xData xml)  
RETURNS varchar(20)  
BEGIN  
   DECLARE @ISBN   varchar(20)  
   SELECT @ISBN = @xData.value('/book[1]/@ISBN', 'varchar(20)')  
   RETURN @ISBN   
END  
```  
  
 ISBN에 대한 테이블에 계산 열을 추가합니다.  
  
```  
ALTER TABLE      T  
ADD   ISBN AS dbo.udf_get_book_ISBN(xCol)  
```  
  
 계산 열은 일반적인 방식으로 인덱싱될 수 있습니다.  
  
### <a name="example-queries-on-a-computed-column-based-on-xml-data-type-methods"></a>예: xml 데이터 형식 메서드에 따른 계산 열 쿼리  
 ISBN이 0-7356-1588-2인 <`book`>을 가져오려면  
  
```  
SELECT xCol  
FROM   T  
WHERE  xCol.exist('/book/@ISBN[. = "0-7356-1588-2"]') = 1  
```  
  
 다음과 같이 계산 열을 사용하도록 XML 열의 쿼리를 다시 작성할 수 있습니다.  
  
```  
SELECT xCol  
FROM   T  
WHERE  ISBN = '0-7356-1588-2'  
```  
  
 사용자 정의 함수를 만들고 사용하여 **xml** 데이터 형식과 계산 열을 반환할 수 있습니다. 하지만 XML 계산 열에는 XML 인덱스를 만들 수 없습니다.  
  
## <a name="creating-property-tables"></a>속성 테이블 만들기  
 XML 데이터에서 여러 값의 속성 중 일부를 하나 이상의 테이블로 승격시키고 해당 테이블에서 인덱스를 만들고 이를 사용하도록 쿼리를 다시 대상화할 수 있습니다. 일반적인 시나리오는 속성 중 일부에 대부분의 쿼리 작업이 포함되는 경우입니다. 사용할 수 있는 기능은 다음과 같습니다.  
  
-   다중 값 속성을 보유하도록 하나 이상의 테이블을 만듭니다. 테이블마다 하나의 속성을 저장하고 기본 테이블로 다시 조인하기 위해 속성 테이블에 있는 기본 테이블의 기본 키를 중복시키는 것이 편리할 수 있습니다.  
  
-   속성의 상대적 순서를 유지하려면 상대적 순서에 대해 개별 열을 사용해야 합니다.  
  
-   속성 테이블을 유지 관리하기 위해 XML 열에 트리거를 만듭니다. 트리거 내에서 다음 중 하나를 수행합니다.  
  
    -   **nodes()** 및 **value()** 와 같은 **xml**데이터 형식의 메서드를 사용하여 속성 테이블의 행을 삽입 및 삭제합니다.  
  
    -   속성 테이블의 행을 삽입 및 삭제하기 위해 CLR(공용 언어 런타임)에 스트리밍 테이블 반환 함수를 만듭니다.  
  
    -   속성 테이블에 대한 SQL 액세스 및 기본 테이블의 XML 열에 대한 XML 액세스를 위한 쿼리를 작성하고 해당 기본 키를 사용하여 테이블 간 조인을 포함시킵니다.  
  
### <a name="example-create-a-property-table"></a>예: 속성 테이블 만들기  
 이해를 돕기 위해 저자의 이름을 승격해야 한다고 가정해 보십시오. 책에는 한 명 이상의 저자가 있으므로 이름은 다중 값 속성입니다. 각 이름은 속성 테이블의 별개의 행에 저장됩니다. 기본 테이블의 기본 키는 역 조인을 위해 속성 테이블에 중복됩니다.  
  
```  
create table tblPropAuthor (propPK int, propAuthor varchar(max))  
```  
  
### <a name="example-create-a-user-defined-function-to-generate-a-rowset-from-an-xml-instance"></a>예: XML 인스턴스로부터 행 집합을 생성하기 위한 사용자 정의 함수 만들기  
 다음 테이블 반환 함수 udf_XML2Table은 기본 키 값과 XML 인스턴스를 허용합니다. 이 함수는 <`book`> 요소에 대한 모든 저자의 이름을 검색하고 기본 키와 이름의 쌍인 행 집합을 반환합니다.  
  
```  
create function udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (propPK int, propAuthor varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
      select @pk, nref.value('.', 'varchar(max)')  
      from   @xCol.nodes('/book/author/first-name') R(nref)  
      return  
end  
```  
  
### <a name="example-create-triggers-to-populate-a-property-table"></a>예: 속성 테이블을 채우기 위한 트리거 만들기  
 삽입 트리거는 속성 테이블에 행을 삽입합니다.  
  
```  
create trigger trg_docs_INS on T for insert  
as  
      declare @wantedXML xml  
      declare @FK int  
      select @wantedXML = xCol from inserted  
      select @FK = PK from inserted  
  
   insert into tblPropAuthor  
   select * from dbo.udf_XML2Table(@FK, @wantedXML)  
```  
  
 삭제 트리거는 삭제된 행의 기본 키 값에 따라 속성 테이블에서 행을 삭제합니다.  
  
```  
create trigger trg_docs_DEL on T for delete  
as  
   declare @FK int  
   select @FK = PK from deleted  
   delete tblPropAuthor where propPK = @FK  
```  
  
 업데이트 트리거는 업데이트된 XML 인스턴스에 따라 속성 테이블에서 기존 행을 삭제하고 속성 테이블에 새 행을 삽입합니다.  
  
```  
create trigger trg_docs_UPD  
on T  
for update  
as  
if update(xCol) or update(pk)  
begin  
      declare @FK int  
      declare @wantedXML xml  
      select @FK = PK from deleted  
      delete tblPropAuthor where propPK = @FK  
  
   select @wantedXML = xCol from inserted  
   select @FK = pk from inserted  
  
   insert into tblPropAuthor   
      select * from dbo.udf_XML2Table(@FK, @wantedXML)  
end  
```  
  
### <a name="example-find-xml-instances-whose-authors-have-the-same-first-name"></a>예: 저자의 이름이 같은 XML 인스턴스 찾기  
 XML 열에 쿼리를 만들 수 있습니다. 또는 속성 테이블에서 "David"라는 이름을 검색하고 기본 테이블에서 역 조인을 수행하여 XML 인스턴스를 반환할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
SELECT xCol   
FROM     T JOIN tblPropAuthor ON T.pk = tblPropAuthor.propPK  
WHERE    tblPropAuthor.propAuthor = 'David'  
```  
  
### <a name="example-solution-using-the-clr-streaming-table-valued-function"></a>예: CLR 스트리밍 테이블 반환 함수를 사용한 해결 방법  
 이 해결 방법은 다음 단계로 구성됩니다.  
  
1.  ISqlReader를 구현하고 XML 인스턴스에 경로 식을 적용하여 스트리밍 테이블 반환 출력을 생성하는 SqlReaderBase라는 CLR 클래스를 정의합니다.  
  
2.  어셈블리 및 Transact-SQL 사용자 정의 함수를 만들어서 CLR 클래스를 시작합니다.  
  
3.  속성 테이블을 유지 관리하기 위한 사용자 정의 함수를 사용하여 삽입, 업데이트 및 삭제 트리거를 정의합니다.  
  
 이렇게 하려면 먼저 스트리밍 CLR 함수를 만듭니다. **xml** 데이터 형식은 ADO.NET의 관리 클래스 SqlXml로 제공되며 XmlReader를 반환하는 **CreateReader()** 메서드를 지원합니다.  
  
> [!NOTE]  
>  이 섹션의 예제 코드에서는 XPathDocument 및 XPathNavigator가 사용됩니다. 이를 통해 사용자는 모든 XML 문서를 메모리에 강제로 로드할 수 있습니다. 일부 큰 XML 문서를 처리하기 위해 애플리케이션에서 비슷한 코드를 사용하는 경우 이 코드는 확장할 수 없습니다. 대신 메모리 할당을 적게 유지하고 가능한 모든 경우에 스트리밍 인터페이스를 사용합니다. 성능에 대한 자세한 내용은 [CLR 통합 아키텍처](https://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)를 참조하세요.  
  
```  
public class c_streaming_xml_tvf {  
   public static ISqlReader streaming_xml_tvf   
(SqlXml xmlDoc, string pathExpression) {  
      return (new TestSqlReaderBase (xmlDoc, pathExpression));  
   }  
}  
  
// Class that implements ISqlReader  
public class TestSqlReaderBase : ISqlReader {  
XPathNodeIterator m_iterator;           
   public SqlChars FirstName;  
// Metadata for current resultset  
private SqlMetaData[] m_rgSqlMetaData;        
  
   public TestSqlReaderBase (SqlXml xmlDoc, string pathExpression) {     
      // Variables for XPath navigation  
      XPathDocument xDoc;  
      XPathNavigator xNav;  
      XPathExpression xPath;  
  
      // Set sql metadata  
      m_rgSqlMetaData = new SqlMetaData[1];  
      m_rgSqlMetaData[0] = new SqlMetaData ("FirstName",    
SqlDbType.NVarChar,50);     
  
      //Set up the Navigator  
      if (!xmlDoc.IsNull)  
          xDoc = new XPathDocument (xmlDoc.CreateReader());  
      else  
          xDoc = new XPathDocument ();  
      xNav = xDoc.CreateNavigator();  
      xPath = xNav.Compile (pathExpression);  
      m_iterator = xNav.Select(xPath);  
   }  
   public bool Read() {  
      bool moreRows = true;  
      if (moreRows = m_iterator.MoveNext())  
         FirstName = new SqlChars (m_iterator.Current.Value);  
      return moreRows;  
   }  
}  
```  
  
 그런 다음 CLR 함수 streaming_xml_tvf에 해당하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수인 SQL_streaming_xml_tvf(표시 안 됨)와 어셈블리를 만듭니다. 행 집합 생성을 위해 테이블 반환 함수인 CLR_udf_XML2Table을 정의하는 데 사용자 정의 함수가 사용됩니다.  
  
```  
create function CLR_udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (FK int, FirstName varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
   select @pk, FirstName   
   FROM   SQL_streaming_xml_tvf (@xCol, '/book/author/first-name')  
      return  
end  
```  
  
 마지막으로 "속성 테이블을 채우기 위한 트리거 만들기" 예에서 표시된 것과 같이 트리거를 정의하고 udf_XML2Table을 CLR_udf_XML2Table 함수로 바꿉니다. 다음 예에는 삽입 트리거가 표시됩니다.  
  
```  
create trigger CLR_trg_docs_INS on T for insert  
as  
   declare @wantedXML xml  
   declare @FK int  
   select @wantedXML = xCol from inserted  
   select @FK = PK from inserted  
  
   insert into tblPropAuthor  
      select *  
   from    dbo.CLR_udf_XML2Table(@FK, @wantedXML)  
```  
  
 삭제 트리거는 비-CLR 버전과 동일합니다. 하지만 업데이트 트리거는 udf_XML2Table() 함수를 CLR_udf_XML2Table() 함수로 바꿉니다.  
  
## <a name="see-also"></a>참고 항목  
 [계산 열에 XML 사용](../../relational-databases/xml/use-xml-in-computed-columns.md)  
  
  
