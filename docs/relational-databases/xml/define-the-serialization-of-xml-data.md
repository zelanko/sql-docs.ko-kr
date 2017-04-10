---
title: "XML 데이터 직렬화 정의 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "엔터티화 규칙 [SQL Server의 XML]"
  - "직렬화"
  - "직렬화된 XML 구조 다시 구문 분석"
  - "인코딩 [SQL Server의 XML]"
  - "XML [SQL Server], 직렬화"
  - "xml 데이터 형식 [SQL Server], 직렬화"
  - "형식화된 XML"
ms.assetid: 42b0b5a4-bdd6-4a60-b451-c87f14758d4b
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# XML 데이터 직렬화 정의
  xml 데이터 형식을 명시적이나 암시적으로 SQL 문자열 또는 이진 유형으로 캐스팅할 때 xml 데이터 형식의 콘텐츠는 이 항목에 설명된 규칙에 따라 직렬화됩니다.  
  
## 직렬화 인코딩  
 SQL 대상 유형이 VARBINARY인 경우 결과는 UTF-16 바이트 순서 표시가 앞에 표시되어 있지만 XML 선언이 없는 UTF-16으로 직렬화됩니다. 대상 유형이 너무 작으면 오류가 발생합니다.  
  
 예를 들어  
  
```  
select CAST(CAST(N'<Δ/>' as XML) as VARBINARY(MAX))  
```  
  
 다음은 결과입니다.  
  
```  
0xFFFE3C0094032F003E00  
```  
  
 SQL 대상 유형이 NVARCHAR 또는 NCHAR인 경우 결과는 앞에 바이트 순서 표시가 없고 XML 선언이 없는 UTF-16으로 직렬화됩니다. 대상 유형이 너무 작으면 오류가 발생합니다.  
  
 예를 들어  
  
```  
select CAST(CAST(N'<Δ/>' as XML) as NVARCHAR(MAX))  
```  
  
 다음은 결과입니다.  
  
```  
<Δ/>  
```  
  
 SQL 대상 유형이 VARCHAR 또는 NCHAR인 경우 결과는 바이트 순서 표시나 XML 선언이 없이 데이터베이스의 데이터 정렬 코드 페이지에 따른 인코딩으로 직렬화됩니다. 대상 유형이 너무 작거나 값을 대상 데이터 정렬 코드 페이지에 매핑할 수 없는 경우 오류가 발생합니다.  
  
 예를 들어  
  
```  
select CAST(CAST(N'<Δ/>' as XML) as VARCHAR(MAX))  
```  
  
 현재 데이터 정렬의 코드 페이지가 유니코드 문자 Δ를 표현할 수 없으면 이 문이 오류를 발생시키거나 유니코드 문자를 특정 인코딩으로 나타냅니다.  
  
 XML 결과를 클라이언트 쪽에 반환할 때 데이터는 UTF-16 인코딩으로 보내집니다. 그런 다음 클라이언트 쪽 공급자는 해당 API 규칙에 따라 이 데이터를 제공합니다.  
  
## XML 구조의 직렬화  
 **xml** 데이터 형식의 콘텐츠는 일반적인 방식으로 직렬화됩니다. 특히 요소 노드는 요소 태그로 매핑되고 텍스트 노드는 텍스트 콘텐츠로 매핑됩니다. 하지만 문자가 엔터티화되는 경우와 형식화된 원자 값이 직렬화되는 방식은 다음 섹션에 설명됩니다.  
  
## 직렬화 중 XML 문자 엔터티화  
 직렬화된 모든 XML 구조는 다시 구문 분석될 수 있어야 합니다. 따라서 일부 문자는 XML 파서의 정규화 단계를 통해 문자의 왕복 기능을 보존할 수 있도록 엔터티화된 방식으로 직렬화되어야 합니다. 하지만 일부 문자는 문서가 잘 작성되고 따라서 구문 분석될 수 있도록 엔터티화되어야 합니다. 다음은 직렬화 중에 적용되는 엔터티화 규칙입니다.  
  
-   &, \< 및 > 문자는 특성 값이나 요소 콘텐츠 내에 있는 경우 항상 &amp;, &lt; 및 &gt;로 엔터티화됩니다.  
  
-   SQL Server는 특성 값을 묶을 때 따옴표(U+0022)를 사용하기 때문에 특성 값에 있는 따옴표는 &quot;로 엔터티화됩니다.  
  
