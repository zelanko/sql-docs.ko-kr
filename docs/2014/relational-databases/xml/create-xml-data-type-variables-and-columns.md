---
title: XML 데이터 형식 변수 및 열 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xml data type [SQL Server], variables
- xml data type [SQL Server], columns
ms.assetid: 8994ab6e-5519-4ba2-97a1-fac8af6f72db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fe1414131991a35b316a50da730f42e8b02d462
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62637996"
---
# <a name="create-xml-data-type-variables-and-columns"></a>XML 데이터 형식 변수 및 열 만들기
  
  `xml` 데이터 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 제공 데이터 형식이며 `int` 및 `varchar`와 같은 다른 기본 제공 유형과 비슷한 점이 있습니다. 다른 기본 제공 유형과 마찬가지로 변수 유형, 매개 변수 유형, `xml` 함수 반환 유형 또는 [CAST 및 CONVERT](/sql/t-sql/functions/cast-and-convert-transact-sql)로 테이블을 만들 때 데이터 형식을 열 유형으로 사용할 수 있습니다.  
  
## <a name="creating-columns-and-variables"></a>열 및 변수 만들기  
 다음 예에서와 같이 테이블의 일부분으로 `xml` 유형 열을 만들려면 `CREATE TABLE` 문을 사용합니다.  
  
```  
CREATE TABLE T1(Col1 int primary key, Col2 xml)   
```  
  
 다음 예에서와 같이 `DECLARE statement` 문을 사용하여 `xml` 유형의 변수를 만들 수 있습니다.  
  
```  
DECLARE @x xml   
```  
  
 다음 예에서와 같이 XML 스키마 컬렉션을 지정하여 형식화된 `xml` 변수를 만듭니다.  
  
```  
DECLARE @x xml (Sales.StoreSurveySchemaCollection)  
```  
  
 다음 예에서와 같이 저장된 프로시저로 `xml` 유형 매개 변수를 전달하려면 `CREATE PROCEDURE` 문을 사용합니다.  
  
```  
CREATE PROCEDURE SampleProc(@XmlDoc xml) AS ...   
```  
  
 XQuery를 사용하여 열, 매개 변수 또는 변수에 저장된 XML 인스턴스를 쿼리할 수 있습니다. 또한 XML DML(XML 데이터 조작 언어)을 사용하여 XML 인스턴스에 업데이트를 적용할 수도 있습니다. XQuery 표준에서는 개발 당시 XQuery DML을 정의하지 않았으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [XML 데이터 수정 언어](/sql/t-sql/xml/xml-data-modification-language-xml-dml) 확장을 XQuery에 도입합니다. 이러한 확장을 사용하여 작업을 삽입, 업데이트 및 삭제할 수 있습니다.  
  
## <a name="assigning-defaults"></a>기본값 할당  
 테이블에서 `xml` 유형의 열에 기본 XML 인스턴스를 할당할 수 있습니다. 기본 XML을 제공할 수 있는 방법으로는 XML 상수를 사용하거나 `xml` 유형으로 명시적 캐스트를 사용하는 두 가지 방법 중 하나가 있습니다.  
  
 XML 상수로 기본 XML을 제공하려면 다음 예에서와 같이 구문을 사용합니다. 문자열은 `xml` 유형으로 암시적으로 CAST가 수행됩니다.  
  
```  
CREATE TABLE T (XmlColumn xml default N'<element1/><element2/>')  
```  
  
 명시적 `CAST` 로써 기본 XML을 `xml`에 제공하려면 다음 예에서와 같이 구문을 사용합니다.  
  
```  
CREATE TABLE T (XmlColumn xml   
                  default CAST(N'<element1/><element2/>' AS xml))  
```  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 `xml` 유형의 열에서 NULL과 NOT NULL 제약 조건도 지원합니다. 다음은 그 예입니다.  
  
```  
CREATE TABLE T (XmlColumn xml NOT NULL)  
```  
  
## <a name="specifying-constraints"></a>제약 조건 지정  
 
  `xml` 유형의 열을 만들 때 열 수준이나 테이블 수준 제약 조건을 정의할 수 있습니다. 다음 경우에 제약 조건을 사용합니다.  
  
-   비즈니스 규칙을 XML 스키마에 표현할 수 없습니다. 예를 들어 꽃 판매점의 배달 주소는 해당 영업소 위치에서 81km 이내에 있어야 합니다. 이러한 사항은 XML 열에 대한 제약 조건으로 작성될 수 있습니다. 제약 조건에는 `xml` 데이터 형식의 메서드가 포함될 수 있습니다.  
  