-   서로게이트 쌍은 서버에서만 캐스팅될 때 단일 숫자 문자 참조로 엔터티화됩니다. 예를 들어 서로게이트 쌍인 U+D800 U+DF00은 숫자 문자 참조인 &\#x00010300;으로 엔터티화됩니다.  
  
-   TAB(U+0009) 및 줄 바꿈(LF, U+000A) 문자가 구문 분석 중에 정규화되지 않도록 보호하기 위해 이러한 문자는 특성 값 내에서 해당 숫자 문자 참조인 &\#x9; 및 &\#xA;로 엔터티화됩니다.  
  
-   캐리지 리턴(CR, U+000D) 문자가 구문 분석 중에 정규화되지 않도록 보호하기 위해 이러한 문자는 특성 값 및 요소 콘텐츠 내에서 해당 숫자 문자 참조인 &\#xD;로 엔터티화됩니다.  
  
-   공백만 포함된 텍스트 노드를 보호하기 위해 공백 문자 중 하나(일반적으로 마지막 공백 문자)는 해당 숫자 문자 참조로 엔터티화됩니다. 이러한 방식으로 다시 구문 분석 과정에서 구문 분석 중의 공백 처리 설정에 관계없이 공백 문자 텍스트 노드를 보존합니다.  
  
 예를 들어  
  
```  
declare @u NVARCHAR(50)  
set @u = N'<a a="  
    '+NCHAR(0xD800)+NCHAR(0xDF00)+N'>">   '+NCHAR(0xA)+N'</a>'  
select CAST(CONVERT(XML,@u,1) as NVARCHAR(50))  
```  
  
 다음은 결과입니다.  
  
```  
<a a="  
    𐌀>">     
</a>  
```  
  
 마지막 공백 보호 규칙을 적용하지 않으려면 **xml**에서 문자열이나 이진 유형으로 캐스팅할 때 명시적 CONVERT 옵션 1을 사용하면 됩니다. 예를 들어 엔터티화를 방지하려면 다음을 수행할 수 있습니다.  
  
```  
select CONVERT(NVARCHAR(50), CONVERT(XML, '<a>   </a>', 1), 1)  
```  
  
 [query() 메서드(xml 데이터 형식)](../../t-sql/xml/query-method-xml-data-type.md)는 xml 데이터 형식 인스턴스를 반환합니다. 따라서 문자열이나 이진 유형으로 캐스팅된 **query()** 메서드의 결과는 앞에서 설명한 규칙에 따라 엔터티화됩니다. 엔터티화되지 않은 문자열 값을 가져오려면 대신 [value() 메서드(xml 데이터 형식)](../../t-sql/xml/value-method-xml-data-type.md)를 사용해야 합니다. 다음은 **query()** 메서드를 사용하는 예제입니다.  
  
```  
declare @x xml  
set @x = N'<a>This example contains an entitized char: <.</a>'  
select @x.query('/a/text()')  
```  
  
 다음은 결과입니다.  
  
```  
This example contains an entitized char: <.  
```  
  
 다음은 **value()** 메서드를 사용하는 예제입니다.  
  
```  
select @x.value('(/a/text())[1]', 'nvarchar(100)')  
```  
  
 다음은 결과입니다.  
  
```  
This example contains an entitized char: <.  
```  
  
## 형식화된 xml 데이터 형식 직렬화  
 형식화된 **xml** 데이터 형식 항목에는 해당 XML 스키마 유형에 따라 형식화된 값이 포함됩니다. 이러한 값은 xs:string으로 캐스팅된 XQuery가 만드는 형식과 동일한 형식으로 해당 XML 스키마 유형에 따라 직렬화됩니다. 자세한 내용은 [XQuery의 형식 캐스트 규칙](../../xquery/type-casting-rules-in-xquery.md)을 참조하세요.  
  
 예를 들어 xs:double 값 1.34e1은 아래 예에서와 같이 13.4로 직렬화됩니다.  
  
```  
declare @x xml  
set @x =''  
select CAST(@x.query('1.34e1') as nvarchar(50))  
```  
  
 이 예에서는 문자열 값 13.4를 반환합니다.  
  
## 참고 항목  
 [XQuery의 캐스트 규칙](../../xquery/type-casting-rules-in-xquery.md)   
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  