-   제약 조건에 테이블의 XML 또는 비-XML 열이 포함됩니다. 한 예는 관계형 CustomerID 열에 있는 값과 일치하는 XML 인스턴스에 있는 고객의 ID(`/Customer/@CustId`)에 대한 강제 적용입니다.  
  
 형식화되거나 형식화되지 않은 `xml` 데이터 형식 열에 대해 제약 조건을 지정할 수 있습니다. 그러나 제약 조건을 지정할 때 [XML 데이터 형식 메서드](/sql/t-sql/xml/xml-data-type-methods) 를 사용할 수 없습니다. 또한 `xml` 데이터 형식은 다음 열 및 테이블 제약 조건을 지원하지 않습니다.  
  
-   PRIMARY KEY/ FOREIGN KEY  
  
-   UNIQUE  
  
-   COLLATE  
  
     XML은 자체 인코딩을 제공합니다. 데이터 정렬은 문자열 유형에만 적용됩니다. 
  `xml` 데이터 형식은 문자열 유형이 아닙니다. 하지만 문자열 표현이 있으며 문자열 데이터 형식으로 캐스팅할 수 있습니다.  
  
-   RULE  
  
 대신 다음 예처럼 사용자 정의 함수인 래퍼를 만들어 `xml` 데이터 형식 메서드를 래핑하고 CHECK 제약 조건에 사용자 정의 함수를 지정합니다.  
  
 다음 예에서 `Col2` 의 제약 조건은 이 열에 저장된 각 XML 인스턴스가 `<ProductDescription>` 특성을 포함하는 `ProductID` 요소를 갖도록 지정합니다. 이 제약 조건은 사용자 정의 함수에 의해 적용됩니다.  
  
```  
CREATE FUNCTION my_udf(@var xml) returns bit  
AS BEGIN   
RETURN @var.exist('/ProductDescription/@ProductID')  
END  
GO  
```  
  
 인스턴스의 `exist()` 요소에 `xml` 특성이 있으면 `1` 데이터 형식의 `<ProductDescription>` 메서드가 `ProductID` 을 반환합니다. 그렇지 않으면 `0`을 반환합니다.  
  
 이제 다음과 같이 열 수준 제약 조건을 가진 테이블을 만들 수 있습니다.  
  
```  
CREATE TABLE T (  
    Col1 int primary key,   
    Col2 xml check(dbo.my_udf(Col2)=1))  
GO  
```  
  
 다음이 삽입됩니다.  
  
```  
INSERT INTO T values(1,'<ProductDescription ProductID="1" />')  
```  
  
 제약 조건 때문에 다음은 삽입되지 않습니다.  
  
```  
INSERT INTO T values(1,'<Product />')  
```  
  
## <a name="same-or-different-table"></a>같은 테이블 또는 다른 테이블  
 다른 `xml` 관계형 열이 포함 된 테이블 또는 주 테이블에 대 한 외래 키 관계가 있는 별도의 테이블에 데이터 형식 열을 만들 수 있습니다.  
  
 다음 조건 `xml` 중 하나에 해당 하는 경우 동일한 테이블에 데이터 형식 열을 만듭니다.  
  
-   애플리케이션이 XML 열에서 데이터 검색을 수행하고 XML 열에 XML 인덱스가 필요하지 않습니다.  
  
-   
  `xml` 데이터 형식의 열에 XML 인덱스를 작성하려고 하며 기본 테이블의 기본 키는 해당 클러스터링 키와 같습니다. 자세한 내용은 [XML 인덱스&#40;SQL Server&#41;](xml-indexes-sql-server.md)를 참조하세요.  
  
 다음 조건에 맞는 경우 별개의 테이블에 `xml` 데이터 형식의 열을 만듭니다.  
  
-   
  `xml` 데이터 형식의 열에 XML 인덱스를 작성하려고 하지만 기본 테이블의 기본 키가 해당 클러스터링 키와 다르거나, 기본 테이블에 기본 키가 없거나, 기본 테이블이 힙(비 클러스터링 키)입니다. 기본 테이블이 이미 있는 경우에는 이 조건에 부합될 수 있습니다.  
  
-   테이블에 있는 XML 열로 인해 테이블 검색 속도가 느려지는 것을 원치 않습니다. XML 열은 행 안에 있든 행 밖에 있든 간에 공간을 사용합니다.  
  
  
